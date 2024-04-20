# Virtual Commits Creation

## Requisites

Please read [VIRTUAL_COMMITS_INTRODUCTION.md](VIRTUAL_COMMITS_INTRODUCTION.md) first.

## About INITIAL_COMMIT_BRANCH

Many of the repos have a branch named `INITIAL_COMMIT_BRANCH` that only has the very first commit on the repo.
That's made in order to ease some of the reconstruction tasks to put everything together again.

## Create commits as normal

So the additional commits are usually created as you would do any commit.
There's nothing special about them.

The magi-retro virtual commits have been added to different repos to ease its development.

## Find commit where a repo has been forked into another repo (Mode 1)

This is an actual exercise when we were not very sure about were Magi came from.
Back in the day we thought that Magi was directly forked from peercoin.
And we suspected, probably according to the first Magic commit that it had to be a version from peercoin from v0.3.0ppc to v0.4.0ppc.rc1.

The comparison is made on two steps.

Step 1: We create fake commits that the only thing that they do is deleting anything peercoin related and adding Magi initial commit onto it.
This is done for every commit that it's available from v0.3.0ppc to v0.4.0ppc.rc1 in the peercoin repo.

Step 2: We can compare each one of the origin commits to their 'Magi initial commit' replaced ones that we have created. The comparison is measured in number of lines.

So, basically the result is a file, let's name it: peercoin-magi-differences34.txt that alongside each one the commits it has its number of lines difference with the initial Magi commit.

The optimal result should be something similar to this:
Warnings:
    - We have added a fake date column to that differences file)
    - Commits are much longer than what depicted

```
2014-02-01 abc123 200
2014-02-04 abc144 150
2014-02-10 edc160  98
2014-02-15 fse160  20
2014-02-18 fde160  50
2014-02-21 fde190  75
2014-02-25 fde210 125
```

This result would give us a hint about commit from: `2014-02-15 fse160  20` line is the one Magi has been forked from.

Here there are the actual bash helpful snippets that were used:

**Create fake commits for comparison**

To be run in peercoin repo.

```
for ncommit in $(git rev-list --ancestry-path v0.3.0ppc..v0.4.0ppc.rc1); do

git checkout "${ncommit}" -b 'fakemagi-old-'"${ncommit}";
mkdir ../peercoin-manual-delete;
mv * ../peercoin-manual-delete;
rm -rf ../peercoin-manual-delete;
cp -a ../magi-initial-commit/* ./;
git checkout -b 'fakemagi-new-'"${ncommit}";
git add .;
git commit -m 'fakemagi-'"${ncommit}";

done
```

**Actual comparison based on number of lines.**

To be run in peercoin repo.

```
echo "" > ../peercoin-magi-differences34.txt
for ncommit in $(git rev-list --ancestry-path v0.3.0ppc..v0.4.0ppc.rc1); do

echo -e -n "${ncommit}\t" >> ../peercoin-magi-differences34.txt;
numdiff=$(git diff "${ncommit}" 'fakemagi-new-'"${ncommit}" | wc -l);
echo -e -n "${numdiff}\n" >> ../peercoin-magi-differences34.txt;

done
```

## Find commit where a repo has been forked into another repo (Mode 2)

This is similar to Mode 1 but we don't measure number of lines of code that have been changed.
We are going to check number of files that have been changed which seems to be cleaner.

In this case we looping from v0.2rc2 to v0.4.0ppcrc1 versions.

**Create fake commits for comparison**

```
for ncommit in $(git rev-list --ancestry-path v0.2rc2..v0.4.0ppc.rc1); do

git checkout "${ncommit}" -b 'fakemagi-old-'"${ncommit}";
mkdir ../peercoin-manual-delete;
mv * ../peercoin-manual-delete;
rm -rf ../peercoin-manual-delete;
cp -a ../magi-initial-commit/* ./;
git checkout -b 'fakemagi-new-'"${ncommit}";
git add .;
git commit -m 'fakemagi-'"${ncommit}";

done
```
**Actual comparison based on number of files.**

