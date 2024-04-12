# Part 2: Staking Flow Problems

We [previously covered](https://docs.chainargos.com/documentation/v/research/library/polygon/polygon\_1) how the real Polygon circulating supply does not match the documents. Now let's show the problems are far deeper.

[This deck](https://lookerstudio.google.com/reporting/b64dcdc6-721b-4ba3-bbd2-667926839c28) explores issues with staking.

[Here](https://lookerstudio.google.com/s/jG-0TCkidd0) is an overview of the stated release schedule.

Then we can look at both:

1. [Flows from vesting to the Foundation](https://lookerstudio.google.com/s/lOFlQvZzw\_4)
2. [Flows out of the Foundation](https://lookerstudio.google.com/s/hZrbifZBr6E)

The point here is that none of this looks quite like the official schedule. Probably the vesting outflows are not really the free-float. Probably the Foundation outflows are the real free-float. We don't know because they do not tell us. But neither matches the official schedule well at all.

Ok so we know the flows look a bit wrong. So? Let's make a table of the correct token allocations from the official docs. That give us [these numbers](https://lookerstudio.google.com/s/it7owP5FODo). In particular look at:

1. The launchpad 1.9b allocation that's all at the beginning.
2. Staking, which begins at 400mm and rises linearly to 1.2b.

There are other interesting rows here. But for now those are sufficient to identify some _extremely_ dodgy behavior.

Tokens are released from the vesting contract and in to the Foundation. Token distribution flows out of the Foundation. This separates "mechanical" unlocking in the vesting contract from "practical" unlocking when tokens flow out of the Foundation. As essentially all the tokens flow from the vesting contract to the foundation it is not fair to say "look the allocations are wrong!" based solely on that. We are of course supposed to see where the Foundation sent everything.

Foundation outflows are given [here](https://lookerstudio.google.com/s/t8gzIBcP4TQ). Those numbers look something like the allocation table. They are all similar sizes. Some are nicely round. Some even match the end totals.

## Launchpad

First let's do an easy bit of tagging. The allocation table gives 1.9b to the "Launchpad Sale." Coincidentally the largest outflow from the Foundation is also 1.9b. If we look at that wallet...it's pretty clear this is a Binance Launchpad related. Go check on [etherscan](https://etherscan.io/address/0x2a39f6e325055f6a8b90ee42ad007dcaac56368b#tokentxns). So that's tagged now.

This is all fine. And it is a great example of how you tag wallets (sometimes).

## Staking

Here is where it gets interesting. Recall the Staking allocation was supposed to start at 400mm and run up, linearly, to 1.2b. But if we look at flows from the Foundation to the Staking contract we get [this](https://lookerstudio.google.com/s/uumJrmX9-9I).

That chart is reasonably linear -- we have questions about why it isn't smoother but fair enough. But it runs from 0 to 800mm. 400mm tokens are somewhere else.

Now go back to the Foundation outflows table. Does anybody get 400mm tokens? Yes. A wallet tagged as "Binance 33" on etherscan does. And if we look at inflows of MATIC to that wallet we get [this](https://lookerstudio.google.com/s/m6d81IqoqWw). So the 400mm were sent in April 2019 when this all started, in one shot, with no further flows.

The initial "staking" was a transfer to Binance in April 2019. That chart above with flows to the staking contract begins in June 2020 just after the contract was deployed.

So we need to look a bit deeper to see what's happened here. First let's look at the [outflows from Binance 33](https://lookerstudio.google.com/s/s\_m6a49dWCY). Nothing till late November 2021. Just before the top in Dec 2021.

And then a flurry of outflows starting late Jan 2023. Again just before the top and a long leg down as 200mm tokens were sent out over the next 5 months.

And where did those outflows go? A [0x2f4ee address](https://lookerstudio.google.com/s/pGEUgVjTg44).

And what do we see in that address? [Inflows from this Binance 33 wallet and the Marketing & Ecosystem wallet](https://lookerstudio.google.com/s/kzXQ6Nn5qpw). Where did they go? Binance 1 and Binance 14 (aka the exchange).

If we broaden our view to all outflows from the 0x2f4ee wallet we see huge outflows to Binance. [Just look](../../../polygon/0x2f4Ee65D536c5a2Dd72004778167B30aeCb8719C/). Recall we already know all these outflows go to Binance.

## Price

The spikes in that last chart occur just before several highs which precede sharp moves down. Look at May, Nov and Dec 2021. Or much of early 2023.
