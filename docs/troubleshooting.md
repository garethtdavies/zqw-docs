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

On Windows `%HOMEPATH%` is typically `C:\Users\username` where `username` is your username. 

## My node isn't syncing or is slow to sync

_There's a number of variables that determine syncing speeds because the blocks are being verified in addition to downloaded... memory, CPU and bandwidth. Is the hardware you use to sync other blockchains the same or comparable to the one you're using for zcash?_

If your node isn't syncing or is slow to sync, first check that you are running the latest version of zec-qt-wallet then check that you have connections to other nodes as you may have a network issue. zec-qt-wallet will display if you are connected via the application footer. 

![zec-qt-wallet connections](images/connections.png)

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

If you send a transaction before the node is fully synced, or perhaps due to network congestion then the transaction may fail and be returned to your wallet due to the [Transaction Expiry](https://z.cash/blog/transaction-expiry/) feature. When a user submits a transaction to the network, by default it will persist in the mempool for 20 blocks (currently approximately 50 minutes). If it has not been mined after that period, it is no longer valid and will be evicted from all mempools. The value will return to the sender’s wallet. 

## How to perform a wallet rescan

!!! note "Slow wallet rescan"
    Depending on the number of addresses in your wallet (particualy shielded addresses) a wallet rescan can be slow. Simply leave it running until the process is complete.

If you need to perform a wallet rescan due to missing transactions or balance errors you will need to start `zcashd` with the `--rescan` option. There are a couple of methods to achieve this and this process will be improved in future versions of the zec-qt-wallet.

### Via an external `zcashd`

If you are running the embedded `zcashd` you will need to run `zcashd` externally to run the rescan and once complete you can safely close and run zec-qt-wallet as normal. With zec-qt-wallet closed open a terminal/command prompt and run the following command depending on your platform (and adjust accordingly to match your system if required). Then open zec-qt-wallet and it should connect to the running `zcashd` and you can monitor the progress of the rescan on the startup screen.

Windows: `cmd /C ""C:\Program Files (x86)\zec-qt-wallet\zcashd.exe" -rescan"` if using the installer or `zcashd.exe -rescan` from the directory of the downloaded binaries
macOS: `/Applications/zec-qt-wallet.app/Contents/MacOS/zcashd -rescan`
Linux: `zcashd -daemon -rescan` if using .deb or `./zcashd -rescan` from the directory of the downloaded binaries

Note that the command above will open zcashd in the foreground, you can change this behaviour by adding the `-daemon` option. You will need to manually stop `zcashd`. You can either force quit with Ctrl-C or restarting your machine as zec-qt-wallet will not close an externally running node.

Note that zec-qt-wallet will no longer stop `zcashd` when running externally and it will run until stopped. The simplest method is to run the `zcash-cli` stop command.

Windows: `cmd /C ""C:\Program Files (x86)\zec-qt-wallet\zcash-cli.exe" stop"` if using the installer or `zcash-cli.exe stop` from the directory of the downloaded binaries
macOS: `/Applications/zec-qt-wallet.app/Contents/MacOS/zcash-cli stop`
Linux: `zcash-cli stop` if using .deb or `./zcash-cli stop` from the directory of the downloaded binaries

### Editing `zcash.conf`

Alternitavely you could edit the `zcash.conf` file and add the line `rescan=1` and then start and stop zec-qt-wallet normally. After you have opened zec-qt-wallet and the rescan is complete you may remove the line from `zcash.conf`. You do not want this line to persist otherwise it will perform a rescan everytime the wallet starts.

## How to perform a reindex

A reindex is sometimes required when the blockchain data becomes corrupted or you wish to enable certain options. When a reindex happens the full blockchain is redownloaded (~22GB) so it will take some time to complete and should only be performed where absolutely necessary.

To complete a reindex simply [follow the instruction for a wallet rescan] replacing `-rescan` with `-reindex`.

``` bash
zcashd -reindex
```

## The displayed balance is incorrect

If your balance is not being correctly displayed, first ensure that your software is up to date and that your node is fully synced. If your balance is still incorrect you can perform a manual [wallet rescan](/troubleshooting/#how-to-perform-a-wallet-rescan) which will rescan the blockchain for missing wallet transactions on startup. Depending on the number of (shielded) addresses in the wallet, this can be _very_ slow so just leave it running until complete andd your balance should be reflected accurately.

## `zcashd` has no connections

See the section on [syncing issues](/troubleshooting/#my-node-isnt-syncing) for common resolutions to this issue.

## Some of my shielded transactions are not displayed in the transaction tab

By default `zcashd` does not store outgoing shielded transactions. To overcome this zec-qt-wallet will store shielded sends locally and this option may be disabled and any transactions cleared. If you are missing any outgoing shielded transactions check that the option to **Remember shielded transactions** is selected in the [wallet options](#). There is no way (currently) of recoving the information about outgoping fully shielded spends if this option is disabled.

## I can't generate a new Sprout address

// TODO Status of Sprout addresses

The use of Sapling addresses is discouraged and Sapling addresses should be used wherever possible. To speed up this process zec-qt-wallet disallows generating new Sprout addressess. If you have a need to do this you can do so simply by using the underlying `zcashd` instance via the following command and the new address will be displayed in zec-qt-wallet` as normal.

``` bash
zcash-cli getnewaddress sprout
```

## Sending from Sprout address to Sapling gives error
You cannot send directly from a Sprout address (zc) to a Sapling address (zs) as it must pass through the turnstile. See the details on the [turnstile migration](/turnstile-migration) for details on how to move your funds from a Sprout address to a Sapling one in a privacy-preserving way.

## Common error messages

### Could not start embedded zcashd

This means zec-qt-wallet couldn't start its embedded `zcashd` for some reason. zec-qt-wallet will show you another dialog box with the error reported from `zcashd` for debugging purposes as well. You might be able to solve this by simply restarting zec-qt-wallet, but if you repeatedly see this error, it might be one of the following reasons:

* If you compiled zec-qt-wallet yourself and are running it: `zcashd` doesn't come with the Github repository, so you'll have to compile `zcashd` separately and copy if over into your zec-qt-wallet directory.
* You might have corrupt zcash params: In this case, you may try deleting your params and letting zec-qt-wallet download them again.

If all else fails, you can run an external `zcashd` and zec-qt-wallet will connect to it.

### Authentication error

Normally, zec-qt-wallet can pick up the rpcuser/rpcpassword from `zcash.conf`. If it doesn't for some reason, you can set the username/password in the **File->Settings** menu. If you are connecting to a remote node, make sure that `zcashd` on the remote machine is accepting connections from your machine. The target machine's firewall needs to allow connections from your host and also `zcashd` is set to be configured to accept connections from this host.

// TODO see the warnings here and maybe rewrite this for best practises: rpcallowip https://zcash.readthedocs.io/en/latest/rtd_pages/zcash_conf_guide.html

### Not enough balance when sending transactions

The most likely cause for this is that you are trying to spend unconfirmed funds. Unlike Bitcoin, the Zcash protocol doesn't let you spent unconfirmed funds yet. Please wait for at least one confirmation and then retry the transaction.

## My issue isn't resolved
Open an [issue on Github]() or tweet at [@zecqtwallet](https://twitter.com/zecqtwallet) for help.