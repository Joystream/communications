# Post

#### Title

Announcing Acropolis

#### Purpose

Announcing our next testnet, Acropolis

#### url

blog.joystream.org/announcing-acropolis/

#### Cover



#### Lead

After the launch `Athens` on mid April, we have fully shifted our attention to our next testnet - `Acropolis`.

#### Body

What is Acropolis
-----------------

As the name might suggest, our intention is for Acropolis to build on, and improve on some of the issues we encountered with the [launch of Athens](https://blog.joystream.org/athens-released/). If you are a frequent flyer, or at least have given the [Athens testnet](https://testnet.joystream.org) a spin, you are already familiar with the problems we had with the `Storage Provider` role, and the recurring [network connectivity problems](https://github.com/Joystream/substrate-node-joystream/issues/68).

Our primary focus with Acropolis can be read from our release [OKR](https://en.wikipedia.org/wiki/OKR), shown below:

#### Objective: Launch Acropolis Network

1.  `Get 75 posts on forum (limits, not Jsg)`
2.  `Forum (runtime), storage (runtime and P2P) fully specd`
3.  `Have 4x replication for all 2 tranches on storage node`
4.  `95% uptime Storage Provider`
5.  `No PRs merged to master (excluding bugfixes and "pioneer") after "Sub-system Test"`

In line with the project goal of openness and transparency, you can find more details in the [release plan](https://github.com/Joystream/joystream/tree/master/testnets/acropolis), and learn more about the project, releases, planning, collaboration in general [here](https://github.com/Joystream/joystream).

Upgrade
-------

As you can see from the OKR, the network connectivity issue is not addressed. We are currently considering three ways of dealing with this message that everyone that has run a node will recognize:

```
Banning PeerId("QmWp8TCAP5nmcsrefaxPgwWpEzUyUh1s1h6BmGNMbvWDCD") because "Peer is on different chain (our genesis: 0x78be...87c7 theirs: 0xf9e2...c2ba)"
```

1.  Accept the problem, and help the community with work arounds to alleviate the problem `*`
2.  Reconsider our [intention](https://github.com/Joystream/joystream/tree/master/testnets/acropolis#deployment) to do an [on-chain upgrade](https://blog.joystream.org/upgrades/), and start from a new genesis block, with a new `[protocolId](https://github.com/Joystream/substrate-node-joystream/issues/69)`
3.  Keep the genesis block (and thus chain) but hardfork in a new `[protocolId](https://github.com/Joystream/substrate-node-joystream/issues/69)`. This would require users to download a new binary, or pass the `--chain /path/to/new/chain-spec.json` flag to their "old" node.

`*` Restarting your node at regular intervals, combined with passing `--in-peers n --out-peers m` where `m` and `n` is larger than 25. The higher the number, the more memory intensive.

Contribute
----------

Although Joystream is currently controlled by us at Jsgenesis, our goal has always been, and still is, to withdraw and leave it to our community. In order for that transition to work smoothly, we need contributors. Just participating on our testnets is helping us immensely (hence why we pay monero for doing so), but we need help in other ways as well.

Developers can report issues or make PRs to [our repos](https://github.com/Joystream), following our [standard rules](https://github.com/Joystream/joystream#contribute). In addition to the [small bounties](https://github.com/JoyStream/helpdesk#builders-and-bug-reporters) we promise for small "patches", feel free to contact us anywhere if you have something larger in mind.

Finally, for the less technical, we currently have an open bounty: [Proposal for improving network issues, while promoting Joystream](https://github.com/Joystream/joystream/issues/39).



#### Disclaimer

All forward looking statements, estimates and commitments found in this blog post should be understood to be highly uncertain, not binding and for which no guarantees of accuracy or reliability can be provided. To the fullest extent permitted by law, in no event shall Joystream, Jsgenesis or our affiliates, or any of our directors, employees, contractors,  service providers or agents have any liability whatsoever to any person  for any direct or indirect loss, liability, cost, claim, expense or  damage of any kind, whether in contract or in tort, including negligence, or otherwise, arising out of or related to the use of all or  part of this post, or any links to third party websites.

#### Preview



#### Social media card cover



#### Social media excerpt

After the launch `Athens` on mid April, we have fully shifted our attention to our next testnet - `Acropolis`.
