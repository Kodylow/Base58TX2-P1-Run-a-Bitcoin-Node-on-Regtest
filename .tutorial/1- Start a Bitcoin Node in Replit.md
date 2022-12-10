# Starting a Bitcoin Node in Replit

### Installing bitcoind, the bitcoin daemon
We're going to walk through how to set up a bitcoin node. Bitcoin is a distributed, peer-to-peer network. A "node" on the network is a computer process running Bitcoin Core software that does a couple things:
- it maintains a complete history of the bitcoin blockchain
- it maintains the current "state" of all the bitcoins. This is called the "Unspent Transaction Outputs Set" or the "UTXO Set" (more on this later).

Replit uses nixOS for its backend, so installing bitcoin is as easy as adding the bitcoin nix package to your dependencies.

### Installation instructions
Check off the following boxes as you work through the exercise.

- [ ] Click the 3 dots next to "Files" on the left hand side of your screen. You should see a menu pop up with 4 options:
    - Upload file
    - Upload folder
    - Download as zip
    - Show hidden files

- [ ] Select 'Show hidden files' to see the repl config files: .replit & replit.nix
> If you see a "Hide hidden files" option instead, you can skip this

- [ ] Open `replit.nix`
- [ ] Add the bitcoin package dependency to the 'deps' list. Keep all the other dependencies. It should look like this when you're finished.

```
    deps = [
        pkgs.bitcoin,
        ...
    ]
```

- [ ] Open the Shell tab in your repl and hit Enter. Your repl will detect the change and install bitcoin core.
- [ ] Run the following command to start bitcoin in your repl (we'll go over what the flags mean later):
    - [ ] 
      `$ bitcoind -daemon -regtest`

You should see a message in your terminal:
`Bitcoin Core starting`

### You've now got bitcoin running in your repl!

Continue reading to learn a little more about those flags you passed in and some alternate options for configuring your node.