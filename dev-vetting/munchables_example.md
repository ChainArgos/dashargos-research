# Munchables dev case study

The dev in this example is the person who "attacked"
[Munchables](https://www.coindesk.com/consensus-magazine/2024/03/27/the-munchables-hack-is-way-worse-than-it-seems/).
Research in to the hack gives us [3 payment addresses and 2 exchange deposit addresses](https://twitter.com/zachxbt/status/1772843238539325947).
Asking a candidate for the wallet they wish to receive their payment as part of the interview process is reasonable.

At this point we can use [standard DashArgos tools](https://dashargos.chainargos.com/) to find inflows
and outflows for those wallets.
If this is a working dev what we care about are inflows to their wallets across time.
When looking at the dev payment wallets identified above we find inflows that are not from this project from:
- `0x19899A49704c7890febc139b4EFA4dE24D88D425`
- `0xf69201aa19c540b74c170a545fc6d8805e0ee9b1`

This [dashboard](https://dashargos.chainargos.com/dashboards/148?Symbol=USDC%2CUSDT%2CDAI&To+Address=0x19899A49704c7890febc139b4EFA4dE24D88D425%2C0xf69201aa19c540b74c170a545fc6d8805e0ee9b1)
shows us stablecoin inflows to those wallets, by source, by month.
The chart shows what looks like:
- 3.5 months of 6.5k salary to `0xd0f9f536aa6332a6fe3bfb3522d549fbb3a1b0ae`
- 2 months of 1.5k salary to `0x74de5d4fcbf63e00296fd95d33236b9794016631`
- 3ish months of 2.75k-ish salary to `0x28c6c06298d514db089934071355e5743bf21d60`
- 6 weeks or so of 2k salary to `0xdfd5293d8e347dfe59e90efd55b2956a1343963d`

and a number of other inflows that plausibly look like dev income (i.e. semi-regular payments for just a few months
that could be contract work or so).
Remember we know some of these flows are definitely dev salary payments from the starting point.
So these are safe assumptions to make during vetting.
