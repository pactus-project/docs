---
title: Fee
weight: 2
math: true
---

Transaction fees in the Pactus blockchain are calculated using a percentage-based fee model.
The fee is a percentage of the transferred amount, within a minimum and maximum range.
The percentage, minimum fee, and maximum fee parameters are part of the blockchain
[consensus parameters](/concepts/consensus/parameters/).

The formula to calculate the transaction fee is as follows:

$$
\begin{align*}
fee = amount \times percentage \newline
\newline
fee =
\begin{cases}
 & fee_{min} & \textbf{ if } \ fee < fee_{min} \newline
  & \newline
 & fee_{max} & \textbf{ if } \ fee > fee_{max} \newline
 & \newline
 & fee & \textbf{otherwise}
 \end{cases}
\end{align*}
$$

## Examples

Currently, the fee fraction or percentage is set to 0.01%, the minimum fee is set to 0.000,001 coin,
and the maximum fee is set to 0.001 coin.

- If Alice wants to transfer 2 coins to Bob, she needs to pay 0.000,2 coins as transaction fee.
- If Alice wants to transfer 0.000,2 coins to Bob, she needs to pay 0.000,001 coins as transaction fee.
- If Alice wants to transfer 20 coins to Bob, she needs to pay 0.001 coins as transaction fee.
