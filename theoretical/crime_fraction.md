# What Fraction Of Flows Is Crime?

Motivated by [this tweet](https://x.com/davidzmorris/status/1785296620289958024).

The question, in primary school terms, is: pick some subset of n transactions from the whole
world of transactions. x is the % of those transaction that are laundering the proceeds of crime.
If y is the pct of GDP that is laundered each year do we expect x = y, x > y or y < x?

That statement, perhaps involving colored balls or pieces of fruit instead of transactions,
should be familiar to just about everyone.

We will use a little math here.
But you do not need to understand the math to understand the results at the bottom -- 
you just need to know these are standard statistical methods.

## Setup

We need a few variables to tackle this:
- G : GDP
- l : The fraction of GDP laundered. L = lG
- T : The financial transactions. |T| = FG where F is "financialization"
- M : The subset of T which are the laundering transactions
- C : The "complexity" of laundering. |M| = CL

This allows us to state the question more precisely.
Pick a subset of n transactions from T. Call it X.
Let m be the number of laundering transactions in X.
Under what conditions is $$\frac{m}{n} > l$$, $$\frac{m}{n} = l$$ and $$\frac{m}{n} < l$$?

## Solution

Assume n is a lot smaller than |T|.
We are taking a "small" sample.
Then we can treat this as a simple binomial problem.*

If p is the probability a transaction is laundering (l),
we pick n transactions and we want to know if at least k are laundering
the answer is:
$$1 - \sum_{i=0}^{\lfloor k \rfloor} {n \choose i} p^i (1-p)^{n-i}$$

This is just the [Binomial Distribution CDF](https://en.wikipedia.org/wiki/Binomial_distribution).

In our units:
- n = |X|
- k = ln
- p = $$\frac{|M|}{|T|} = \frac{lCG}{FG} = l\frac{C}{F}$$

Substituting gives us:
$$1 - \sum_{i=0}^{\lfloor l n \rfloor} {n \choose i} (l \frac{C}{F})^i (1-(l \frac{C}{F}))^{n-i}$$

## Analysis

Our formula depends highly on $$\frac{C}{F}$$: the ratio of how many transactions are needed to launder
1 unit of stolen GDP to the number of transactions required to generate 1 unit of GDP.

The denominator we can get a sense for easily.
Fedwire -- the US Fed's interbank payment system -- does about [$1 quadrillion](https://www.frbservices.org/resources/financial-services/wires/volume-value-stats/monthly-stats.html)
per year in volume
vs [$20T in US GDP and $100T world GDP](https://en.wikipedia.org/wiki/List_of_countries_by_GDP_(nominal)).
Additionally the US [bond](https://www.sifma.org/resources/research/us-treasury-securities-statistics/)
and [equity](https://www.nasdaqtrader.com/trader.aspx?id=FullVolumeSummary) markets do 5x-10x US GDP per year.
Global FX markets do something like [15x-20x](https://www.bis.org/publ/qtrpdf/r_qt2212f.htm) world GDP per year.
The Eurozone's Target2 system does [5x](https://www.ecb.europa.eu/paym/target/target2/facts/html/index.en.html) world GDP.
Recall almost every country has bond and equity markets and an interbank payment system; we are not
trying to be exhaustive here.
So F is at least the sum of all these ratios.
Let's assume it is somewhere 20-100.

But C. How do we estimate C?
One argument is that C should be near 1 as criminals do not like to get caught. Hence they try to
minimize the number of transactions they undertake.
Note as an aside that legal paperwork to create shell companies doesn't create financial transactions --
it creates legal ones which we are not counting here.

It is hard to estimate C because, well, it is measuring the average complexity of financial
crimes.

So lets try this out for a range of values of C and F. F runs across the top. C runs top-to-bottom.
The values are the probability a randomly chosen set of N transactions is at least
$$l$$% laundering.


N = 100

|C \ F|10|25|50|75|100|
|---|---|---|---|---|---|
|1.0|0.00%|0.00%|0.00%|0.00%|0.00%|
|2.5|0.17%|0.00%|0.00%|0.00%|0.00%|
|5.0|3.99%|0.05%|0.00%|0.00%|0.00%|
|7.5|17.36%|0.41%|0.01%|0.00%|0.00%|
|10|38.40%|1.55%|0.05%|0.01%|0.00%|
|15|76.92%|8.08%|0.41%|0.05%|0.01%|

N = 1000

|C \ F|10|25|50|75|100|
|---|---|---|---|---|---|
|1.0|0.00%|0.00%|0.00%|0.00%|0.00%|
|2.5|0.00%|0.00%|0.00%|0.00%|0.00%|
|5.0|0.00%|0.00%|0.00%|0.00%|0.00%|
|7.5|1.86%|0.00%|0.00%|0.00%|0.00%|
|10|46.25%|0.00%|0.00%|0.00%|0.00%|
|15|99.90%|0.02%|0.00%|0.00%|0.00%|

N = 10000

|C \ F|10|25|50|75|100|
|---|---|---|---|---|---|
|1.0|0.00%|0.00%|0.00%|0.00%|0.00%|
|2.5|0.00%|0.00%|0.00%|0.00%|0.00%|
|5.0|0.00%|0.00%|0.00%|0.00%|0.00%|
|7.5|0.00%|0.00%|0.00%|0.00%|0.00%|
|10|48.81%|0.00%|0.00%|0.00%|0.00%|
|15|100.00%|0.00%|0.00%|0.00%|0.00%|

N = 100000

|C \ F|10|25|50|75|100|
|---|---|---|---|---|---|
|1.0|0.00%|0.00%|0.00%|0.00%|0.00%|
|2.5|0.00%|0.00%|0.00%|0.00%|0.00%|
|5.0|0.00%|0.00%|0.00%|0.00%|0.00%|
|7.5|0.00%|0.00%|0.00%|0.00%|0.00%|
|10|49.62%|0.00%|0.00%|0.00%|0.00%|
|15|100.00%|0.00%|0.00%|0.00%|0.00%|

What we see is that, so long as $$F > C$$ there is essentially no chance a random sample ever comes up
with $$l$$.

When N is small those non-zero numbers are [noise](https://en.wikipedia.org/wiki/Noise_(signal_processing)).
If we only pick 3 transactions it's a bit of a coin toss whether we get 0 or 33% laundering.
We are not capable of getting 5% with only 3 samples.

## Notes

(*) Strictly speaking we are not sampling with replacement here.
But given we are taking samples from "all the transactions in the economy" this approximation is reasonable.
