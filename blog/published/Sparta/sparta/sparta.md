Sparta Released
===============

We have previously written about [why](https://blog.joystream.org/pay-for-play/) we are paying users monero to participate on our testnet, and [how](https://blog.joystream.org/sparta-incentives-structure/) much you can make. This post aims to explain what you can do to earn real money on testnet!

![](https://blog.joystream.org/content/images/2019/02/10.png)

![](https://blog.joystream.org/content/images/2019/02/20.png)

![](https://blog.joystream.org/content/images/2019/02/100.png)

After launching our first testnet on Tendermint using the cosmos SDK before [christmas](https://blog.joystream.org/mesopotamia/), we have become more convinced [Polkadot](https://polkadot.network/) and [Substrate](https://github.com/paritytech/substrate) are the better choice for purpose. There are always trade offs when choosing between different software package solutions, but in sum we are quite confident in our choice. If you want to learn more about the Joystream project, please consult our [whitepaper](https://github.com/Joystream/whitepaper/blob/master/paper.pdf).

How to claim your rewards
-------------------------

If you successfully have become a Validator or Council Member, you need to prove your monero address by putting your XMR address in the `My memo` tab under `My Accounts` sidebar. (Note that this feature this not work with zero balance.)

```
# Format:
"4or8YourXmrAddressInDoubleQuotesAndNothingElse"
```

If you want to skip straight to the Validator setup tutorial, follow [this link](https://blog.joystream.org/sparta/#validator).

Become a Council Member
-----------------------

![](https://blog.joystream.org/content/images/2019/02/Council-3.svg)

Being a council member requires no downloads or software installation. Go to our browser based UI, and [create your account](https://sparta.joystream.org/apps/#/accounts) now. The first election will be held on the 5th of March. There are four stages in the election cycle:

### Initial Stage

The stage before the first Announcement stage. During this stage, you can accumulate `JOY` tokens before the election cycle starts.

### Announcement Stage

-   Starts : `block 65,000` (05.03.19, ~12:00 GMT)
-   Lasts : `43,200 blocks` (3 days)

In this stage, anyone with sufficient `JOY` tokens (one trip to the faucet) can announce their candidacy. Go to `Council` in the sidebar, and click on the `Applicants` tab. Here you can set the amount of tokens you wish to stake (you can add more at any time during the announcement stage). After sending the transaction, you should appear under "Applicants". The max number of Applicants is `25`. When the 25th candidate applies, the one with the lowest amount staked will be pushed off the list, and get their stake returned. Maximum `12` Council Members can be elected.

### Voting Stage

-   Starts : `block 108,200` (08.03.19, ~12:00 GMT)
-   Lasts : `14,400 blocks` (1 day)

After n blocks (d days), the Announcement Stage closes, and you can begin voting for applicants. As with everything else, you need to stake in order to do so. Joystream is currently working under the "One Token - One Vote" principal. Go to the `Votes` tab, set your staking amount, select your candidate and generate a `Random salt`. This will be needed to reveal and actually "broadcast" your vote. You can vote more than once, and for more than one applicant.

### Reveal Stage

-   Starts : `block 122,600` (09.03.19, ~12:00 GMT)
-   Lasts : `14,400 blocks` (1 day)

After n blocks, the Voting Stage closes, and the Revealing stage begins. This is when you can reveal your vote. Go to the `Reveal a vote` tab, to actually broadcast your vote. Votes that are not revealed in time will not get counted in the election.

### Term Stage

-   Starts : `block 137,000` (10.03.19, ~12:00 GMT)
-   Lasts: `201,600 blocks` (14 days)

At this stage, all users can make proposals, which the Council Members have `28,800 blocks` (2 days) to vote on. After the Term Stage is over, we are back in the Announcement Stage.

Become a Validator
------------------

![](https://blog.joystream.org/content/images/2019/02/Block_carving-7.svg)

This is a step by step guide to become a validator on the Sparta Testnet. If you are comfortable with the command line and want to build from source, go to our [node-repo](https://github.com/Joystream/substrate-node-joystream) and (optionally) the [UI-repo](https://github.com/Joystream/apps/tree/joystream), to get started. Instructions for [Windows](https://blog.joystream.org/sparta/#windows), [Mac](https://blog.joystream.org/sparta/#unix) and [Linux](https://blog.joystream.org/sparta/#unix) (debian based, 64 bits).

-   Download and set up a full node
-   Launch the UI
-   Become a validator

On Windows
----------

### General Notes

Every time something is written in `<brackets>`, this means you have  to replace this with your input - without the `<>`. For terminal  commands, `>` and `$` means you must type what comes after that on windows and mac respectively. `#` Means it's just a comment/explanation, and must not be typed.

```
# On Windows:
> do_xyz
# On Mac/Linux
$ ./do_xyz
```

Means you must type/paste exactly `do_xyz` or `./do_xyz`.

### Install and start a full node

Get the binary [here](https://github.com/Joystream/substrate-node-joystream/releases/download/v0.10.1/joystream-node-win-x86_64.zip). To make the actual commands the same for all users, I'm going to save and unzip to `C:\joystream-node-windows-x64`. Feel free to store it somewhere else, just make sure you use the correct path.

If you don't have it, download Microsoft Visual Studio C++ runtime distributable 2015 [here](https://www.microsoft.com/en-ie/download/details.aspx?id=48145).  

Get the missing ssl libraries [here](https://indy.fulgan.com/SSL/openssl-1.0.2q-x64_86-win64.zip), extract, and move the files `ssleay32.dll` and `libeay32.dll` to `C:\joystream-node-windows-x64`.

Open `Command Prompt` (type in cmd... after clicking windows button):

```
> cd C:\joystream-node-windows-x64
> joystream-node.exe
# If you want your node to have a public name:
> joystream-node.exe --name <nodename>

```

This should start your full node. Note that this window has to stay open in order to keep your node running!

### Launch the UI

To get started right away, go to the UI [website](https://sparta.joystream.org/apps/#/accounts) and connect to you full node by changing the `remote node/endpoint` to `Local Node` under `Settings`.

If you'd rather go the advanced route, and install the UI App locally, instructions can be found [here](https://blog.joystream.org/p/8e8f08a6-08d5-4a64-9f08-08aedd0d5719/). **Note that there are no extra benefits or features with this option.**

### Become a validator

*Note that there may be competition for this spot, so be prepared to fight!*

If you chose not to download the UI locally, go [here](https://sparta.joystream.org/apps/#/accounts) to access to same UI. Go to `settings`, and and change the remote node/endpoint to Local Node (127.0.0.1:9944) to have it point to your own node.

In the app, open `My Account` in sidebar, and create a new account. Make sure to select `raw seed` instead of `mnemonic` and save the `raw seed` somewhere. Back up the account if you wish, it will be called `5MyAddress.json`. Then go to the `Faucet`, and claim tokens. After they are received, navigate to `Validators`. Check the current status, to find out how much you need to stake to get accepted, and click the `Validator staking` tab. Stake the amount of tokens you want to stake. Navigate back to `Validators` and your address should show under `next up`.

Now, go to the terminal window where your node is running, and stop it using ctrl+c. Take your  `raw seed` from wherever you saved it, then:

```
> joystream-node.exe --validator --key <raw seed>
# add --name <nodename> at the end if you want to
```

You will become a validator in the next era! Remember to keep your node command prompt window open at all times to keep validating. If you do want to stop validating, `unstake` your funds and wait for the next era to avoid getting slashed.

You should see your node listed on the [network status site](https://telemetry.polkadot.io/#/Joystream%20Testnet%20v1).

On Mac/Linux
------------

### Install and start the node

Get the binary for Mac [here](https://github.com/Joystream/substrate-node-joystream/releases/download/v0.10.1/joystream-node-osx-x86_64.zip), Linux [here](https://github.com/Joystream/substrate-node-joystream/releases/download/v0.10.1/joystream-node-linux-gnu-x86_64.zip) or use `wget` as shown in the beginning of the code block. Open the terminal, and do the following on your Mac:

```
# Get the binary with wget:
$ cd
$ wget https://github.com/Joystream/substrate-node-joystream/releases/download/v0.10.1/joystream-node-osx-x86_64.zip
-----
# If you downloaded it with the link:
$ cd
$ cp ~/Downloads/joystream-node-osx-x86_64.zip ~/
-----
# Regardless
$ tar -vxf joystream-node-osx-x86_64.zip
$ ./joystream-node
# If you want your node to have a public name:
$ ./joystream-node --name <nodename>
```

On linux:

```
# Get the binary with wget:
$ cd
$ wget https://github.com/Joystream/substrate-node-joystream/releases/download/v0.10.1/joystream-node-linux-gnu-x86_64.zip
-----
# If you downloaded it with the link:
$ cd
$ cp ~/joystream-node-linux-gnu-x86_64.zip ~/
-----
# Regardless
$ sudo apt-get install unzip
$ unzip joystream-node-linux-gnu-x86_64.zip
$ ./joystream-node
# If you want your node to have a public name:
$ ./joystream-node --name <nodename>
```

### Launch the UI

To get started right away, go to the UI [website](https://sparta.joystream.org/apps/#/accounts) and connect to you full node by changing the `remote node/endpoint` to `Local Node` under `Settings`.

If you'd rather go the advanced route, and install the UI App locally, instructions can be found [here](https://blog.joystream.org/p/8e8f08a6-08d5-4a64-9f08-08aedd0d5719/). **Note that there are no extra benefits or features with this option.**

### Become a validator

*Note that there may be competition for this spot, so be prepared to fight!*

If you chose not to download the UI locally, go [here](https://sparta.joystream.org/apps/#/accounts) to access to same UI. Go to settings, and and change the remote node/endpoint to Local Node (127.0.0.1:9944) to have it point to your own node.

In the app, open `My Account` in sidebar, and create a new account. Make sure to select `raw seed` instead of `mnemonic` and save the `raw seed` somewhere. Back up the account if you wish, it will be called `5MyAddress.json`. Then go to the `Faucet`, and claim tokens. After they are received, navigate to `Validators`. Check the current status, to find out how much you need to stake to get accepted, and click the `Validator staking` tab. Stake the amount of tokens you want to stake. Navigate back to `Validators` and your address should show under `next up`.

Now, go to the terminal window where your node is running, and stop it using ctrl+c. Take your  `raw seed` from wherever you saved it, then:

```
$ ./joystream-node --validator --key <raw seed>
# add --name <nodename> at the end if you want to
```

You will become a validator in the next era! Remember to keep your node command prompt window open at all times to keep validating. If you do want to stop validating, `unstake` your funds and wait for the next era to avoid getting slashed.

You should see your node listed on the [network status site](https://telemetry.polkadot.io/#/Joystream%20Testnet%20v1).

* * * * *

###### Disclaimer

All forward looking statements, estimates and commitments found in this blog post should be understood to be highly uncertain, not binding and for which no guarantees of accuracy or reliability can be provided. To the fullest extent permitted by law, in no event shall Joystream, Jsgenesis or our affiliates, or any of our directors, employees, contractors,  service providers or agents have any liability whatsoever to any person  for any direct or indirect loss, liability, cost, claim, expense or  damage of any kind, whether in contract or in tort, including negligence, or otherwise, arising out of or related to the use of all or  part of this post, or any links to third party websites.