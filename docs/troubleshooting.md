# Troubleshooting

---

## The `zcashd` debug log

## My node isn't syncing

## My transaction didn't get mined

## How to perform a wallet rescan

## How to perform a reindex

## If your displayed balance is incorrect

## If you have no connections

## Some of my shielded transactions are not displayed in the transaction tab

## I can't generate a new Sprout address

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

## Sending from a Sprout address to a Sapling one
