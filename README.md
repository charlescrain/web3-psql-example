# web3-psql

Using the [selda](https://github.com/valderman/selda) and [hs-web3](https://github.com/f-o-a-m/hs-web3) libraries it should be possible to build an event indexer for free using template haskell and generics. This is sort of a sketch pad for how we can imagine doing that. The generated event indexer wont be optimized, but it will make it easy to spin up a postgres backend for any smart contract that corresponds to the events emmited by that contract.

## build
```bash
> make all
```

## run
```bash
> env CONTRACT_ADDRESS=<YOUR ERC20 ADDRESS> make transfer-indexer
```

## future work
It's clear that the abi quasi-quoter plus generic derivations are going to unlock a lot of awesome things. From immediate plug and play with postgres, to pretty printing, json serialization, and maybe even some integration with servant in the future. This repo is exploring what the postgres integration looks like. It seems that selda is a good choice because it is actively developed, has amazing support for generics, and is pretty built out in terms of features -- e.g. supports joins. It seems like all that is needed in order to make this work is some sort of `web3-sql` library that gives instances for selda's `SqlType` class to all the solidity types defined in `hs-web3`. You can see the `Orphans.hs` module in this repo for an example of what that might look like.
