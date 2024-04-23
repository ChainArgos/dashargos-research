---
description: >-
  This documentation will trace the initial token misallocation issues for
  ETHFI, a popular DeFi project, and helps users discover underlying trading
  signals.
---

# 🔘 ether.fi

## Information from the team

The initial allocation of ETHFI is described both [by the team](https://etherfi.gitbook.io/etherfi/governance/ethfi-allocations) and in a [Binance research piece](https://www.binance.com/en/research/projects/etherfi). The later piece tells us the initial circulating supply should be 115.2mm tokens out of a total of 1b. It also gives the end-state breakdown allocation as:

* 2% Binance Launchpool
* 11% airdrop
* 32.5% investors & advisors
* 23.26% team
* 1% protocol guild
* 27.24% DAO treasury
* 3% liquidity

These would be the total amount handed out over time. The document tells us there are a range of vesting schedules and the like. From these we get an approximate initial allocation, which we know should total 11.52%, of:

* 2% launchpool
* 5.5% airdrop
* 3% liquidity
* 1.02% investors and advisors

The team and guild initial allocations look like 0. While the document does not directly address the DAO treasury initial allocation it is clear the circulating supply should be 11.52%. So, at most, there is a little confusion over how that amount is allocated.

## Finding Candidate Project Wallets

We can start [here](https://dashargos.chainargos.com/dashboards/162?Relative+Months+Prior=%5B0%2C48%5D&Symbol=ETHFI)
with a listing of the largest senders and receivers of the ETHFI token.

The team also documents a [large number of addresses](https://etherfi.gitbook.io/etherfi/contracts-and-integrations/deployed-contracts).
But you'll notice quite a few of the most-active addresses are not on that list.
Several belong to large CeXs like Binance and OKX -- but the most interesting ones do not.

## Initial handouts

We find that [0x7a6a41f353b3002751d94118aa7f4935da39bb53](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x7a6a41f353b3002751d94118aa7f4935da39bb53\&Symbol=) receives the full 1b tokens from null in February. So this is some kind of team-controlled contract. It is a vanilla multisig. Three things to notice here:

1. This address was not disclosed by the team.
2. This address also receives 1.5mm tokens from OKX. this is weird and we will revisit it later.
3. There are myriad outflows in March 2024 we can try to match to the allocations.

The largest recipient from this initial address is [0x5f0e7a424d306e9e310be4f5bb347216e473ae55](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x5f0e7a424d306e9e310be4f5bb347216e473ae55\&Symbol=). This address gets 140mm ETHFI on 13th March 2024. Now notice:

1. This exceeds the initial circulating supply.
2. This doesn't correspond to any given category above.
3. This is another undisclosed generic multisig.

From the 0x5f0 address we see:

1. \~50mm to an address tagged as airdrop-related. This is close to the expected amount. [0x93fff4028927f53f708534397ed349b9cd4e2f9f](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x93fff4028927f53f708534397ed349b9cd4e2f9f\&Symbol=)
2. 20mm to an address which sends on to Binance. This looks like the launchpool amount. [0x80d4e342b211610798aab0f8eb6305fef4c12b9c](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x80d4e342b211610798aab0f8eb6305fef4c12b9c\&Symbol=)
3. \~500k tokens to about a dozen small random addresses. Some kind of team payments? Anyway small.
4. \~70mm tokens left over in this address.

So far so good.

Now if we go back to the 0x7a6 address there are \~27mm tokens sent to another dozen or so addresses. This leaves us with 140mm tokens that left the inital wallet allocated as follows:

1. 20mm to binance launchpool ✅
2. 50mm to airdrop ✅
3. 27.5mm to a few dozen small addresses ✅ (maybe?)
4. 70mm in a team-controlled allocation wallet 🚩

## Status & trading signals

At this point the circulating supply is now either 20+50+27.5=97.5mm or 167.5mm. Neither of those is the stated 115.2mm amount.

This gives at least one excellent trading signal: If the team sends tokens from 0x5f0 to an exchange it is probably a good idea to short the token. Certainly if this activity is not associated with any announcements.

## OKX-related errors

Three addresses that received tokens from the initial wallet sent them on to OKX. These are:

1. [0x07a4883a912f6bbbc13a37798f3ead7623b5f390](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x07a4883a912f6bbbc13a37798f3ead7623b5f390\&Symbol=)
2. [0x662d185062bd15e780e652bc7b5bbd3ebcae6862](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x662d185062bd15e780e652bc7b5bbd3ebcae6862\&Symbol=)
3. [0x243340e228d2fd8a2cfb5f3cf53d4f9ba3acdfa6](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x243340e228d2fd8a2cfb5f3cf53d4f9ba3acdfa6\&Symbol=)

1.5mm tokens were returned to [0x7a6](https://dashargos.chainargos.com/dashboards/57?To+or+From+Address=0x7a6a41f353b3002751d94118aa7f4935da39bb53\&Symbol=). Someone returned them. There is some kind of error here. And probably some co-conspirator(s).
