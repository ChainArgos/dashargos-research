# Tether blacklisted, burned, and then unblacklisted

Tether blacklists and unblacklists wallets.
Tether can also burn blacklisted funds.
Here is an example that shows all of those features.

`0x55Df4Ecd9066C417103F59d3eCc9B309Dedfd131` was blacklisted and unblacklisted.
There are several ways to see this.
1. The information is visible in the [wallet label](https://dashargos.chainargos.com/dashboards/88?Address=%250x55Df4Ecd9066C417103F59d3eCc9B309Dedfd131%25)
2. You can search using the [usual tools](../blacklist/monitoring.md)
3. Building any query using blacklisting-related tags [like some of these](https://docs.chainargos.com/documentation/info/explore/ethereum/to-wallet)

Most likely you are running a report of recently-blacklisted addresses.
Here is a dashboard [for this address](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x55Df4Ecd9066C417103F59d3eCc9B309Dedfd131&Symbol=).
You will notice an outflow to `0x0.000` or `NULL` before the blacklisting was lifted.

We can drill in to this as normal and get the transaction hash:
`0x0da9684a6bc67db25050a7006e35f576a95b01832a0e8f09c2cd25a9651f139b`.

This is not a normal ERC-20 transfer. It comes from a call to `DestroyedBlackFunds`.
You can see this on etherscan [here](https://etherscan.io/tx/0x0da9684a6bc67db25050a7006e35f576a95b01832a0e8f09c2cd25a9651f139b#eventlog).
DashArgos simplifies this for you by showing the flow as a transfer.
Notice the flow does not appear in many other sources -- the balance jumps without a corresponding outflow.

These flows are [fairly common](https://dashargos.chainargos.com/looks/770).

## Unblacklisting

In the case of `0x55Df4Ecd9066C417103F59d3eCc9B309Dedfd131` we see the following chain of events:
1. Blacklisted 2022-10-18
2. $863k of funds burned by Tether 2024-03-08
3. Unblacklisted 2024-03-08

This left a balance of about $390k in the wallet. Not everything was burned.

This sure looks like Tether recovered some of the balance for law enforcement and then let the address
go with the rest.
