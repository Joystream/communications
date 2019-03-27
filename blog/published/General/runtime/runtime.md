On-chain Consensus Upgrades Without Hardforks
=============================================

One of the main requirements we had deciding on which framework to build on, was the ability to do consensus upgrades through an on-chain governance system. In this blog post, we will provide both a practical and technical explanation of the why and how.

Runtime Upgrades vs Hardforks
-----------------------------

Everyone that has been following this space for a while have seen that hardforks are tricky. Looking at the two most well-known blockchains, e.g. Bitcoin and Ethereum, hardforks (and threats of them) have lead to [never-ending debates](https://en.bitcoin.it/wiki/Block_size_limit_controversy), [power struggles](https://bitcoinexchangeguide.com/new-craig-wright-and-roger-ver-twitter-feud-after-bangkok-meeting-leads-to-new-questions/), [organizational nightmares](https://decryptmedia.com/4520/constantinople-ethereum-hard-fork-upgrade-delay-postponed), and finally [schisms](https://en.wikipedia.org/wiki/Ethereum_Classic).

![](https://blog.joystream.org/content/images/2019/03/20904663876_287f1aeeff_z.jpg)

Some forks breaks

In the case of Bitcoin, this has lead to an unwillingness to even consider hardforking for a large part of the ecosystem, leading to significant [kludge](https://en.wikipedia.org/wiki/Kludge) (ref [segwit](https://en.bitcoin.it/wiki/Segregated_Witness)). There is a strong argument to be made this is actually a strength for a project of Bitcoin's scope and size. That is not to say all projects should adopt this approach.

![](https://blog.joystream.org/content/images/2019/03/7959772300_7805e85cd6_z.jpg)

Tech moves fast

For a media platform like Joystream, there are a number of non system critical changes that will have to be made as the project gains traction, e.g. changing parameters like [`transfer_fee`](https://github.com/Joystream/substrate-node-joystream/blob/master/src/chain_spec.rs/#L142) and [`validator_count`](https://github.com/Joystream/substrate-node-joystream/blob/master/src/chain_spec.rs/#L164). For a protocol as rigorous as that of Bitcoins, similar changes would require a hardfork. For a protocol built on the Substrate framework, these can be changed trivially with a single [extrensic](https://wiki.parity.io/Extrinsic) (for simplicity, we will just call it transaction) if the pre-defined governance mechanism elects to do so.

Another application for runtime upgrades can be to fix bugs. Joystream has already gone through one upgrade to fix a bug where validators were not able to `unstake`. A fix implemented in this [PR](https://github.com/Joystream/substrate-node-joystream/pull/44) followed by a `sudo` transaction (next section) automatically updated the consensus code for all current and future nodes on the network in flight, without anyone having to upgrade their software.

What are Runtime Upgrades
-------------------------

For the less technically inclined, a quick and dirty way of defining the runtime is simply the way a program executes and runs. This includes certain aspects of the code, which has an impact both on the consensus, efficiency and behavior. The paragraphs will focus on the consensus aspect of the runtime.

For a substrate based blockchain like Joystream, the initial [runtime](https://wiki.parity.io/Runtime.html) is part of the genesis block as a [WASM](https://webassembly.org/) image. This means that when a validator produces a block, it must follow all the rules as defined in the runtime, or it will be rejected by the other validators and nodes on the network.

#### Requirements for Upgrading

In our [genesis](https://github.com/Joystream/substrate-node-joystream/blob/39600bdd5582a18c1337458497b3f740a447a3fa/src/chain_spec.rs) runtime, we included two mechanisms for allowing an upgrade to happen:

1.  Directly with a transaction signed by `sudo.key`
2.  Through a runtime upgrade proposal transaction

![](https://blog.joystream.org/content/images/2019/03/ilu_blog.png)

The `sudo.key` address can be found by accessing the testnet UI [settings](https://sparta.joystream.org/apps/#/settings), and changing to `Fully featured` interface. Then, access the `Chain state` from the sidebar, select `Sudo` from the `selected state query` drop down menu, and click the `+` button on the right. We in Jsgenesis control the private key corresponding to this address, allowing us to force through changes. This feature will be removed either when the platform goes live on mainnet, or shortly after a transitional period. Even now, we intend to use it scarcely as possible.

![](https://blog.joystream.org/content/images/2019/03/Council-1.png)

For voting through the new runtime, a [proposal](https://sparta.joystream.org/apps/#/proposals) must first be submitted to the council. If the proposal reaches `[approval_quorum](https://github.com/Joystream/substrate-node-joystream/blob/03f87d875098511caea98d42b233bf12e3d66999/src/chain_spec.rs/#L187)` within the `[voting_period](https://github.com/Joystream/substrate-node-joystream/blob/03f87d875098511caea98d42b233bf12e3d66999/src/chain_spec.rs/#L191)`, the proposed runtime upgrade is automatically deployed to the network. In future testnets and mainnet, there will be some extra checks and balances depending on which parameters of the consensus code is changed.

Perhaps the most interesting aspect of this is that a successful runtime upgrade can introduce new rules and mechanisms for making future runtime changes.

![](https://blog.joystream.org/content/images/2019/03/meta-2.jpeg)

Doge approves

#### The Mechanics of an Upgrade

As described above, after a transaction containing a new WASM image of the runtime is submitted to the chain, the validators will check whether the requirements in  `1.` or  `2.` have been fulfilled. This is necessary because everyone can actually send a transaction that *tries* to upgrade.

Currently, validator nodes cannot verify the code itself. When a runtime proposal is made the burden is on the council members to follow a procedure to verify the quality and correctness of the proposed runtime (in a future post we will share one possible approach for doing this).

> In the future, we plan on building in a module where this WASM image is compiled locally on each validator machine, and verify that the checksum matches that of the proposal voted through. This will provide an extra layer of security, as it can be proven deterministically both that the code is the same for every validator, and that it matches that of the proposal. Thus confirming all the tests and scrutiny the platforms software developers has done applies.

Assuming the sudo transaction was indeed valid, or after a proposal has been passed by the council, the new runtime will be stored on chain. At the next block all blocks produced must follow the new consensus rules included in the new runtime in order to avoid being invalidated and thus forked off.

Conclusion
----------

As with all software implementations, there are trade-offs and compromises. Validators and nodes can manually configure the code to outright reject certain types of transactions or collude to force through their own upgrades if they feel threatened. Bugs can knock-out the whole network simultaneously and chain splits can still occur in certain circumstances. Just as for other blockchains, the former has to be resolved through governance and incentives, whereas the latter depends on the the fail-safe mechanisms and quality of the of tools, engineers and QA practices.

![](https://blog.joystream.org/content/images/2019/03/5097486285_dee7125140_z.jpg)

Different strokes

In sum, we believe that this system is the best for the Joystream blockchain, as it needs to be adaptive and responsive to rapid changes of circumstances. Examples can include things like quickly increasing the budget for `storage providers` or `membership screeners` if some nodes go offline, or there is a burst of new membership applicants after an article or publicity event occurs. If every participant had to manually or forcible upgrade their software from some repository every time, it would be an organizational challenge at best or an attack vector at worst.

* * * * *

###### Disclaimer

All forward looking statements, estimates and commitments found in this blog post should be understood to be highly uncertain, not binding and for which no guarantees of accuracy or reliability can be provided. To the fullest extent permitted by law, in no event shall Joystream, Jsgenesis or our affiliates, or any of our directors, employees, contractors,  service providers or agents have any liability whatsoever to any person  for any direct or indirect loss, liability, cost, claim, expense or  damage of any kind, whether in contract or in tort, including negligence, or otherwise, arising out of or related to the use of all or  part of this post, or any links to third party websites.