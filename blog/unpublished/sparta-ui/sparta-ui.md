Sparta - Install the UI on Windows/Mac
======================================

If you want to take things a step further and run the User Interface App locally, this guide will help you along.

### Get the UI App running locally on Windows

This requires quite a lot of steps, and install quite a lot of software. This unlocks no new features or benefits. We have not reviewed these ourselves, and only tested on a VM. **Proceed at your own risk!!**

Instead of showing all the commands, this guide will instead direct the users to various other guides.

Install the scoop package manager by following [this](https://github.com/lukesampson/scoop/wiki/Quick-Start) guide.

Then, install [yarn](https://yarnpkg.com/lang/en/docs/install/#windows-stable) using powershell as when installing scoop:

```
> scoop install yarn
> scoop install node-js
> scoop install nvm
```

Close powershell as prompted, and open it again to install the UI:

```
> scoop install git
> cd C:\
> git clone -b joystream https://github.com/Joystream/apps
> cd apps
> npm config set msvs_version 2015
> yarn
> yarn run start
# Leave the window open under use
```

Open chrome or firefox, and go to <localhost:3000> to run the app. Go to settings, and and change the remote node/endpoint to Local Node (127.0.0.1:9944) to have it point to your own node.

Unlike the node, there is no need to keep this running when you don't want to use the UI app. If you want to open it again after closing, open powershell and:

```
> cd C:\apps
> yarn run start
# Leave the window open under use
```

### Get the UI App running locally on Mac

This unlocks no new features or benefits. If you don't have brew install, go [here](https://brew.sh/).

```
$ brew install node yarn git
```

Clone the repo, and run the app:

```
$ cd
$ git clone -b joystream https://github.com/Joystream/apps
$ cd apps
$ yarn
$ yarn run start
# Leave the window open under use
```

Open chrome or firefox, and go to <localhost:3000> to run the app. Go to settings, and and change the remote node/endpoint to Local Node (127.0.0.1:9944) to have it point to your own node.

Unlike the node, there is no need to keep this running when you don't want to use the UI app. If you want to open it again after closing, open a terminal and:

```
$ cd apps
$ yarn run start
# Leave the window open under use
```

* * * * *

###### Disclaimer

All forward looking statements, estimates and commitments found in this blog post should be understood to be highly uncertain, not binding and for which no guarantees of accuracy or reliability can be provided. To the fullest extent permitted by law, in no event shall Joystream, Jsgenesis or our affiliates, or any of our directors, employees, contractors,  service providers or agents have any liability whatsoever to any person  for any direct or indirect loss, liability, cost, claim, expense or  damage of any kind, whether in contract or in tort, including negligence, or otherwise, arising out of or related to the use of all or  part of this post, or any links to third party websites.