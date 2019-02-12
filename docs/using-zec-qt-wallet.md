# Using zec-qt-wallet
---

## Getting started

!!! info "Initial Parameters Download"
    The first time zec-qt-wallet starts it will create a `zcash.conf` file with default configuration values as well as downloading the parameters required for sending and validating transactions. These parameters are currently around 1.7GB in size and only need to be downloaded once.

Now that you have zec-qt-wallet [installed](/installation) it is time to start using the software. 

If you are using the embedded `zcashd` and it is your first time using the software, the system parameters will be downloaded from the internet (~1.7GB) and a `zcash.conf` file created specifying some default configuration values. The blockchain will then begin to sync, which is a time consuming process taking anywhere of the order of 8 hours to days depending on your hardware and network performance. You can monitor the progress in the bottom right corner wof zec-qt-wallet which displays the number of blocks downloaded and a sync percentage.

!!! note "Initial Sync"
    The blockchain is around **21GB** in size and will take around 8+ hours to download. Monitor the progress via the sync progress in the bottom right corner of zec-qt-wallet.

## Generating a new address

Visting the **Receive** tab of zec-qt-wallet will show all current addresses and enable you to generate new ones. To learn about the different types of addresses available which are transparent, shielded (Sprout and Sapling) please visit [this page](https://zcash.readthedocs.io/en/latest/rtd_pages/addresses.html). It is not possible to remove an address from the wallet once it has been generated.

!!! tip "Backup after generating a new address"
    Whenever a new address is generated you should ensure that you have a backup of the address. Only Sapling uses a HD wallet and can be [recreated from a seed](#) whereas transaparent or Sprout addresses either require the private key or a wallet.dat backup made after the address was created. See the [Backup section](#) for more details.

![Addresses Tab](/images/addresses.png)    

Transparent addresses are automatically created when clicking the **t-Addr** button as transparent addressess should not be reused. Unlike transparent addresses it is fine to reuse shielded addresses and so new addresses can be manually created via the **New Address** button.

Optionally add a label to easily identify the address and add it to your address book. A QR code is also provided for the address which may be used to receive funds.

## Sending a transaction

Once you've generated an address and have sent some funds to it, you can send some ZEC. Click on the **Send** tab:

![Send Tab](/images/semd.png)

You can only send funds with at least one confirmation. While transactions are being confirmed they are easily identificable as they are highlighted in red.

Choose an address with funds in it and enter the receipient address. You may specifify multiple recipients per transaction and there may be a mixture of transparent and shielded recipients. The Memo field is only available when sending **to** a shielded address (either Sprout or Sapling). The default mining fee is 0.0001 ZEC which is recommended for all transactions. See the Options section if you wish to customise this behviour and understand the implications.

!!! note "Shielded send requirements"
    Sending Sapling transaction requires only around 40Mb of memory and happen in a few seconds. If you still have funds in legacy Sprout addresses sending times are typically around 30 seconds and require 1.3GB of memory.

// TODO send screen    

### Viewing transaction on explorer

Once complete, the txid will be displayed. Right click to bring up a menu to view on the block explorer. Alternitavely for any transactions on the **Transactions** tab right click and choose "View on block explorer".

This will open up the default block explorer of xxxx. If your transaction is a shielded one there will not be any public information available except the mining fee (as in the example transaction above). Once the funds are confirming any values will be highlighted in red until they receive one confirmation and will not be spendable until they have had one confirmation.

### Pay Zcash URI

// TODO

Paste in a Zcash URI.

## Address book

The address book makes managing addresses and labels simple. Either select **Address Book** in the application menu or select the button on the **Send** tab. You can import an address book in csv format?

## Backing up

zec-qt-wallet provides multiple options to ensure your wallet and keys are backed up. It is important that you perform regular backups if you are not exclusively using Sapling addressess. Only Sapling has a HD wallet and once you have the HD seed addressess can be recreated from it.\

!!! warning "It is not yet possible to import a Sapling HD seed"
    While Sapling provides a [HD wallet](#) the feature to import the seed does not yet exist, so while your funds would not be lost in the situation where you have the seed they would be rendered unusable until this feature is added. Therefore it is recommended you keep regular backups of either private keys or the `wallet.dat` file until this feature is implemented. 

### Export a single private key

To export a single private key on the **Balance** tab right click on the address and choose **Get private key** from the context menu. Alternitavely on the **Receive** tab choose the address in question and click the **Export Private Key**. The output of both is the private key which you can copy to a secure storage medium or be used to import into other applications.

### Export all private keys

You can export all private keys for addresses in your wallet by choosing the **Export all private keys** from the File menu. This will provide a list of all private keys.

Note that by default when `zcashd` starts it creates 100 transparent addresses for the keypool for use as change addresses hence this list will always contain at least 100 transparent address keys not all of which have been used. 

### Backing up wallet.dat

You can backup all of your private keys by making a copy of the `wallet.dat` file. To recover you then replace any existing `wallet.dat` file in the [data directory](#). 

!!! danger "Create a new backup after each address"
    As new addresses are generated you will need to create an updated backup else the new keys will not be included.

While this is a convinient method of backing up it means that you are restricted to importing to compatible software with `zcashd` and also if you have many addresses that are unused it will slow the initial import over say importing your addresses with funds.

## Importing private keys

To import a private key, simply choose the **Import private key** from the File main menu. You may paste in multiple keys, one per line that will be imported into the wallet. Note that depending on the number of keys to import and if they are shielded addresses it may take some time for the import to be completed.

## zeq-qt-wallet options

zec-qt wallet has a number of options that allow you to customise how the software works and may be accessed in the **Settings->Options** menu as shown below.

![zec-qt-wallet options](/images/options.png)

### Remember shielded transactions

By default `zcashd` will not store information about your outgoing fully shielded transactions. By default zec-qt-wallet will store outgoing transactions in an local database so that any shielded spends will appear on the transactions tab. If you do not wish these transactions to be stored by zec-qt-wallet simply toggle the option for "Remember shielded transactions". At any point you may clear your shielded transaction history locally (there is no way of recovering this data).

### Allow custom fees

//TODO

### Shield change automatically to Sapling address

//TODO

### Connect via TOR

//TODO

## Encrypted Memo field

//TODO

### Including a reply address

//TODO

### Replying to a memo

//TODO

## Exporting transactions

//TODO

## Apps

//TODO

### Using z-board.net

//TODO

### Turnstile migration

See the [page on the turnstile migration](#turnstile-migration) for full details.

## Customising `zcash.conf`

The `zcash.conf` file may be used to customise how the `zcashd` software behaves. There are a number of [config options available](). when zec-qt-wallet is installed it creates this file with sensible defaults such as connecting to the mainnet and a random password. The location of `zcash.conf` varies by system. By default it is located in the following location on each platform:

* Windows: `%HOMEPATH%\AppData\Roaming\Zcash\zcash.conf`
* macOS: `~/Library/Application Support/Zcash/zcash.conf`
* Linux: `~/.zcash/zcash.conf`

## Connecting to an external `zcashd`

//TODO