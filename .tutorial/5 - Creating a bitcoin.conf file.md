# Creating a bitcoin.conf File

There's actually a much easier way to pass configuration options into bitcion and that's by using a "configuration file" where we put all the settings we'd like for our bitcoin node, then only pass the conf file in through the command line. All the flags we've been passing in with the command line are arguments you can set in the conf file.

Jameson Lopp, a long time developer in bitcoin, made an excellent tool for building properly formatted configuration files, feel free to [check it out](https://jlopp.github.io/bitcoin-core-config-generator/)!

The flags we've been using so far are `-regtest -daemon -fallbackfee=0.0000025`

You can set your conf file to use those settings by creating file called `bitcoin.conf` that has the following text in it

```
regtest=1
daemon=1
fallbackfee=0.0000025
```

Then when you start your bitcoind process, the only flag to pass in is 

`bitcoind -conf=$(pwd)/bitcoin.conf`

which will load the configuration file and set the appropriate settings.

You can set different settings for the different networks (mainnet, testnet, signet, regtest), or set general settings. This is normally the best practice: to set all your configurations in a .conf file except which network to start on, then when starting bitcoind to pass in the network and configuration file.
- [ ] Create a file called `bitcoin.conf`
- [ ] Set the configuration settings above
- [ ] Start your bitcoin node by running `bitcoind -conf=$(pwd)/bitcoin.conf`

And your node should be running on regtest with the proper configurations. You can confirm by running `bitcoin-cli -regtest getblockchaininfo` (we still have to pass in the network flag to the cli tool even if you're using a conf file setup)


###  That's it, congratulations on finishing Project 1A!

### Jump back to Udemy to continue the course!