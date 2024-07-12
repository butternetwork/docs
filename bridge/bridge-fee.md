# How is the bridge fee calculated?

Users are able to roughly estimate the cost of a transaction depending on the formulae given below as reference.

The Bridge Fee consists of two components.

1. The first part is omnichain service to deliver message . This portion is determined by the fluctuations in the market gas price and gasLimit want to use for execute on the destination chain .
2. The second part is levied to provide rewards to both the  liquidity providers and the Protocol.

   this part will be calculated based on the amount and a predetermined percentage factor.

   $$
   fee = amount * rate
   $$

   There are lower bound and upper bound in the Fee.

   $$
   min\left\{
   \begin{aligned}
   &minimum \\
   &amount * rate \\
   &maximum
   \end{aligned}
   \right.
   $$

   If the trading volume multiplied by rate is less than the minimum, then this part fee will still charge the minimum as a basic commission.

   If the trading volume multiplied by rate is more than the maximum, then this part fee will only charge the maximum as a basic commission.