```
echo "" > ../peercoin-magi-differences-bigcompare-1.txt
for ncommit in $(git rev-list --ancestry-path v0.2rc2..v0.4.0ppc.rc1); do

echo -e -n "${ncommit}\t" >> ../peercoin-magi-differences-bigcompare-1.txt;
numdiff=$(git diff "${ncommit}" 'fakemagi-new-'"${ncommit}" | grep 'diff --git' | wc -l);
echo -e -n "${numdiff}\n" >> ../peercoin-magi-differences-bigcompare-1.txt;

done
```

Please check **Mode 1** for how to read the differences file and find out which it's the most probable commit where the code has been forked from.

## Forward creation of commits

Sometimes when you are too much of stuck in the prediction on where you are supposed to be forking a repo you can force the fork thanks to some obvious replacements.
So you can create a new branch like: `mintcoin-magi-fork-commit-candidate-1-replace-to-step1` and then apply commits after applying these changes:

```
find -type f -exec sed -i 's/MintCoind/magid/g' {} \;
find -type f -exec sed -i 's/Mintcoin-qt/magi-qt/g' {} \;
find -type f -exec sed -i 's/MintCoin/Magi/g' {} \;
find -type f -exec sed -i 's/mintcoin-qt/magi-qt/g' {} \;
find -type f -exec sed -i 's/mintcoin/magi/g' {} \;
```

This might help you on finding which commit is the original one when the fork was actually done.

Now the project is finished I don't recommend this forward creation of commits but just use `git add -i` to add the individual changes.

This is another example of forward creation of commits:

```
find -type f -name 'README_windows.txt' -exec sed -i 's/2013-2014 X11Coin Developers/2013-2014 Magi Developers/g' {} \;
find -type f -name 'README' -exec sed -i 's/2013-2014 X11Coin Developers/2014 Magi Developers/g' {} \;
find -type f -exec sed -i 's/2012-2013 The X11Coin/2012-2014 The Magi/g' {} \;
find -type f -exec sed -i 's/2013-2014 X11Coin/2014 Magi/g' {} \;
find -type f -exec sed -i 's/X11Coin.conf/magi.conf/g' {} \;
find -type f -exec sed -i 's/X11Coin.pro/magi-qt.pro/g' {} \;
find -type f -exec sed -i 's/X11Coind.pid/magid.pid/g' {} \;
find -type f -exec sed -i 's/X11Coin.pid/magi.pid/g' {} \;
find -type f -exec sed -i 's/X11Coin.ico/magi.ico/g' {} \;
find -type f -exec sed -i 's/#X11Coin/#magi/g' {} \;
find -type f -exec sed -i 's/X11Coind \[options\]/magid [options]/g' {} \;
find -type f -exec sed -i 's/server or X11Coind/server or magid/g' {} \;
find -type f -exec sed -i 's/x11coind/magid/g' {} \;
find -type f -exec sed -i 's/X11Coin-qt/magi-qt/g' {} \;
find -type f -exec sed -i 's/provides X11Coin-Qt/provides magi-Qt/g' {} \;
find -type f -exec sed -i 's/X11Coin-Qt/Magi-Qt/g' {} \;
find -type f -exec sed -i 's/X11Coin/Magi/g' {} \;
find -type f -exec sed -i 's/x11coin-qt/magi-qt/g' {} \;
find -type f -exec sed -i 's/x11coin/magi/g' {} \;
find -type f -exec sed -i 's/ThreadBitcoinMiner/ThreadMagiMiner/g' {} \;
find -type f -name 'bitcoinstrings.cpp' -exec sed -i 's/rpcuser=bitcoinrpc/rpcuser=magirpc/g' {} \;
```

which was associated to the `x11coin-magi-fork-commit-candidate-1-replace-to-step1` branch.

## MELD

**TODO**
