# Magi-Retro

## About Magi-Retro

**Magi-Retro project** original objective is to recreate the history of [Magi coin actual repo](https://github.com/magi-dev/magi) but coming from its actual older repo which seems to be [peercoin](https://github.com/magi-retro/peercoin).

You can find the final [reconstructed magi repo as peercoin here](https://github.com/magi-retro/peercoin).

## Additional objetives

- Fill gaps between old bitcoin forks
- Help new developers to find what Magi is about.

## What you can learn from this project

- How to create virtual commits
- How to put all of the commits together
- Some Magi history

## Magi history

Many people think that Magi coin started as Magi coin.
That's not right. Magi coin had a completly different codebase than the one it's using right now.
Magi coin was, back in the day **Magicoin**. That's why you see this weird name *Coin of the magi*.

You could actually exchange or swap those old Magiccoin coins to Magi coins.

- [2014 09 12 Magi thread snaphost](https://web.archive.org/web/20140912075652/https://bitcointalk.org/index.php?topic=735170.0) where you see a **Coin swap** section refering to Magi as a continuation of the Magicoin project.
- [2014 09 20 Magicoin thread snapshot](https://web.archive.org/web/20140920014622/https://bitcointalk.org/index.php?topic=548368.0) where it leads you to the new Magi thread link.

## Magi based on crypto projects source code

**Or the Magi code base history based on forks.**

- [Peercoin v0.2.2ppc](https://github.com/magi-retro/peercoin/commits/v0.2.2ppc/) was based on an older Bitcoin codebase.
- [Some Novacoin files](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-PEERCOIN-NOVACOIN/) were based on Peercoin v0.2.2.ppc and this was probably was not needed for the magi-retro project.
- [Bitgem](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-NOVACOIN-BITGEM/) was based on Novacoin 0.4.1 which was based on Peercoin v0.2.2.ppc.
- [Bottlecaps](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-BITGEM-BOTTLECAP/) was based on Bitgem which was actually quite similar to Novacoin 0.4.1.
- [Graincoin](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-BOTTLECAPS-GRAINCOIN/) was based on Bottlecaps 1.4.2.
- [Mintcoin](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-GRAINCOIN-MINTCOIN/) was based on Graincoin 1.4.0.
- [Ghostcoin](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-MINTCOIN-GHOSTCOIN/) was based on Mintcoin 1.4.0.
- [Whitecoin](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-GHOSTCOIN-WHITECOIN/) was based on Ghostcoin 1.0.2.
- [BadgerCoin](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-WHITECOIN-BADGERCOIN/) was based on Whitecoin 1.0.1.
- [zebrains-x11coin](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-BADGERCOIN-ZEBRAINSX11/) was based on BadgerCoin 0.9.1.2.
- [atcsecure-x11coin](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-ZEBRAINSX11-ATCSECUREX11/) was based on zebrains-x11coin 0.9.1.4.
- [Magicoin - First commit](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-X11COIN-MAGIv2/) was based on:
    - atcsecure-x11coin 0.9.1.33. (What this repo uses)
    - Probably some Bitcoin version from around 2014 09 15 which it is the first official Magi repo commit date.
- [Magicoin - Snapshot from 2021 02 14](https://github.com/magi-retro/peercoin/commits/MAGI-2021-02-14/) was based on its **Magicoin - First commit** as it is obvious.

## Random rambles about the project

### Misc notes

- POW_CUTOFF_HEIGHT is specific to X11Coin.
- Whitecoin. There is a Whitecoin project that forks from Blackcoin. And there is another Whitecoin project that from Ghostcoin. Magicoin fork history uses the Whitecoin project that has been forked from Ghostcoin.

### gitian-downloader keys unveils changes

Back in the day some coin developers used `sed` in order to change their ticker, the coin name and so on without knowning what they were doing.
This has helped us to find out some ancestor repos to the ones we were studying.

One clear example affects the `contrib/gitian-downloader/scottnadal-key.gpg` file.

As you might now a gpg file is not supposed to be changed, either you change it completly or you don't.

So... if there are two letters or three letters that change there you might find out that, yes, there has been a ticker change.
Take a look at these two commits:

- [WC gets changed onto BDG](https://github.com/magi-retro/peercoin/commit/98897226a1c37b22407c2a733707921970b9f5e7)
- [BDG gets changed onto XC](https://github.com/magi-retro/peercoin/commit/da8975290b537f51c49b1bb9cf79fcdec525723b)

### Dos2unix against comparisons

When a file seems completly different than another one it's worth running `dos2unix` or `unix2dos` on it to see if it needs to be converted in order to find out what are the actual differences.

### Renaming

You might need to rename some files like `.pro` files in order to compare them properly. Otherwise you won't find the actual useful changes.

### Detect changes based on port

You can find where a project was forked from if you checked all of the files where a port should have been changed. This was an example that compared whitecoin and zebrains-x11coin:

- doc/README:                15814.(default) 23489(default)
- doc/README_windows.txt:    15814(default) 23489(default)
- src/bitcoinrpc.cpp:        24071(rpc-testnet):15815(rpc-default) 22347(rpc-testnet):32347(rpc-default)
- src/init.cpp:              15814(default)!24070(testnet) 32348(default)!22347(testnet)
- src/init.cpp:              15815(rpc-default)!24071(rpc-testnet) 32347(rpc-default)!22347(rpc-testnet)
- src/protocol.h:            24070(testnet)!15814(default) 22347(testnet)!32348(default)
- src/qt/bitcoinstrings.cpp: 15814(default)!22788(testnet) 23489(default)!22788(testnet)

Summary:

- WhiteCoin non-rpc default port should be: 15814
- WhiteCoin non-rpc testnet port should be: 24070
- WhiteCoin     rpc default port should be: 15815
- WhiteCoin     rpc testnet port should be: 24071

Conclusion:

- Leftover from WhiteCoin (which comes from Mintcoin) is: 22788 (probably non-rpc) testnet port.
- Leftover from an intermediate fork previous to zebrains-x11coin: 23489 .

In the end we found out that **23489 port** was Badgercoin which was another fork which we were missing.

## About virtual commits

**Note: You are highly advised to read this Virtual commits introduction in order to read this git repo history.**

- [VIRTUAL_COMMITS_INTRODUCTION.md](VIRTUAL_COMMITS_INTRODUCTION.md)

## How to create virtual commits

- [VIRTUAL_COMMITS_CREATION.md](VIRTUAL_COMMITS_CREATION.md)

## How to put all of the commits together

- [VIRTUAL_COMMITS_FINAL_SQUASH.md](VIRTUAL_COMMITS_FINAL_SQUASH.md)

## Advice on resuming Magi development

### Introduction

Many people that have Magi coins from mining back in 2014 want the coin to be resumed in a more recent codebase.
Also, many people, just for fun want to learn how to improve Magi.
For all of you here there are some thoughts about how to push the Magi development forward.

### Misc notes

- The best approach would be to use peercoin as a base and then add the ProofOfWork stuff that has in additional Magi.
- You need to make a coin that does not need [checkpoints](https://github.com/magi-retro/peercoin/blob/MAGI-2021-02-14/src/checkpoints.cpp#L28-L55). Otherwise we are at the mercy of the private key of the coin creator.
- So,... before removing checkpoints it might be wise to replace the [public master key](https://github.com/magi-retro/peercoin/blob/MAGI-2021-02-14/src/checkpoints.cpp#L400) that creates the different checkpoints and use another one of your own so that you can say that you actually control the coin. This will probably need a fork (So double the coins and so on).

### About removing PoS or PoW

- At a time I thought that it was a good idea to remove either the PoW or the PoS part of Magi coin. Having both a PoW and PoS system at the same time it's very great but it comes with a cost regarding how easy it's the coin to maintain. You need to check the PoW ancestors and also the PoS ancestors and see how they are upgrading their codebases. If you only use either PoW or PoS it should easier. So just think about it.

### About exchanges

- What exchanges actually want is a codebase similar to recent codebase or coins that they already have so that it's easier to integrate onto their systems. So, maybe, peercoin is not a good idea because, right now, not too many big and well-known exchanges enable you to trade peercoin. You might want to find out another PoS coin, probably based on peercoin, which it's more used.

### Leveldb and memory

What actually makes a coin is its blockchain. Currently the blockchain is being saved onto a leveldb database which with the current blockchain size is not suitable for a 1 GB device.
So either something else like sqlite is used or the minimal requisites need to be something like 4 GiB or even 8 GiB of RAM.

**You should also think about doing an snapshot so that balances are kept but all of the history is lost.**

### Leveldb and forks

What actually makes a coin is its blockchain. Currently the blockchain is being saved onto a leveldb database.
Each one of the blocks define if they are either a PoS or a PoW block.

So if you want to remove either PoS or PoW you would need to create a versions that supports both of them, then does not allow, let's say, PoW, and then later on it only supports PoS in a new version.

This will also simplify the source code regarding how to deal with Leveldb.

### About learning old code

I think it's worth checking many of the forks mentioned here to see how they have evolved into the current days.
E.g.: Is it Badgercoin maintained nowadays? Is it still PoS? And so on.

- You could also check differences between the different peercoin big releases and try to apply that into the PoS part of Magi coin.
- You could also check differences between the different Bitcoin big releases and try to apply that into the PoW part of Magi coin.

- You could also use some of the comparison techniques used here to see what it's actually different in a recent peercoin version and Magi coin.

## Media

This work (including the documentation part of this own repo) was recorded in a Youtube playlist which you can check: [https://www.youtube.com/watch?v=5OUoClM9VuE&list=PLUCT1oZWwYjyix7qikVAlkY1cJ2QcVxpB&index=1](https://www.youtube.com/watch?v=5OUoClM9VuE&list=PLUCT1oZWwYjyix7qikVAlkY1cJ2QcVxpB&index=1).
