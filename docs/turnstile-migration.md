# Turnstile Migration

---

!!! info "This is not an official implementation of the turnstile"
    `zcashd` has yet to implement support for the Sapling turnstile. There is a proposal in the form of a ZIP which has yet to be implemented into `zcashd`. You can follow progress of development [here](https://github.com/zcash/zips/pull/197) and the zec-qt-wallet is an individual implementation following the [suggested privacy recommendations](https://zcash.readthedocs.io/en/latest/rtd_pages/sapling_turnstile.html#privacy-recommendations). If you are concerned, then wait until the official RPC tool is released into `zcashd` before migrating funds.


## Turnstile Migration overview

[The Sapling turnstile](https://zcash.readthedocs.io/en/latest/rtd_pages/sapling_turnstile.html) is an auditing mechanism for the number of ZEC in circulation. The Sapling turnstile provides accounting for the ZEC held in Sprout shielded addresses as they are migrated to Sapling shielded addresses. To achieve this, owners of shielded ZEC are required to send their balances to a transparent address before sending to Sapling shielded addresses.

If you simply send the funds from a Sprout address to a transparent address to a Sapling address it would be relitavely trivial to link the balances. The [zcash docs] detail the best practises for handling this turnstile migration. zec-qt-wallet includes a tool to make this simple to migrate your shielded coins from the Sprout to Sapling sheilded pool. It is recommended that all users perform this migration.

zec-qt-wallet can migrate your Sprout funds to a Sapling address in a privacy preserving manner following the [privacy recommendations](https://zcash.readthedocs.io/en/latest/rtd_pages/sapling_turnstile.html#privacy-recommendations) by:

* Creating new transparent addresses in your wallet to move from Sprout to the transparent addressess
* Splits the funds across multiple transaparent addresses over multiple blocks
* Uses rouund numbers to obscure any identifying information as these round number values e.g. 10 will be very common in the blockchain

## Using the turnstile tool

![Turnstile migration](/images/turnstile-start.png)

To start the turnstile migration tool, simply open it by choosing **Apps->Sapling Turnstile** and choose the Sprout address (zc) to migrate funds from and the Sapling address (zs) to send funds too in addition to the number of days you would like to migrate the funds over.

Generally, increasing the migrate over is the best solution but note that there will be an increase in the number of transactions all of which require a fee. The migrate over 4 days (2304 blocks) requires 10 transactions resulting in fees of 0.001 ZEC for the migration.

!!! tip "You do not need to keep the wallet open during the migration"
    If you shut down the wallet then it'll send on reopening. You *will* need the wallet to be open in order for any transactions to be sent so you should open it frequently.

Note that you may only perform one migration at a time using the app.

To check on the progress of the turnstile at any time simply visit **Apps->Sapling Turnstile** and you will be presented with the migration progress and how many transactions until the next block.

!!! danger "Backup your wallet.dat file after starting the migration"
    zec-qt-wallet creates new transparent addresses for the turnstile. You must create a backup once the turnstile migration has started to ensure you have the private keys for these intermediate addresses in case there is an issue. To do so simply visit **File->Backup wallet.dat**.

![Turnstile progress](/images/turnstile-progress.png)

### Aborting the turnstil migration

If at any time you wish to abort the migration simply visit **Apps->Sapling Turnstile** and choose **Abort** and no further transactions will take place (confirm this).