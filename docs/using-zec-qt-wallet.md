# Using zec-qt-wallet
---

!!! info 
    The first time zec-qt-wallet starts it will create a `zcash.conf` file with default values as well as downloading the parameters required for sending and validating transactions. 
    These parameters are currently around 1.7GB in size and only need to be downloaded once.

## Getting started

Now that you have zec-qt-wallet [installed](/installation) it is time to start using the software. 

If you are using the embedded `zcashd` and it is your first time using the software, the system parameters will be downloaded from the internet (~1.7GB) and a `zcash.conf` file created specifying some default configuration values. The blockchain will then begin to sync, which is a time consuming process taking anywhere of the order of 8 hours to days depending on your hardware and network performance. You can monitor the progress in the bottom left corner which displays the sync percentage.

!!! note "Initial Sync"
    The blockchain is around xxx GB in size and will take around 8+ hours to download. Monitor the progress via the sync progress in the bottom right corner of zec-qt-wallet.

## Generating a new address

Visting the **Receive** tab will show all current addresses and enable you to generate new ones. To learn about the different types of addresses transparent, shielded (Sprout and Sapling) please visit [this page](https://zcash.readthedocs.io/en/latest/rtd_pages/addresses.html). It is not possible to remove an address from the wallet. Whenever a new address is generated care should be taken to ensure that a backup of the wallet is taken. The QR code may be scanned by a compatible device.

## Sending a transaction

Show fields used to send...

### Viewing transaction on explorer

Once complete, the txid will be displayed. Right click to bring up a menu to view on the block explorer. Alternitavely for any transactions on the **Transactions** tab right click and choose "View on block explorer".

### Pay Zcash URI

How to use

## Address book

## Backing up

### Export a single private key

### Export all private keys

### Backing up wallet.dat

## Importing private keys

## zeq-qt-wallet options

zec-qt wallet has a number of options which may be viewed in the **Settings->Options** menu as shown below.

![zec-qt-wallet options](/images/options.png)

### Remember shielded transactions

By default `zcashd` will not store information about your outgoing fully shielded transactions. By default zec-qt-wallet will store outgoing transactions in an local database so that any shielded spends will appear on the transactions tab. If you do not wish these transactions to be stored by zec-qt-wallet simply toggle the option for "Remember shielded transactions". At any point you may clear your shielded transaction history locally (there is no way of recovering this data).

### Allow custom fees

### Shield change automatically to Sapling address

### Connect via TOR

## Encrypted Memo field

### Including a reply address

### Replying to a memo

## Exporting transactions

## Apps

### Using z-board.net

### Turnstile migration

## Customising `zcash.conf`

## Connecting to an external `zcashd`