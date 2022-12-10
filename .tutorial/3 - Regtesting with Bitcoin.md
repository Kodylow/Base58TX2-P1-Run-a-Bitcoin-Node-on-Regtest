# Regtesting with Bitcoin

### A regtest alias:
Bitcoin software's defaults are set to mainnet, so whenever we're using a different network like regtest we have to pass in the network as a flag. It's annoying to type out 'bitcoin-cli -regtest' every time, so let's alias it to `bcr` with the following shell command:

    `alias bcr="bitcoin-cli -regtest"`

You should now be able to run that same `help` command with the alias as `bcr help`.

## Creating a regtest wallet
There's a couple quirks to regtest: we're the only one using it, we mine all the blocks manually, it starts from scratch, but otherwise it operates the same way as bitcoin normally does. So when we start our regtest blockchain, there's no blocks and we don't have any bitcoin yet.

We can confirm this with the following commands, try running them in the terminal:
- [ ] `bcr getblockchaininfo`
- [ ] `bcr listunspent` (If you have bitcoins, this will list the coins as json in the terminal, but we don't even have a wallet yet, much less coins.)

So let's create a wallet called "regwallet" that we'll use to store our bitcoins. There's a bitcoin-cli command called `createwallet`, we can ask the cli what arguments we need to pass to make our wallet:
- [ ] `bcr help createwallet`

There's a bunch of configuration options that are beyond the scope of this minicurriculum, we just want to name the wallet so let's run:
- [ ] `bcr createwallet regwallet`

That should return the following JSON, if it doesn't you need to start bitcoin core again using the command on line 69:

    {
      "name": "regwallet",
      "warning": ""
    }

## Mining Regtest Bitcoins:
Again, we have complete control of our regtest bitcoin blockchain. We can get ourselves some bitcoins by mining blocks which pay out bitcoins directly to our wallet. Let's get a new address from our wallet:

- [ ] `bcr getnewaddress`

Then mine a block with our address receiving the bitcoins:

- [ ] `bcr generatetoaddress 1 <your-new-address-here>`

The `generatetoaddress` command only works in regtest: it immediately mines a new block on the blockchain paying out the miner's reward to the specified address. The result you get back is an array with a single hash. The hash is the hash of the block you just magically mined. 
 
 We can get some info about the new block with the command:

- [ ] `bcr getblock <your-blockhash-here>`

The result is a JSON object with a bunch of block data. Most of this information comes from the 'blockheader'. 

We're interested in the single tx (transaction) included in the block, which we can see in the "tx": [] array. As of version v24 of bitcoin-core, it is the last item in the JSON object.

```
  "tx": [
    "e537b460f4387491aaf343120f9eb93a18cac55fa9949c024d7b4145e3a079b8" # your txid will be different
  ]
```