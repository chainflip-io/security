# Known Issues and Deliberate Design Decisions

The following behaviours are known and are either deliberate design decisions or accepted risks. Reports of these issues are not eligible for a reward under the [Bug Bounty Program](./README.md).

This list is not exhaustive. It is updated as positions are given to researchers. If your finding is a variant of one of these entries that leads to a materially different impact, say so explicitly in your report and explain why.

## Boost risk model

Boosted deposits are credited before the deposit is final on the source chain. If the deposit is later orphaned or double-spent, the boost pool takes the loss. This is the documented risk that boosters accept in exchange for boost fees.

## External reorgs beyond safety margins

A transaction that is reorged out of an external chain and only reappears after the deduplication window may be processed again. Safety margins are chosen so that this is very unlikely, and the protocol cannot fully protect against it.

## Keygen and signing offenders

Nodes that fail to respond in a key generation or signing ceremony can be reported as offenders and penalised. The offender set is agreed by State Chain consensus, so it already has supermajority agreement; this is not a path for an individual node to penalise others.

## Withdrawal whitelists and FLIP redemption

Withdrawal whitelists protect an account's earnings. FLIP redemption is governed by the separate redeem-address binding, not the whitelist. Unifying the two may come later.

## Broker bound withdrawal address

The bound withdrawal address applies to Ethereum withdrawals only, because broker fees are earned in USDC.

## Broker and LP API exposure

The Broker API and LP API are run by the broker or liquidity provider themselves. Securing their network exposure (firewall, reverse proxy, authentication) is the operator's responsibility, not a protocol vulnerability.

## KeyManager

In the Ethereum KeyManager contract, zero-address keys and the genesis governor key rotation are deliberate.

## Lending

The utilisation cap is a soft limit. Interest is charged from the instantaneous utilisation reading, which includes the effect of supplying funds shortly before a charge.

## Protocol fee swaps

Swaps of protocol fees have no price protection today. Oracle-based protection is planned.

## Pre-swap price checks

Just-in-time order books mean that the price available at execution can differ from any price observed beforehand. Pre-swap price checks are therefore unreliable by design, and this is not a vulnerability.
