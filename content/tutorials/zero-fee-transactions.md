---
title: Send Zero-Fee Transactions
weight: 13
---

## Preface

Pactus supports zero-fee transactions starting from
[Version 1.6.0 (Mumbai)](https://pactus.org/2024/11/14/pactus-1.6.0-mumbai-released/).
However, for security reasons, there are restrictions on zero-fee transactions:

- Each address can send approximately two zero-fee transactions daily.
- Zero-fee transactions have longer confirmation times.

## How Does It Work?

Zero-fee transactions are based on the consumption-based fee model
detailed in [PIP-31](https://pips.pactus.org/PIPs/pip-31).

According to the Consumptional Fee model, each address has a daily limit for sending zero-fee transactions.
This limit is measured in bytes and decreases whenever a transaction from the address
is broadcast to the network or confirmed in a block.
By default, each address is allowed 360 bytes of zero-fee transactions daily.

It is important to note that the fee configuration in Pactus is not deterministic.
Each validator sets its own preferences for accepting transactions, which means:

1. A validator first checks whether the transaction's fee meets its minimum requirements.
2. If the fee is sufficient, the transaction is added to the transaction pool and
   processed when a validator proposes a new block.
3. If the fee is below the threshold, the validator ignores it but
   broadcasts the transaction to other validators, who may or may not accept it.

This approach makes it impossible to guarantee that a transaction will be accepted by the network.
Users can monitor their transactions on the [Fee Tracker](https://pacviewer.com/fee) page in PacViewer.
This page displays unconfirmed transactions in the pool and
allows users to check whether their transaction is confirmed or not.

Please note that every transaction in Pactus has a lifetime of one day.
If a transaction is not included in a block within one day, it will be invalidated.

## How to Send Zero-Fee Transactions?

By default, the transaction fee is set to `0.01` PAC. To send a zero-fee transaction:

- **In the GUI**: Set the fee to `0` PAC.
- **In the Command Line**: Use the `--fee 0` option.

## How to Accept Zero-Fee Transactions?

By default, the consumptional fee is disabled in the
[configuration file](https://github.com/pactus-project/pactus/blob/main/config/example_config.toml).
If your validator node has sufficient resources,
you can update the configuration to accept and process zero-fee transactions:

1. Increase the transaction pool size to accommodate more transactions.
2. Set `fixed_fee` to `0` to accept transactions with zero fee.
3. Adjust the `daily_limit` and `unit_price` as needed. The recommended settings are:
   - `daily_limit`: 360 bytes
   - `unit_price`: 0.000005 PAC per byte

Here is an example configuration for accepting zero-fee transactions:

```toml
# `tx_pool` contains configuration options for the transaction pool module.
[tx_pool]

  # `max_size` indicates the maximum number of unconfirmed transactions inside the pool.
  # Default is `1000`.
  max_size = 2000

  # `tx_pool.fee` contains configuration to calculate the transaction fee.
  [tx_pool.fee]

    # The `fixed_fee` is a constant fee in PAC that applies to each transaction, regardless of its size or type.
    # Default is `0.01` PAC.
    fixed_fee = 0.00

    # The `daily_limit` is the number of bytes an account can send each day without paying a fee.
    # The `daily_limit` is part of the consumptional fee model.
    # To understand how the consumptional fee model works, you can refer to
    # PIP-31: Consumptional Fee Mode (https://pips.pactus.org/PIPs/pip-31)
    # Default is `360` bytes.
    daily_limit = 360

    # The `unit_price` defines the fee per byte in PAC.
    # The `unit_price` is part of the consumptional fee model.
    # If it is zero, the consumptional fee will be ignored.
    # To understand how the consumptional fee model works, you can refer to
    # PIP-31: Consumptional Fee Mode (https://pips.pactus.org/PIPs/pip-31)
    # Default is `0.0` PAC.
    unit_price = 0.000005

```

After updating the configuration, restart your node to enable the consumptional fee model.
