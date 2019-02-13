# Turnstile Migration

---

!!! info "This is not an official implementation of the turnstile"
    `zcashd` has yet to implement support for the Sapling turnstile. There is an official proposal which has yet to be implemented into `zcashd`. You can follow progress of development [here](https://github.com/zcash/zips/pull/197) and the zec-qt-wallet is an individual implementation. If you are concerned then wait until the official RPC tool is released.


## Turnstile Migration overview

[The Sapling turnstile](https://zcash.readthedocs.io/en/latest/rtd_pages/sapling_turnstile.html) is an auditing mechanism for the number of ZEC in circulation. The Sapling turnstile provides accounting for the ZEC held in Sprout shielded addresses as they are migrated to Sapling shielded addresses. To achieve this, owners of shielded ZEC are required to send their balances to a transparent address before sending to Sapling shielded addresses.

If you simply send the funds from a Sprout address to a transparent address to a Sapling address it would be relitavely trivial to link the balances.

The [zcash docs] detail the best practises for handling this turnstile migration. zec-qt-wallet includes a tool to make this simple to migrate your shielded coins from the Sprout to Sapling sheilded pool. It is recommended that all users perform this migration.

zec-qt-wallet can migrate your Sprout funds to a Sapling address in a privacy preserving manner folling the [privacy recommendations] by:

* Creating new transparent addresses in your wallet to move from Sprout to the transparent addressess
* Splits the funds across multiple transaparent addresses over multiple blocks
* Uses rouund numbers to obscure any identifying information as these round number values e.g. 10 will be very common in the blockchain

## Using the turnstile tool

!!! tip "You do not need to keep the wallet open during the migration"
    If you shut down the wallet then it'll send on reopening. You *will* need the wallet to be open in order for any transactions to be sent.

Steps...

You may only perform one migration at a time using the app.