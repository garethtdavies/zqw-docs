# FAQ
---

## Installation

### Where do I download the software?

zec-qt-wallet is available to download from the [Zcash Foundation Github repository](https://github.com/ZcashFoundation/zec-qt-wallet). The [releases page](https://github.com/ZcashFoundation/zec-qt-wallet/releases) lists the latest available downloads for each platform.

### Which installer should I download?

See the [installation](/installation/#download-and-install) section for more details for your platform.

### How do I verify the download file?

All releases are signed and may be verified?

## Blockchain

### Is zec-qt-wallet a light client?

No, zec-qt-wallet requires a full `zcashd` node to operate. A light client protocol is currently in development that would substantially reduce the storage and bandwidth requirements for a light wallet and once this development is complete...

### How large is the blockchain?

Currently the blockchain data directory is around 25GB (Feb, 2019) and will continue to grow with time.

### Can I move the data directory?

If you are starting zec-qt-wallet for the first time then you can choose the advanced configuration and select the location of your data directory, which may for example be on a seperate disk. If you have an existing data directory you would like to move, you can achieve this through the following steps:

* Create the new directory
* Copy your [existing data directory](#) to the new location
* Update [zcash.conf](#) with the `datadir=/your/new/path`
* Restart zec-qt-wallet

### Can I move the params directory?

No, unlike the data directory there is no configurable option to specify the params directory and `zcashd` expects the Params directory to be in the following locations:

//TODO check this

* Windows: `%HOMEPATH%\AppData\Roaming\ZcashParams`
* macOS: `~/Library/Application Support/ZcashParams`
* Linux: `~/.zcashparams`

As a workaround you can use any filesystem operations for your OS e.g. creating a sysmlink of the directory but these are unsupported.

## Transactions

### Can I use funds with zero confirmations?

No, Zcash requires that you have at least 1 confirmation before sending. Trying to spend unconfirmed funds will result in an error.

### Can I use a custom fee?

Yes, but here's why you shouldn't...

### Why does my change go to a new address?

Like Bitcoin ...

### How long does a Sapling transaction take?

Sapling greatly reduced the time taken to perform proofs down to just a few seconds. Sprout transactions take around 70-90 seconds and is dependent on hardware and the number of JoinSplits.

### Can I have my change automatically shielded to a Sapling address?

### Can I remove shielded transactions sends from persisting in the wallet?

### Will zec-qt wallet remember my outgoing shielded sends?

Yes, by default zec-qt-wallet will store shielded sends in a local database as `zcashd` does not provide this information. You caan override this behaviour in the [Options](#) setting and can remove any stored transactions at any time (note that these will not be recoverable if you delete them).

## zcashd node

### Where is the default data directory on each platform?

* Windows: `%HOMEPATH%\AppData\Roaming\Zcash\zcash.conf`
* macOS: `~/Library/Application Support/Zcash/zcash.conf`
* Linux: `~/.zcash/zcash.conf`

### Where is `zcash.conf` located?

zcash.conf is located in the [default data directory](#) and will be in this location even if the datadir has been moved to a different location.

### Can I use zec-qt-wallet with a remote node?

Yes, zec-qt-wallet will attempt to connect to 

You should not (see security settings)

### Does zec-qt-wallet work on testnet?

Yes, zec-qt-wallet will work with testnet. To do so you simply add the following lines to your [zcash.conf](#) file, replacing the existing values if present:

```
addnode=testnet.z.cash
testnet=1
```

### Does zec-qt-wallet support selective disclosure?

Not yet. While s[elective disclosure](#) works on Sprout addresses it has not yet been updated in `zcashd` to support Sapling addresses.

### Does zec-qt-wallet support viewing keys?

`zcashd` doesn’t currently support Sapling viewing keys yet and will be implemented once supported.

## Wallet

### Is the wallet encrypted?

No wallet encryption is [currently disabled](#) by `zcashd`. Users are advised to use full disk encyption or to manually encrpyt/decrypt their `wallet.dat` files when not using the software.

### How do I read a memo?

If there is a [memo](#) attached to a transaction then it will be visible by a message icon by the transaction. Simply right click the transaction and choose **View Memo**.

![Memo](/images/memo.png)

### Can I use zec-qt-wallet with a hardware wallet?

No, this is currently not supported.

### Can I remove an address from the wallet?

No, addresses cannot be removed from the wallet. It is advised that you export the private keys for addresses you are interested in and then delete the `wallet.dat` file. You can then import the private keys you require.

### Seed phrases

#### Does zec-qt-wallet have a 12 word seed

#### Where can I find the Sapling HD seed?

#### Can I export a seed phrase?

In zcashd only Sapling addresses are HD compatible. There is a Sapling master seed but this is currently not accessible to the zec-qt-wallet. To get this seed you need to run the following command via the zcashd CLI. `zcash-cli z_exportwallet` having set an export path in your `zcash.conf`. The Sapling seed will be displayed at the top of the file in the format...

#### Can I import a Sapling HD seed

It should be noted that it is currently not possible to _import_ the seed to zcashd but this functionality will be enabled shorty.

### Can I mine with zec-qt-wallet?

No, zec-qt-wallet is a wallet and full node. while you can configure zcashd to run the inbuilt CPU miner this isn't practical to run on mainnet and you need alternative hardware and software to run. See this page for more information on mining.

## WinZEC

### How do I upgrade from WinZEC?

WinZEC has now been deprecated. You can simply install zec-qt-wallet and it'll use the data directory and wallet from WinZEC and all your funds will be available.  

### Can I import WinZEC address book?

Yes, simply brose to the location of the address book file (xxxxxx)