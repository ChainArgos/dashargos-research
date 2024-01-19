# Uniswap Price Feeds

The idea here is to derive price information from on-chain DeX sources.

[WBTC price and volume](https://dashargos.chainargos.com/looks/274) over time from Uniswap.
This one chart covers several different fee pools and stablecoins.
You get a good overview of WBTC pricing and can check visually if there is much variance by
contra stable or fee.

[Volumes by token and protocol](https://dashargos.chainargos.com/looks/209) gives a larger
overview of the DeX landscape. This includes Uniswap and several forks and all involved tokens.

Those looks compute volume weighted average price (VWAP) a day at a time. We can also run that
hourly or weekly.
But we can get even more clever if needed.
[This shows the rolling 7 day average price](https://dashargos.chainargos.com/looks/281) where
we are averaging 7 consecutive VWAPs. Maybe that is sensible.
Or maybe [we should weight a rolling 7 days of VWAPS by each day's volume](https://dashargos.chainargos.com/looks/282).

This is only limited by user demand and creativity.

Here is a table that shows daily average price for every token that's been through Uniswap.
[There are a lot of columns](https://dashargos.chainargos.com/looks/678).