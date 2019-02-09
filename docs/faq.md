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

## Transactions

### Can I use funds with zero confirmations?

### Can I use a custom fee?

### Why does my change go a new address?

### How long does a Sapling transaction take?

### Can I have my change automatically shielded to a Sapling address?

### Can I remove shielded transactions sends from persisting in the wallet?

### Will zec-qt wallet remember my outgoing shielded sends?

## zcashd node

### Where is the default data directory on each platform?

```
* Windows: `%HOMEPATH%\AppData\Roaming\Zcash\zcash.conf`
* macOS: `~/Library/Application Support/Zcash/zcash.conf`
* Linux: `~/.zcash/zcash.conf`
```

### Where is `zcash.conf` located?

zcash.conf is located in the [default data directory](#) and will be in this location even if the datadir has been moved to a different location.

### Can I use zec-qt-wallet with a remote node?

### Does zec-qt-wallet work on testnet?

### Does zec-qt-wallet support selective disclosure?

### Does zec-qt-wallet support viewing keys?

`zcashd` doesn’t currently support Sapling viewing keys yet and will be implemented once supported.

## Wallet

### Is the wallet encrypted?

### How do I read a memo?

### Can I use zec-qt-wallet with a hardware wallet?

### Can I import a Sapling HD seed

### Can I remove an address from the wallet?

### Can I export a seed phrase?

### Can I mine with zec-qt-wallet?

## WinZEC

### How do I upgrade from WinZEC?

### Can I import WinZEC address book?