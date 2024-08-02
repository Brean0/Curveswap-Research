# Curveswap-Research

As a primer, Curve Finance is a AMM protocol that allows for more efficient swaps on like-asset pairs, compared to traditional AMMs such as uniswap/sushiswap. This is due to the formula Curve uses to determine the swap price.

[<img src="BrianOlympus/Curveswap-Stuff/blob/main/curveswap.png" alt="Alt text" title="Optional title"> ](https://github.com/BrianOlympus/Curveswap-Stuff/blob/main/curveswap.png)


The gist of this formula is that it shifts between a constant sum (X + Y = K) and constant product (X * Y = K) formula as the balance of assets leans more heavily towards one asset. In an ideal world, the constant sum allows for perfect swaps (you put in 10 tokens, you get 10 tokens). However, there is finite liquidity (if you have a position of 10 Token A and 10 Token B, you are at most able to swap 10 tokens), and a high risk that the composition of the pool will never be balanced. The A parameter controls how fast the formula switches from a constant sum to a constant product formula. 

At first glance, it seems that most stablecoin projects should shoot for as high of an A factor as possible, in order to induce stability and enable large trades. However, without a robust peg maintenance system, it can lead to inorganic demand, large pool imbalances, and an inability to return to peg.

In beanstalks case, it does not give assurances of short term price stability, but instead imposes mechanisms to oscillate around a value peg. Those who sold above the value peg can be confident that BEAN will drop at or below the value peg, and will be able to rejoin the bean-economy, and vice versa. 

The A factor, however, can affect this oscillation heavily. With a high A factor, relatively small deviations cause massive pool imbalances. This makes sense for large stable caps such as USDC, DAI or USDT. They have a need to facilitate large sized trades with low slippage. However, for beanstalk, the high A factor creates inefficiencies seen in the convert and field functions.

The convert is a soft peg stability mechanism, **backed by the willingness of the market** to convert. The attractiveness of Converting comes from the price deviations, rather than the DeltaB sum of pools. As a higher A factor minimizes the price deviations as the pool gets imbalanced, it reduces the arbitrage gained from converting.

For the field, your return is denominated in beans given the weather. However, the lower price the farmer purchases bean to sow, the higher actual return is (e.g buying bean at 0.25 at 1000% weather means an effective weather at 4000%). This means with a high A factor, beanstalk would have to compensate with a higher weather, as given a deltaB the price woudl be higher. This could ultimately result in a longer podline and larger podrate. 

TL:DR bigger is not always better, even going from A = 0 to A = 1 is a massive increase in utility. It is important to use the stableswap formula as an additive tool for utility, rather than the main force of stability. Being dependent on Curve's A factor to induce stability hinders growth and pushes the risk towards the tail end.
