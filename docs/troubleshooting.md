# Troubleshooting

---

## The `zcashd` debug log

The `debug.log` file is the first place to start for troubleshooting issues. The file is located in the data directory and by default is located in the following locations:

* Windows: `%HOMEPATH%\AppData\Roaming\Zcash\debug.log`
* macOS: `~/Library/Application Support/Zcash/debug.log`
* Linux: `~/.zcash/debug.log`

If you have specified a custom `datadir` option then the `debug.log` file will be located in that directory. Using a tool such as `tail` you can view the last 100 lines with the following command:

``` bash
tail -n 100 ~/.zcash/debug.log
```

## My node isn't syncing

If your node isn't syncing or is slow to sync, first check that you have connections to other nodes as you may have a network issue. zec-qt-wallet will display if you are connected via the application footer. 

![zec-qt-wallet connections](/images/connections.png)

You can also find this information in the **zcashd** tab on the main menu (if you are running the embedded `zcashd`) and it will list the number of connections to other peers which should be greater than 0. If you do not have any connections then check your internet connection, then check that the [ports required](/troubleshooting/#zcashd-ports) for `zcashd` are not blocked and that you have not specified a TOR connection in the options but do not have TOR running.

If you are still having issues, then look in the [debug log](/troubleshooting/#the-zcashd-debug-log) to identify any error messages.

## zcashd ports

By default `zcashd` runs on the following ports.

* **8232** for mainnet RPC
* **8233** for mainnet peer-to-peer network
* **18232** for testnet RPC
* **18233** for testnet peer-to-peer network

You may override any of these values in `zcash.conf`.

## My transaction didn't get mined

## How to perform a wallet rescan

## How to perform a reindex

## The displayed balance is incorrect

## `zcashd` has no connections

## Some of my shielded transactions are not displayed in the transaction tab

## I can't generate a new Sprout address

## Sending from a Sprout address to a Sapling one results in error

## Common error messages

### Could not start embedded zcashd

This means zec-qt-wallet couldn't start its embedded zcashd for some reason. zec-qt-wallet will show you another dialog box with the error reported from zcashd for debugging purposes as well. You might be able to solve this by simply restarting zec-qt-wallet, but if you repeatedly see this error, it might be one of the following reasons:

* If you compiled zec-qt-wallet yourself and are running it: zcashd doesn't come with the github repository, so you'll have to compile zcashd separately and copy if over into your zec-qt-wallet directory.
* You might have corrupt zcash params: In this case, you may try deleting your params and letting zec-qt-wallet download them again.

If all else fails, you can run an external zcashd and zec-qt-wallet will connect to it.

### Authentication error

Normally, zec-qt-wallet can pick up the rpcuser/rpcpassword from zcash.conf. If it doesn't for some reason, you can set the username/password in the File->Settings menu. If you are connecting to a remote node, make sure that zcashd on the remote machine is accepting connections from your machine. The target machine's firewall needs to allow connections from your host and also zcashd is set to be configured to accept connections from this host.

### Not enough balance when sending transactions

The most likely cause for this is that you are trying to spend unconfirmed funds. Unlike Bitcoin, the Zcash protocol doesn't let you spent unconfirmed funds yet. Please wait for 1-2 blocks for the funds to confirm and retry the transaction.

## My issue isn't resolved
Open an issue on Github or tweet at [@zecqtwallet](https://twitter.com/zecqtwallet) for help.