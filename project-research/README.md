# 🧪 Project Research

This is an outline of common steps for introductory project research. It begins assuming you know the token you want to look at and have some basic documentation -- possibly with initial allocations or similar -- available. If you do not have any documentation at all that is fine but you're going to need to invent your own labels to get started (i.e. rather than calling something "treasury allocation" it is just going to be "large holder 1").

## Setup

This example looks at Ethereum and Orbler (ORBR) with [this documentation](https://docs.orbler.io/tokenomics/token-allocation).

The first place to check is the [wallet tag data](https://dashargos.chainargos.com/dashboards/159?Categories+=\&Labels=%25orbler%25\&Organizations=) to see what we already have.

## Monthly flows

Start from [this dashboard](https://dashargos.chainargos.com/dashboards/139?Symbol=ORBR) to get monthly on-chain volumes. This will help narrow down the time frame (or frames) to start with.

Now we know the initial period is in February and maybe March 2022.

## Largest senders and receivers

Candidate "important wallet" addresses are easily found [here](https://dashargos.chainargos.com/dashboards/162?Relative+Months+Prior=%5B0%2C48%5D\&Symbol=ORBR). Note that, because we do not know exactly what happened or when it happened, that these are just candidates and we want to aim broadly with the time frame.

## Working out the wallets

From those tables we can see that `0xf8db5580cdcb77119c753f149eb91b815ee006e0` is the issuance wallet. Why?

1. It receives the full 2 billion from null
2. It sends all 2b out and never receives any more.
3. Some amounts match the allocations.

On the last point we are going to split up the outflows later. It is normal to need 2 or 3 layers of wallets to find everything. For example airdrops are often run out of a separate wallet with hundreds or even thousands of small destinations.

The outflows are:

| address                                    | amount         |
| ------------------------------------------ | -------------- |
| 0x58e33934411f8e453b5cb04c498d194d01b3fad8 | 960,000,000.00 |
| 0x78b4964bf6cbc618e340aac960f8bc61c06434ff | 400,000,000.00 |
| 0x8ff19db5b7d712b98026acf692793d47dceece56 | 220,000,000.00 |
| 0xeb926db328044c0cdb8c5fbcf1bd3649d8cd4b57 | 200,000,000.00 |
| 0x6f0df17a5872c14492ff7ce8d305ba0cdd22cb11 | 200,000,000.00 |
| 0xcb7f80a4d3fa609cc3acd2a018547a9e8ec56548 | 20,000,000.00  |

Compare this to a stated allocation of:

| label               | amount |
| ------------------- | ------ |
| marketing           | 20mm   |
| sale                | 300mm  |
| team                | 140mm  |
| partner & advisor   | 20mm   |
| liquidity / staking | 400mm  |
| treasury            | 1120mm |

This means we are going to need to do a little guesswork to figure things out.

### Treasury

`0x58e33934411f8e453b5cb04c498d194d01b3fad8` receives 960mm from the issuance wallet and enough to make up the difference to 1120mm [from two other wallets given above](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x58e33934411f8e453b5cb04c498d194d01b3fad8\&Symbol=ORBR):

| address                                    | amount |
| ------------------------------------------ | ------ |
| 0x78b4964bf6cbc618e340aac960f8bc61c06434ff | 100mm  |
| 0x6f0df17a5872c14492ff7ce8d305ba0cdd22cb11 | 60mm   |

### Sale

Net of the 100mm above this leaves 300mm in `0x78b4964bf6cbc618e340aac960f8bc61c06434ff`. That makes it a good candidate to be the "sale" wallet. And if we [look at that wallet](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x78b4964bf6cbc618e340aac960f8bc61c06434ff\&Symbol=ORBR) this looks correct. The other recipients are not addresses we already know.

This may take a bit more checking to confirm but it is a good candidate.

### Liquidity & staking

[`0x8ff19db5b7d712b98026acf692793d47dceece56`](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x8ff19db5b7d712b98026acf692793d47dceece56\&Symbol=ORBR) receives 220mm from treasury and 180mm from [`0xeb926db328044c0cdb8c5fbcf1bd3649d8cd4b57`](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0xeb926db328044c0cdb8c5fbcf1bd3649d8cd4b57\&Symbol=ORBR). That is 400mm.

It distributes a long tail of 8.33mm chunks, 17.36mm to `0x833b0f56ea206df8ee784fa115c42ecdf00e3f08` and then a lot of 4mm and down amounts.

This looks like the liquidity and staking wallet.

### Partner & advisor

`0xeb926db328044c0cdb8c5fbcf1bd3649d8cd4b57` receives 200mm from treasury. It sends 180mm to `0x8ff19db5b7d712b98026acf692793d47dceece56` and then a lot of 1.11mm and 833k single payments.

That looks like paying related parties but could also be marketing expenses,

### Team

[`0x6f0df17a5872c14492ff7ce8d305ba0cdd22cb11`](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x6f0df17a5872c14492ff7ce8d305ba0cdd22cb11\&Symbol=ORBR) receives 200mm from treasury. It sends 60mm to `0x58e33934411f8e453b5cb04c498d194d01b3fad8` and then another long tail of 7.77mm and other clearly-allocations-amounts.

This looks like the team wallet.

### Marketing

[`0xcb7f80a4d3fa609cc3acd2a018547a9e8ec56548`](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0xcb7f80a4d3fa609cc3acd2a018547a9e8ec56548\&Symbol=ORBR) deposits a bit to exchanges but still has the bulk of the initial 20mm tokens.

This looks like a partially-spent marketing budget. But it is also possible they just did not have as many partners as expected.

### Notes

It is plausible we have the marketing and partner & advisor wallets backwards. That would mean they have incurred a lot of marketing expenses and stiffed (or never had) partners. It does not really matter which happened.

In more complex cases you may need to look downstream from these wallets. Or if it really matters which is marketing and which is the partner wallet we would need to look further. But for the purposes of an intro this is a reasonable place to stop.
