The Sparta Incentives Structure
===============================

As we announced in our [previous post](https://blog.joystream.org/pay-for-play/), we will pay users in real money (monero) to participate on our testnets.

![](https://blog.joystream.org/content/images/2019/02/10-11.svg)

![](https://blog.joystream.org/content/images/2019/02/20-19.svg)

![](https://blog.joystream.org/content/images/2019/02/100-11.svg)

Who, Why and What?
------------------

For Sparta, anyone **who** wants to can participate and wee assume this will be the case for future testnets as well. Community members may be given some extra incentives or assistance from time to time though.

The **why** was discussed in detail in our previous post. TL;DR:\
We are paying to prepare active participants for an autonomous platform, and test the incentive structure with "real money".

**What** you can do to qualify for getting paid on Sparta is described below.

To get the actual payout, you need to prove your monero address by putting your XMR address in the `My memo` tab under `My Accounts` sidebar. (Note that this feature this not work with zero balance, and currently not when you are staking to be/are a Validator.)

```
# Format:
"4or8YourXmrAddressInDoubleQuotesAndNothingElse"
```

### Validators

![](https://blog.joystream.org/content/images/2019/02/Block_carving-5.svg)

**Compete for $20 per week**

In proof of stake systems, block producers, or Validators, are typically paid a fixed amount for each block produced. For Sparta, we intend to reward the validator group (excluding the Jsgenesis team) with **$20 per week**. Assuming 3/4 of blocks are produced by our community members:

```
blocktime = 6
weekly_reward = 2000
seconds_in_week = 60*60*24*7
community_blocks = 3/4

blockreward = (weekly_reward * blocktime)/(seconds_in_week * community_blocks)
print(blockreward)

----

0.02645503
```

The number - 0.026 cents per block - seems a bit underwhelming, but validation requires little effort for the user after setup.

Council Member
--------------

![](https://blog.joystream.org/content/images/2019/02/Council.svg)

**Earn $10 per Election Cycle**

Council Members are elected by the stakeholders in the system to act in the interest of their constituency. Somewhat simplified, the council will allocate the platforms resources, and hire executive personnel to run the day to day.

We are looking at how to best incentivize them to act in the platforms long term interest. For Sparta, we will pay them both for getting elected, and give out a bonus on two conditions:

-   Vote on `>2/3` of proposals made
-   Vote `yes` on the [runtime upgrade](https://substrate.readme.io/docs/substrate-runtime-recipes)

You will receive $5 to get elected, and an extra $5 if you qualify for the bonus. During the `Announcement` and `Voting` stage, you should include some information about why you should get elected in your `memo` field. If you do get elected, make sure to change the `memo` field to your monero address in order to get your reward.

#### Bug Reporter

![](https://blog.joystream.org/content/images/2019/02/Bug_report.svg)

**Earn up to $20 for reporting, and $100 for fixing bugs.**

Unlike the Validators and Council Members, the bug bounty payments will be somewhat subjective. Long term, such decisions will be resolved by the platform, so in future testnets these payouts will at least partially be made by the Council.

To report an `Issue` or make a `Pull request` go to the [node-repo](https://github.com/Joystream/substrate-node-joystream) or the [UI-repo](https://github.com/Joystream/apps/tree/joystream). Based on the *importance and quality* of the issue/PR, the Jsgenesis team will decide on the rewards.

-   For issues, the reward will range up to $20
-   For a PR, the reward can range up to $100

The quality of an issue can be measured from the level of details in general, like how to reproduce, pasted log outputs, etc. In terms of PRs, simply copying new features implemented on substrate will not be rewarded unless the PR includes changes that was required for compatibility on Joystream.

The contributor must include either their Joystream or monero address when submitting the issue/PR. If you choose the former, you must then make sure the add your monero address to the `memo` field of your account.

```
# Format of memo field:
"4or8YourXmrAddressInDoubleQuotesAndNothingElse"
```

* * * * *

###### Disclaimer

All forward looking statements, estimates and commitments found in this blog post should be understood to be highly uncertain, not binding and for which no guarantees of accuracy or reliability can be provided. To the fullest extent permitted by law, in no event shall Joystream, Jsgenesis or our affiliates, or any of our directors, employees, contractors,  service providers or agents have any liability whatsoever to any person  for any direct or indirect loss, liability, cost, claim, expense or  damage of any kind, whether in contract or in tort, including negligence, or otherwise, arising out of or related to the use of all or  part of this post, or any links to third party websites.