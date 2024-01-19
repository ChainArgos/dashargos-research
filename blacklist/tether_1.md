# Frozen & Escaped Tether

Related to [this Twitter thread](https://twitter.com/ChainArgos/status/1748171855859773836).

On 18-Jan-2024 Tether unblacklisted 2 addresses, both of which were originally blacklisted
22-Jun-2023:
1. [0x5e60ca67be076e1175022fbbf5c03f5ef85811d5](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x5e60ca67be076e1175022fbbf5c03f5ef85811d5&Symbol=)
2. [0x0f9c5c6da70d7fbe606e9ab2dc08082261407636](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x0f9c5c6da70d7fbe606e9ab2dc08082261407636&Symbol=)

Notice those are not busy addresses.
Each received 1k USDT, both from [0x988e9D68Ac8Ab7BBe0cEeFe9bBDa1a4a000C717D](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x988e9D68Ac8Ab7BBe0cEeFe9bBDa1a4a000C717D&Symbol=).

That address was funded from a single Binance withdrawal for 259k USDT.

There are 3 other destinations for USDT from that address that were *not* frozen:
1. [0x8A5A1Db04b36CFd104d66CFe03beCd45F71DE6E3](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x8A5A1Db04b36CFd104d66CFe03beCd45F71DE6E3&Symbol=)
2. [0x32A9b6037596386A0Af31bD28a67B50A1ecBde53](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x32A9b6037596386A0Af31bD28a67B50A1ecBde53&Symbol=)
3. [0x33a0e565e2327814df1533d4fe67de580117904c](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x33a0e565e2327814df1533d4fe67de580117904c&Symbol=)

Notice that all 3 of those addresses deposit their USDT to [eXch](https://exch.cx/).
And that those deposits comprise all but 2k of the 259k USDT withdrawn from Binance.

So 99% of the USDT were sent to an exchange before the freeze was put in to effect.

To review the timeline was:
- 19-Jun-2023: 259k USDT withdrawn from Binance to `0x988e9D68Ac8Ab7BBe0cEeFe9bBDa1a4a000C717D`
- 20-Jun-2023: Those USDT sent to 5 addresses 
- 20-Jun-2023: 3 of those 5 addresses, containing 99% of the funds, deposited to eXch 
- 22-Jun-2023: Remaining 2 addresses, holding ~1% of the funds, frozen by Tether 
- 18-Jan-2024: Those 2 addresses are unfrozen by Tether
