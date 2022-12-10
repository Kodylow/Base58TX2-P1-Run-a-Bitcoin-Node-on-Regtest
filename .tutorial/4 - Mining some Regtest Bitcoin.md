# Regtest Coinbase Transactions
The tx (transaction) you just pulled is the "coinbase" transaction. It is the only transaction in this block. The coinbase transaction pays the miner a reward for mining the block, bitcoin-core adds it automatically on regtest blocks. 

The block reward starts at 50 regtest bitcoins. It gets paid to the address you specified in `generatetoaddress`. Let's confirm that we got them at our address by running:

- [ ] `bcr gettransaction <tx>`

This will return a JSON object with details about the tx. We're interested in the "details" section.


### Regtest Block Confirmations:

    "details": [
        {
          "address": "address-you-passed-in-earlier",
          "category": "immature",
          "amount": 50.00000000,
          "label": "",
          "vout": 0
        }
      ]

The coins in this transaction are categorized as "immature" (see 2nd line). 

There's a rule in bitcoin that coinbase transactions are only spendable after 100 MORE blocks get mined on top of it. We call these blocks building on top "confirmations". (This is only for the coinbase transactions, normal bitcoin transactions don't require that many confirmations.) So if we check our wallet for unspent coins with `listunspent` ...:

- [ ] `bcr listunspent`

We'll see we don't have any spendable coins (it returns an empty array). 

To make the tx spendable, mine another 100 blocks. The following command will do this:

- [ ] `bcr generatetoaddress 100 $(bcr getnewaddress)`

> The $(bcr getnewaddress) part just grabs a new address in a single command, it's a useful shell trick for doing multiple commands in a single line.

We've now got 101 blocks in our regtest blockchain, which we can confirm with the command. Look for the `blocks` field.

-[ ] `bcr getblockchaininfo`

This should make our the coinbase from block one spendable. Let's check our list of unspent coins again. We should have one result now.

- [ ] `bcr listunspent`

This process of mining regtest bitcoin to ourselves is important to get right, because we'll be doing it for all the regtest exercises to initially get the coins we'll be using to practice digital signatures and transactions.