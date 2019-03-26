Launching Testnet - Mesopotamia
===============================

As we announced in our final blog posts on medium, we have released our first Testnet - codenamed Mesopotamia.

Goals
-----

Our goals with this release are to get familiar with the framework, test the functionality of [Tendermint](https://tendermint.com/) and the [Cosmos SDK](https://cosmos.network/), and give our community a taste of where the project is heading.

Although there are a limited set of features at this stage, we hope some of you will join in testing, give some feedback, and prepare yourselves to be full node operators and validators on future releases.

If you're comfortable with the command line and want to compile from source, please visit our [github repo](https://github.com/Joystream/joystream-manual) to get started. The latest binaries can be found [here](https://github.com/Joystream/joystream-builder/releases). If you are interested in the project, but need a little more help to get started, continue with the tutorial below!

Tutorial
--------

This is a step by step guide to getting a full node up and running on the Joystream Testnet, with the option of becoming a validator. The instructions are divided into four sections, and given for both Windows and Mac users.

-   Download and install the binaries
-   Setup your account and start your full node
-   Get JOY tokens from the faucet
-   Become a validator

For linux users that doesn't wish to compile the binaries, the instructions should be very similar to those on Mac. If you need any extra help, feel free to reach out on [Telegram](https://t.me/joinchat/CNyeUxHD9H56m3e_44hXIA), [Twitter](https://twitter.com/JoystreamApp) or [Reddit](https://www.reddit.com/r/JoyStream/)!

### General Notes

Every time something is written in 'single_quotes', this means you have to replace this with your input - without the quotes. For terminal commands, `>` and `$` means you must type what comes after that on windows and mac respectively.

Assuming `joystream1hh4egjkafgxn7q26zxgsuz8tw9k8ur2dfefntz` is your address, and you want to check your balance, the following instruction...

```
#On windows
> joycli query account 'joystream_address' --chain-id joy-testnet-1000
#On Mac
$ ./joycli query account 'joystream_address' --chain-id joy-testnet-1000
```

...means you must paste/type exactly:

`joycli query account joystream1hh4egjkafgxn7q26zxgsuz8tw9k8ur2dfefntz --chain-id joy-testnet-1000` on windows.  

`./joycli query account joystream1hh4egjkafgxn7q26zxgsuz8tw9k8ur2dfefntz --chain-id joy-testnet-1000` on mac.

Windows
-------

### Download and Verify the Binaries

If you haven't already downloaded the correct file, click [here](https://github.com/Joystream/joystream-builder/releases/download/v0.29.0/windows_amd64.zip). Go to your download folder, and extract the file to the destination of your choice. To simplify the instructions, I'm going to extract it to `C:\Joy\` so the full path to the executable files is `C:\Joy\windows_amd64\`

Now, open your first windows terminal (Command Prompt) and give the following command:

```
> cd C:\Joy\windows_amd64\
```

The command `dir` should reveal four files in the folder, `joyd.exe`,  `joycli.exe`, `config.toml` and `genesis.json`.

Verify the versions (and optionally, the checksums):

```
#Versions
> joyd version
0.29.0-30-g1dbaa640-joystream
> joycli version
0.29.0-30-g1dbaa640-joystream

#Checksums
> Certutil -hashfile joyd.exe sha256
128ed575a748ce30bf814a3d26ac890569c43717ac67450fc2fbe096004521d0
> Certutil -hashfile joycli.exe sha256
e2e4f5689f38f0aafc2cad49f11f54b7afc11ce1047693971b9cf04e5902f59c
```

If you get different outputs, go to [github](https://github.com/Joystream/joystream-builder/releases) and make sure you have downloaded the correct binaries.

### Setup Your Account and Start the Node

First, make the following command:

```
> mkdir C:\.joyd\config

#Assuming you unpacked the .zip file to C:\Joy:
> copy config.toml C:\.joyd\config
> copy genesis.json C:\.joyd\config
```

For the next part, you don't need the terminal, but leave it open. Open Explorer, and navigate to `C:\.joyd\config`. Open `config.toml`with a text editor, and replace `node0` with your preferred moniker on line 7.

Go back to the terminal window, and fire up your node:

```
> joyd start
```

This will start the network, and sync your node. When the rate of new blocks has slowed to once every 5 seconds, it means you are fully synced. You are now running a full node!\
If you want to leave your node running, don't close the terminal, as this will kill the process.

### Get JOY Tokens from the Faucet

To get some tokens, you first need to find your address. Without closing the old one, open a new terminal (terminal 2). To generate an account with a set of keys:

```
> cd C:\Joy\windows_amd64\
> joycli keys add 'your_account_name'
```

After you have successfully typed and repeated your 8+ character passphrase, the output will be an address, public key and 24 word [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) compatible seed (derivation path: 44'/118'/0'/0/0). If you want to continue using your account, or keeping it for future testnets, write down your seed on a piece of paper.

Now, copy your address to the clipboard, and head over to our [faucet](https://faucet.joystream.org/). Paste it in, solve the captcha, and hit `Send me tokens`.

To check your new balance, go back to terminal 2 and type:

```
> joycli query account 'your_address' --chain-id joy-testnet-2000
```

If you see `"joy","amount":"100"` somewhere in the output, you have now received your first JOY tokens! If you get and error message, chances are you are not yet fully synced. If you are impatient, go to the [block explorer](http://explorer.joystream.org/blocks), and you should see your transaction if you scroll down.

### Become a Validator

If you want to earn your share of the block reward, you need to become a validator. In terminal 2:

```
> joyd tendermint show-validator
```

To get your `validator_pub_key`, then create a staking transaction:

```
> joycli tx stake create-validator --amount=100joy --pubkey='validator_pub_key' ^
--moniker='your_moniker' --chain-id=joy-testnet-2000 --from='your_account' ^
--commission-rate="0.10" --commission-max-rate="0.20" --commission-max-change-rate="0.01"
```

The output can be quite confusing, so it's best to check your status in the [block explorer](http://explorer.joystream.org/). If your moniker is be listed as part of the validator set, you have succeeded in becoming a validator!

If you want to bond more stake, either to yourself or someone else:

```
#Check your balance again
> joycli query account 'your_address' --chain-id joy-testnet-2000

#List the validator set
> joycli query stake validators --trust-node=1

#Replace 'amount' and 'operator_address' with your desired amount and destination
> joycli tx stake delegate --amount 'amount'joy --from 'your_account' ^
--chain-id joy-testnet-2000 --validator 'operator_address'
```

If you want to try out some other features, make sure to go [here](https://github.com/Joystream/joystream-manual) after you're up and running!

On Mac
------

### Download and Verify the Binaries

If you haven't already downloaded the correct file, click [here](https://github.com/Joystream/joystream-builder/releases/download/v0.29.0/darwin_amd64.zip), and download `darwin_amd64.zip`.

Go to your download folder, and extract the file to the destination of your choice. Assuming you you unzipped to your download folder, open the terminal, and type the following command:

```
$ cp -R Downloads/darwin_amd64 ~/
$ cd darwin_amd64
```

The `ls` command should list `joyd` and `joycli`.

Verify the versions (and optionally, the checksums):

```
#Version
$ ./joyd version
0.29.0-30-g1dbaa640-joystream
$ ./joycli version
0.29.0-30-g1dbaa640-joystream

#Checksum
$ shasum -a256 joyd
fae662e318be15d8a9e9d2db6e6ce9004ef0e86906ce8a2cf241a9d86e71c9d8  joyd
$ shasum -a256 joycli
6348353f4090a47eaad1057a9bb7cc15657c0312b9fb83c367819786b0168a21  joycli

```

If you get different outputs, go to [github](https://github.com/Joystream/joystream-builder/releases) and make sure you have downloaded the correct binaries.

### Setup Your Account and Start the Node

There are a few different ways of doing this next part, but the easiest is with the following commands:

```
#Create a new directory
$ mkdir -p $HOME/.joyd/config

#Fetch the correct genesis.json file
$ curl https://raw.githubusercontent.com/joystream/joystream-testnets/master/latest/genesis.json\
> $HOME/.joyd/config/genesis.json

#Fetch the correct config.toml file
$ curl https://raw.githubusercontent.com/joystream/joystream-testnets/master/latest/config.toml\
> $HOME/.joyd/config/config.toml
```

Set your moniker:

```
$ nano ~/.joyd/config/config.toml
#Edit the seventh line, by replacing node0 with your preferred moniker.
#Ctrl+x and y to save and exit.
```

Assuming you are still in `~/darwin_amd64`, to fire up node:

```
$ ./joyd start
```

This will start the network, and sync your node. When the rate of new blocks has slowed to once every 2 seconds, it means you are fully synced. You are now running a full node!\
If you want to leave your node running, don't close the terminal, as this will kill the process.

### Get JOY Tokens from the Faucet

To get some tokens, you first need to find your address. Without closing the old one, open a new terminal (terminal 2). To generate an account with a set of keys:

```
$ cd ~/darwin_amd64
$ ./joycli keys add 'your_account'
```

After you have successfully typed and repeated your 8+ character passphrase, the output will be an address, public key and 24 word [BIP39](https://github.com/bitcoin/bips/blob/master/bip-0039.mediawiki) compatible seed (derivation path: 44'/118'/0'/0/0). If you want to continue using your account, or keeping it for future testnets, write down your seed on a piece of paper.

Now, copy your address to the clipboard, and head over to our [faucet](https://faucet.joystream.org/). Paste it in, solve the captcha, and hit `Send me tokens`.

To check your new balance, go back to terminal 2 and type:

```
$ joycli query account 'your_address' --chain-id joy-testnet-2000
```

If you see `"joy","amount":"100"` somewhere in the output, you have now received your first JOY tokens! If you get and error message, chances are you are not yet fully synced. If you are impatient, go to the [block explorer](http://explorer.joystream.org/blocks), and you should see your transaction if you scroll down.

### Become a Validator

If you want to earn your share of the block reward, you need to become a validator. In terminal 2:

```
$ ./joyd tendermint show-validator
```

To get your `validator_pub_key`, then create a staking transaction:

```
$ ./joycli tx stake create-validator --amount=100joy --pubkey='validator_pub_key'\
--moniker='your_moniker' --chain-id=joy-testnet-2000 --from='your_account'\
--commission-rate="0.10" --commission-max-rate="0.20" --commission-max-change-rate="0.01"
```

The output can be quite confusing, so it's best to check your status in the [block explorer](http://explorer.joystream.org/). If your moniker is be listed as part of the validator set, you have succeeded in becoming a validator!

If you want to bond more stake, either to yourself or someone else:

```
#Check your balance again
$ ./joycli query account 'your_address' --chain-id joy-testnet-2000

#List the validator set
$ ./joycli query stake validators --trust-node=1

#Replace 'amount'/'operator_address' with your desired amount/destination
$ ./joycli tx stake delegate --amount 'amount'joy --from 'your_account'\
--chain-id joy-testnet-2000 --validator 'operator_address'
```

If you want to try out some other features, make sure to go [here](https://github.com/Joystream/joystream-manual) after you're up and running!