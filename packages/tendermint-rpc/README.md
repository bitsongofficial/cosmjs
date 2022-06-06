# @cosmjs-rn/tendermint-rpc

[![npm version](https://img.shields.io/npm/v/@cosmjs-rn/tendermint-rpc.svg)](https://www.npmjs.com/package/@cosmjs-rn/tendermint-rpc)

This package provides a type-safe wrapper around
[Tendermint RPC](https://docs.tendermint.com/master/rpc/). Notably, all binary
data is passed in and out as `Uint8Array`, and this module is reponsible for the
hex/base64 encoding/decoding depending on the field and version of Tendermint.
Also handles converting numbers to and from strings.

## License

This package is part of the cosmjs repository, licensed under the Apache License
2.0 (see [NOTICE](https://github.com/bitsongofficial/cosmjs-rn/blob/main/NOTICE) and
[LICENSE](https://github.com/bitsongofficial/cosmjs-rn/blob/main/LICENSE)).
