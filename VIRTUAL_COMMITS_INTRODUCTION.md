# Virtual Commits Introduction

## What are virtual commits?

Magi-Retro project is about reconstructing the history of Magi coin from its older peercoin repo to its newest x11coin repo. There are like 8 or 9 jumps/gaps between those different repos. And what's a gap? Well, it's just a cryptocurrency repo becoming alive with either a tar.gz or a git repo of its own (usually in Github) which **does not have any proper GIT/commit connection with the original is being based from**.

Let me give an example of this gap.

[Bottlecaps](https://github.com/magi-retro/bottlecaps/commits/master/) is a cryptocurrency that apparently ended its development at 2017. Its [initial commit](https://github.com/magi-retro/bottlecaps/commits/INITIAL_COMMIT_BRANCH) is from 2013 06 23. If you dig into the actual [BottleCaps Initialized commit](https://github.com/magi-retro/bottlecaps/commit/65c2cc8383ac1ab751bd5fda31f275197bec62e0) you can see how it adds plenty of files that somehow are very similar to other projects from 2013 such as peercoin or bitcoin itself.

Well, it happens to be that Bottlecaps was based on Bitgem which it's quite similar to Novacoin 0.4.1. So... Novacoin is an actual fork of Peercoin and you can find actual commits from those days that connect both projects.

Although Bottlecaps was based on Bitgem there are no commits from those days connecting both repos.

In order to understand how Magi base code evolved even from projects prior to it we need to **create those commits** even if they did not exist back in the day.

We are going to call such commits as **Virtual commits**.

## About commit prefixes

Many of the virtual commits have a prefix that reveals what this virtual commit is about.
Unfortunately their names weren't initially well thought out so some of them might seem a bit confusing.
This can be clarified thanks to the following list with the different meanings:

- FORK-MAGI : **From atcsecure-x11coin** forking commit **to Magi coin** first useful initial commit. ([MANUAL-FORK-X11COIN-MAGIv2 branch](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-X11COIN-MAGIv2/))
- FORK-ATCSECUREX11 : **From zebrains-x11coin** forking commit **to atcsecure-x11coin** first useful initial commit. ([MANUAL-FORK-ZEBRAINSX11-ATCSECUREX11 branch](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-ZEBRAINSX11-ATCSECUREX11/))
- FORK-BADGERX11 : **From badgercoin** forking commit **to zebrains-x11coin** first useful initial commit. ([MANUAL-FORK-BADGERCOIN-ZEBRAINSX11 branch](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-BADGERCOIN-ZEBRAINSX11/))
- FORK-BADGER : **From whitecoin** forking commit **to badgercoin** first useful initial commit. ([MANUAL-FORK-WHITECOIN-BADGERCOIN branch](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-WHITECOIN-BADGERCOIN/))
- FORK-WHITE : **From ghostcoin** forking commit **to whitecoin** first useful initial commit. ([MANUAL-FORK-GHOSTCOIN-WHITECOIN branch](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-GHOSTCOIN-WHITECOIN/))
- FORK-GHOST : **From mintcoin** forking commit **to ghostcoin** first useful initial commit. ([MANUAL-FORK-MINTCOIN-GHOSTCOIN branch](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-MINTCOIN-GHOSTCOIN/))
- FORK-MINT : **From graincoin** forking commit **to mintcoin** first useful initial commit. ([MANUAL-FORK-GRAINCOIN-MINTCOIN branch](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-GRAINCOIN-MINTCOIN/))
- FORK-GRAIN : **From bottlecaps** forking commit **to graincoin** first useful initial commit. ([MANUAL-FORK-BOTTLECAPS-GRAINCOIN branch](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-BOTTLECAPS-GRAINCOIN/))
- FORK-BOTTLE : **From bitgem** forking commit **to bottlecaps** first useful initial commit. ([MANUAL-FORK-BITGEM-BOTTLECAP branch](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-BITGEM-BOTTLECAP/))
- FORK-BITGEM : **From novacoin** forking commit **to bitgem** first useful initial commit. ([MANUAL-FORK-NOVACOIN-BITGEM branch](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-NOVACOIN-BITGEM/))
- FORK-NOVA : **From peercoin** forking commit **to novacoin** first useful initial commit. ([MANUAL-FORK-PEERCOIN-NOVACOIN branch](https://github.com/magi-retro/peercoin/commits/MANUAL-FORK-PEERCOIN-NOVACOIN/))

## About commit subject labels on Virtual commits

These virtual commits do not have usual commit messages with an explanation of the changes that the commit has done to the repo or to several files on it.

In addition to those message we have added some labels so that it's easier to identify useful commits from non-useful commits.
A commit can have more than one label.
This is a list regarding almost all of those labels which start and end like this: `[LABELNAME]` and their intended meaning.

- `[REMOVE]`: It's probably non useful for understanding what Magi project is about. It might be a ticker name change, a coin name change, some image files being changed, etc.
- `[REPLACE-IMAGES]`: Some images have their content being replaced to match the new project images.
- `[REPLACE-TICKER]`: E.g. Bottlecaps becomes Graincoin so... BOT becomes GRA.
- `[REPLACE-COINNAME]`: E.g. Bottlecaps becomes Graincoin.
- `[CHANGE-SEED]`: Change either DNS seeds or IP seeds.
- `[CHANGE-GENESIS]` - The blockchain genesis commit is changed from one newspaper headline to another newspaper headline.
- `[CHANGE-MERKLEROOT]`: Similar to Change Genesis but regarding to Merkleroot.
- `[CHANGE-CHECKPOINTS]`: Change the different checkpoints that hardcode valid commits from the blockchain on the software.
- `[CHANGE-DOTPRO]`: Change X11Pro or similar
- `[DOUBT]`: We are not sure if this is useful or not for understanding what Magi project is about.
- `[PUBKEY-ADDRESS]`: Pubkey address is changed.
- `[CHANGE-PORT]`: Change ports where the software is listening for incoming connections. Production and testnet.
- `[CONFIRMATIONS-NUMBER]`: Number of confirmations when the coin considers that a transaction is finally a valid transaction.
- `[SPECIFIC]`: Specific to the current repo fork that we are studying.
- `[NEWANDCOMMENT]`: New content that it's worth a comment.
- `[PCHMESSAGESTART]`: Regarding PCH Message start.
- `[ADAPT]`: **Useful for understanding what Magi project is about.**

## Virtual commit message example

```
FORK-MAGI: [ADAPT] Delete non unsed Thumbs.db files.
```
