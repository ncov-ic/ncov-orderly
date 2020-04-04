# ncov-orderly

[![Build status](https://badge.buildkite.com/c46c74b1e9d8e487dd701a8fae599582d971a98e6d1e303bc4.svg?branch=master)](https://buildkite.com/mrc-ide/ncov-orderly)

This is the docker container for [ncov-outputs](https://github.com/ncov-ic/ncov-outputs).  It exists outside that repository because otherwise every new report we use risks dragging in a new LaTeX installation.

This repo is a fork of [`montagu-orderly`](https://github.com/vimc/montagu-orderly) with minor modifications

**Interaction with the server**.  These commands interact with the orderly server on the *same host* as you run it.  If you run these on your desktop they will not affect any other machine.

Make sure you have the most recent version of the container with with

Update the `ncov-outputs` repo on the orderly volume

```
./pull_sources
```

Run orderly commands with

```
./orderly run <name>
./orderly list names
./orderly --help
```

etc.

Get a shell on the container with

```
./shell
```

## Building the image

The image is built on [Buildkite](https://buildkite.com/mrc-ide/ncov-orderly), as it is too large to build on travis now (build times out after an hour).
