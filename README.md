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
- About changes to contrib/gitian-downloader/richardsmith-key.gpg .
- dos2unix against comparisons.
- Whitecoin. There is a Whitecoin project that forks from Blackcoin. And there is another Whitecoin project that from Ghostcoin. Magicoin fork history uses the Whitecoin project that has been forked from Ghostcoin.

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
