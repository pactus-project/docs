---
title: How to Enable Consumptional Fee?
weight: 10
---

## Preface

The blockchain ecosystem is continuously evolving, with new models and protocols emerging to address specific needs
and challenges. One of these is [PIP-31](https://pips.pactus.org/PIPs/pip-31), the "Consumptional Fee Model," a
unique approach to transaction fees within the Pactus blockchain network.
Traditional fee models often impose fixed charges, potentially excluding lower-priority or low-fee transactions from
timely processing. This can create barriers for users who prefer economical transactions over speed, particularly
within decentralized environments where inclusion is a priority.

This tutorial explores the foundation of the Consumptional Fee Model, designed to provide a balanced and flexible 
fee structure based on data consumption. This model allows users to benefit from a zero or low-fee option, albeit 
with trade-offs in transaction confirmation speed. 
The approach aims to incentivize efficient data usage while giving validators the flexibility to configure fees
dynamically based on network demands and user transaction patterns.

## Configuring the Consumptional Fee

By default, the consumptional fee is disabled in the [configuration](https://github.com/pactus-project/pactus/blob/main/config/example_config.toml).

{{< githubcode
   link="https://github.com/pactus-project/pactus/blob/main/config/example_config.toml"
   startLine="123"
   endLine="142"
>}}

When the consumptional fee model is enabled, each signer can have 1–2 zero-fee transactions per day.
This configuration is recommended for enabling the consumptional fee, though you can adjust
`daily_limit` and `unit_price` as needed.

- `daily_limit` = the maximum allowable data consumption per day (in bytes)
- `unit_price` = the fee per byte of data

```toml
  [tx_pool.fee]
    fixed_fee = 0.0
    daily_limit = 360
    unit_price = 0.000005
```

After updating your node configuration, you will need to restart your node to enable the consumptional fee.
