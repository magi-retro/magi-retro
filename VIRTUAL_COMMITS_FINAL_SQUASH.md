# Virtual Commits - Putting all of them together

## Requisites

Please read [VIRTUAL_COMMITS_INTRODUCTION.md](VIRTUAL_COMMITS_INTRODUCTION.md) and [VIRTUAL_COMMITS_CREATION.md](VIRTUAL_COMMITS_CREATION.md) first.

## Introduction

Basically the commits that start in a future repo are dumped as email attachments.
Then those email attachments are converted onto commit in the past repo.

This method is not perfect but works fine most of the time.

## Dump commits onto email attachments.

- Past repo: peercoin (bottlecap branch)
- Future repo: graincoin (New branch: `MANUAL-FORK-BOTTLECAPS-GRAINCOIN`)

```
cd ~/github/magi-retro-repos/bottlecaps/
mkdir ../bottlecaps-dump
git checkout MANUAL-FORK-BOTTLECAPS-GRAINCOIN
git format-patch -o ../bottlecaps-dump/ INITIAL_COMMIT_BRANCH
```

## Convert email attachments onto commits

- Past repo: peercoin (bottlecap branch)
- Future repo: graincoin (New branch: `MANUAL-FORK-BOTTLECAPS-GRAINCOIN`)

```
cd ~/github/magi-retro-repos/peercoin/
git checkout MANUAL-FORK-BITGEM-BOTTLECAP -b MANUAL-FORK-BOTTLECAPS-GRAINCOIN
for npatch in ../bottlecaps-dump/*patch ; do echo "$npatch" ; git am --keep-cr $npatch ; done
```
