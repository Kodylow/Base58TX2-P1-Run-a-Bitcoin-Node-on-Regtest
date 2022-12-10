# Using the `bitcoin-cli`

## What's a "-daemon"?
A command line terminal has 1 "foreground" process and many "background" processes. The background processes are often called "daemons". Background processes do not output logging information to your terminal and they don't steal control flow. Since the program is running "in the background", you can continue using the terminal's foreground process to input commands.

The `-daemon` flag tells bitcoin core to start itself as a background process. 

Run the following command to start bitcoind in the foreground of your shell, see what happens for a couple seconds, then kill the foreground process by hitting `Ctrl-c`.  Notice how you're not able to input any new commands when bitcoind is running in the foreground.

- [ ] `$ bitcoind -regtest`
- [ ] `Ctrl-c`

Bitcoin Core does a lot of different things as you can see from the logs, but we don't need all that logging right now. We just need it to run as a background process in the repl, then in the foreground of the terminal we'll issue commands using the bitcoin command line interface `bitcoin-cli`

## The "-regtest" flag: Running bitcoind on Different Networks
Once installed, we can run bitcoin and point it at the network we want to run the node on. Bitcoin core can run on many different networks.

- **Mainnet**: The main network has "real" bitcoins that are valuable and trade for tens of thousands of dollars. This is the network people are normally referring to when they talk about "Bitcoin". You can check out the blockchain and specific blocks/transactions/addresses using a "block explorer" like [mempool.space](mempool.space) or [blockstream.info](blockstream.info)

There are other networks we can use for testing and experimenting:

- **Testnet**: Testnet is identical to mainnet, except Testnet coins have no value. The testnet network, like mainnet, produces blocks through "mining". Testnet is mostly used to test mining software, or to stress test other bitcoin apps where the variable blocktime can provide unique insights.  [Mempool](mempool.space/testnet) and [Blockstream](blockstream.info/testnet) both have similar explorers for testnet .
  > Note that the time between blocks on testnet varies wildly. Sometimes  it will take 20 minutes for a new block to be found, other times there will be 20 blocks found in an hour. 

- **Signet**: this is a "signature network". Signets are identical to mainnet in every way EXCEPT that there is no mining: Signet blocks are created every 10 minutes when the bitcoin developers who run the Signet "sign" a new block into existence. Signet lets us connect and send transactions to other developers the same way the bitcoin network does, so is useful for testing wallet and other transactions software. It just doesn't have mining, so the blocks always come exactly at every 10 minutes instead of approximately every 10 minutes like they do on mainnet and testnet.
  
- **Regtest**: This is the "Regression Testing Network". Regtest is designed for local development by a solo developer, normally on a single device. New blocks are created with a shell command, `generatetoaddress`.

> We're just doing local practice for this exercise, so we'll be running bitcoin on `regtest`. In some of the following exercises we'll be connecting to the Base58 Signet, where you'll be able to send signet bitcoins to and from your friends or classmates :)

For regtest, we must set a "fallbackfee rate". Normally, your wallet calculates a fallback fee for transactions based on current network conditions. But we're the only ones using our private regtest network so there's no other transactions besides the ones we're creating. Instead, we set the feerate ourselves at start.

- [ ] Run the following command to start Bitcoind on regtest as a background process in the repl:

    `bitcoind -regtest -daemon -fallbackfee=0.0000025`

You should see the following print to your shell: `Bitcoin Core starting`. If you see a message that bitcoind can't get a lock on the directory, kill the process with `bitcoin-cli -regtest stop` then run the above startup command again and you should see the 'Bitcoin Core starting' message.

Now that bitcoind is running on regtest, you should be able to send commands to it using the bitcoin-cli tool. 
- [ ] Run the following to see the complete list of bitcoin-cli commands

    `bitcoin-cli -regtest help`