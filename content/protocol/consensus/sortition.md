---
title: Sortition Algorithm
weight: 4
math: true
---

The sortition algorithm is an important part of the Pactus blockchain, responsible for the fair, transparent
and random selection of validators to join the [committee](/protocol/consensus/committee/).
It utilizes a Verifiable Random Function, or VRF for short, to generate a verifiable random number.

The generated random number should be in the range of 0 to the total staked coins.
If validators can prove that their generated number is less than their stake,
they can send the [sortition transaction](/protocol/transaction/sortition/).
Once a sortition transaction is included in a block, the validator will join the committee,
and the oldest validator in the committee will leave it.

## Verifiable Random Function

Verifiable Random Function is a pseudo-random function that the owner of key $s$ can evaluate $v = f_s(x)$ and also provides
$proof_{x}$ efficiently proving that $v$ is correct. We call such a mathematical
object a verifiable pseudo-random function, VRF for brevity [^first].

Pactus uses the BLS signature scheme as the source of VRF.
Since BLS signatures are [unique](/protocol/blockchain/cryptography/#non-malleability),
the hash of a BLS signature can be used to produce a secure and verifiable random number.

The VRF takes three parameters:

1. The secret key of the validator
2. The sortition seed
3. The total stake of the blockchain.

Once the VRF is executed, it produces an index with a proof.
The index is a number between zero and the total staked coins, and the proof allows other validators to verify the correctness
of the generated index.

The pseudocode below demonstrates the evaluation of the VRF for the sortition algorithm:

$$
\begin{align*}
& \textbf{function} \ generateVRF(sk, seed, stake_{total}) \newline
& \qquad pk \gets P_{BLS}(sk) \newline
& \qquad proof \gets S_{BLS}(sk, seed \| pk) \newline
& \qquad rnd \gets H(proof) \newline
& \qquad index \gets \frac{(rnd \times stake_{total})}{2^{256}} \newline
& \qquad \newline
& \qquad \textbf{return} \ index, proof \newline
& \textbf{end function}
\end{align*}
$$

where:

- $sk$ is the secret key of the validator
- $seed$ is the sortition seed
- $stake_{total}$ is the total stake of the blockchain
- $P_{BLS}$ is a cryptographic function that derives the public key from the secret key for the BLS signature
- $S_{BLS}$ is a cryptographic function that signs a message with the secret key for the BLS signature
- $H$ is a cryptographic hash function that generates a number between $0$ to $2 ^{256}$
- $\|$ denotes the concatenation of two values

To verify a sortition proof, both the validator's public key and stake are required:

$$
\begin{align*}
& \textbf{function} \ verifyVRF(pk, seed, proof, stake, stake_{total}) \newline
& \qquad \textbf{if} \ V_{BLS}(pk, seed \| pk, proof) = True \ \textbf{then} \newline
& \qquad \qquad rnd \gets H(proof) \newline
& \qquad \qquad index \gets \frac{(rnd \times stake_{total})}{2^{256}} \newline
& \qquad \newline
& \qquad  \qquad \textbf{return} \ index < stake \newline
& \qquad  \textbf{else} \newline
& \qquad  \qquad \textbf{return} \ False \newline
& \qquad  \textbf{end if} \newline
& \textbf{end function}
\end{align*}
$$

where:

- $V_{BLS}$ is a cryptographic function used to verify a signed message using the BLS signature scheme
- $stake$ is the validator's stake in the blockchain

There is no need to send $index$ alongside $proof$ because the
result should be less than the validator's stake, and the validator's stake is known at each block.

## Sortition Seed

The sortition algorithm relies on a random and publicly verifiable seed that cannot be manipulated by adversaries.
Otherwise, adversaries may select a seed that favors the selection of corrupt users.

To prevent this, the BLS signature scheme is used to generate the sortition seed.
Since BLS signatures are unique and deterministic, adversaries cannot generate more than one valid signature per block.
In each block, the block proposer generates a new sortition seed based on the previous seed using the following function:

$$
\begin{align*}
& \textbf{function} \ generateSeed(sk, seed_{prev}) \newline
& \qquad \textbf{return} \ S_{BLS}(sk, H(seed_{prev})) \newline
& \textbf{end function}
\end{align*}
$$

Since the proposer's public key is known, the seed for the next block can be easily verified.
If the seed is invalid, the proposed block will be rejected.
The verification function is as follows:

$$
\begin{align*}
& \textbf{function} \ verifySeed(pk, seed_{prev}, seed) \newline
& \qquad \textbf{return} \ V_{BLS}(pk, H(seed_{prev}), seed) \newline
& \textbf{end function}
\end{align*}
$$

The sortition seed for the genesis block set to 0.

## Sortition Probability

The Sortition probability refers to the expected number of validators that may join the committee in each block,
assuming all validators are actively online and executing the sortition algorithm.

The probability of a validator $i$ being selected depends on their stake relative to the total stake in the system:

$$
p_i=\frac{S_i}{S_t}
$$

where:

- $p_i$ is the probability of validator $i$ being selected
- $S_i$​ is the stake of validator $i$
- $S_t$​ is the total stake of all validators.

Therefore, the expected number of validators joining the committee at each block can be represented as:

$$
P=\sum_{i=1}^{n}{p_i}=\sum_{i=1}^{n}{\frac{S_i}{S_t}}=\frac{S_1+S_2+\ldots+S_n}{S_t}
$$

where $n$ is the total number of validators. We know that $S_t={S_1+S_2+\ldots+S_n}$. Therefore we will have:

$$
P=\frac{S_t}{S_t}=1
$$

Thus, on average, we expect one validator to join the committee at each block.
In practice, the actual number of validators joining the committee in each block
may differ due to the randomness in the sortition algorithm, or the possibility of some validators being offline.

## FAQ

### How is the total staked coin calculated?

The total staked coin in each block is calculated by summing the staked coins of all active validators.
An active validator is a validator that has not yet [unbonded](/protocol/transaction/unbond/).

### How is the oldest validator determined?

The height at which the validator joined the committee is recorded as the "Last Joined Height" field in
the [validator](/protocol/blockchain/validator/) structure.
The validator with the lowest "Last Joined Height" in the committee is considered the oldest.

[^first]: [Verifiable Random Function](https://people.csail.mit.edu/silvio/Selected%20Scientific%20Papers/Pseudo%20Randomness/Verifiable_Random_Functions.pdf)
