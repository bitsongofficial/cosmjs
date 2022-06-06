# CHANGELOG

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to
[Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

## [0.27.1] - 2022-01-26

### Added

- @cosmjs-rn/cosmwasm-stargate: Add `fromBinary`/`toBinary` to convert between
  JavaScript objects and the JSON representation of `cosmwasm_std::Binary`
  (base64).
- @cosmjs-rn/cosmwasm-stargate: Export `WasmExtension` and `setupWasmExtension`.
- @cosmjs-rn/ledger-amino: Added `LedgerSigner.showAddress` and
  `LaunchpadLedger.showAddress` to show the user's address in the Ledger screen.

### Changed

- @cosmjs-rn/stargate: The error messages for missing types in `AminoTypes` now
  contain the type that was searched for ([#990]).
- @cosmjs-rn/tendermint-rpc: Change the `Evidence` type to `any` and avoid decoding
  it. The structure we had before was outdated and trying to decode it led to
  exceptions at runtime when a block with actual values was encountered.
  ([#980])

[#990]: https://github.com/bitsongofficial/cosmjs-rn/pull/990
[#980]: https://github.com/bitsongofficial/cosmjs-rn/issues/980

## [0.27.0] - 2022-01-10

### Added

- @cosmjs-rn/tendermint-rpc: Add `hash` field to `BroadcastTxAsyncResponse`
  ([#938]).
- @cosmjs-rn/stargate: Add `denomMetadata` and `denomsMetadata` to `BankExtension`
  ([#932]).
- @cosmjs-rn/stargate: Merge `DeliverTxFailure` and `DeliverTxSuccess` into a
  single `DeliverTxResponse` ([#878], [#949]). Add `assertIsDeliverTxFailure`.
- @cosmjs-rn/stargate: Created initial `MintExtension`.
- @cosmjs-rn/stargate: Created `types.Dec` decoder function
  `decodeCosmosSdkDecFromProto`.
- @cosmjs-rn/amino: Added `StdTx`, `isStdTx` and `makeStdTx` and removed them from
  @cosmjs-rn/launchpad. They are re-exported in @cosmjs-rn/launchpad for backwards
  compatibility.
- @cosmjs-rn/stargate: Add `GasPrice.toString`.

[#938]: https://github.com/bitsongofficial/cosmjs-rn/issues/938
[#932]: https://github.com/bitsongofficial/cosmjs-rn/issues/932
[#878]: https://github.com/bitsongofficial/cosmjs-rn/issues/878
[#949]: https://github.com/bitsongofficial/cosmjs-rn/issues/949

### Fixed

- @cosmjs-rn/tendermint-rpc: Add missing `BlockSearchResponse` case to `Response`.

### Changed

- @cosmjs-rn/stargate: Remove verified queries from `AuthExtension` and
  `BankExtension` as well as `StargateClient.getAccountVerified` because the
  storage layout is not stable across multiple Cosmos SDK releases. Verified
  queries remain available in the `IbcExtension` because for IBC the storage
  layout is standardized. Such queries can still be implemented in CosmJS caller
  code that only needs to support one backend. ([#865])
- @cosmjs-rn/tendermint-rpc: Remove default URL from `HttpClient` and
  `WebsocketClient` constructors ([#897]).
- all: Upgrade cosmjs-types to 0.4. This includes the types of the Cosmos SDK
  0.44 modules x/authz and x/feegrant. It causes a few breaking changes by
  adding fields to interfaces as well as changing `Date` to a `Timestamp`
  object. ([#928])
- @cosmjs-rn/stargate and @cosmjs-rn/cosmwasm-stargate: Add simulation support
  ([#931]).
- @cosmjs-rn/tendermint-rpc: Remove `Tendermint33Client` and related symbols.
- @cosmjs-rn/cosmwasm-stargate: Add support for wasmd 0.21. This changes the AMINO
  JSON representation of `Msg{Execute,Instantiate,Migrate}Contract.msg` from
  base64 strings to JSON objects. ([#948])
- @cosmjs-rn/cli: Replace `colors` dependency with `chalk` (see
  https://snyk.io/blog/open-source-npm-packages-colors-faker/)

[#865]: https://github.com/bitsongofficial/cosmjs-rn/issues/865
[#897]: https://github.com/bitsongofficial/cosmjs-rn/issues/897
[#928]: https://github.com/bitsongofficial/cosmjs-rn/issues/928
[#931]: https://github.com/bitsongofficial/cosmjs-rn/pull/931
[#709]: https://github.com/bitsongofficial/cosmjs-rn/issues/709
[#948]: https://github.com/bitsongofficial/cosmjs-rn/pull/948

## [0.26.6] - 2022-01-10

### Changed

- @cosmjs-rn/cli: Replace `colors` dependency with `chalk` (see
  https://snyk.io/blog/open-source-npm-packages-colors-faker/)

## [0.26.5] - 2021-11-20

### Added

- @cosmjs-rn/amino: The `coin` and `coins` helpers now support both `number` and
  `string` as input types for the amount. This is useful if your values exceed
  the safe integer range.

### Fixed

- @cosmjs-rn/tendermint-rpc: Fix undefined `this` in `decodeBroadcastTxAsync` and
  `broadcastTxAsync` ([#937]).

[#937]: https://github.com/bitsongofficial/cosmjs-rn/pull/937

## [0.26.4] - 2021-10-28

### Fixed

- @cosmjs-rn/cosmwasm-stargate: Fix response error handling for smart queries.

## [0.26.3] - 2021-10-25

### Added

- @cosmjs-rn/ledger-amino: Add support for using forks of the Cosmos Ledger app by
  adding the fields `LaunchpadLedgerOptions.ledgerAppName` and
  `.minLedgerAppVersion`.

### Deprecated

- @cosmjs-rn/stargate: The verified queries from `AuthExtension` and
  `BankExtension` as well as `StargateClient.getAccountVerified` are deprecated
  and will be removed in 0.27 ([#910]).

[#910]: https://github.com/bitsongofficial/cosmjs-rn/pull/910

## [0.26.2] - 2021-10-12

### Fixed

- @cosmjs-rn/stargate: remove extra space in messageTimeout registry.
- @cosmjs-rn/cosmwasm-stargate: Fix Amino JSON representation of
  `MsgInstantiateContract`, `MsgMigrateContract` and `MsgExecuteContract` to
  match the wasmd expectation. This was broken since the wasmd upgrade to
  Stargate such that no Ledger signing was possible for those message types in
  the meantime.

## [0.26.1] - 2021-09-30

### Added

- @cosmjs-rn/amino: `decodeBech32Pubkey` and `decodeAminoPubkey` now support
  decoding multisig public keys ([#882]).

### Fixed

- @cosmjs-rn/stargate: Add missing pagination key arguments to query types in
  `GovExtension`.

[#882]: https://github.com/bitsongofficial/cosmjs-rn/issues/882

## [0.26.0] - 2021-08-24

### Added

- @cosmjs-rn/tendermint-rpc: `Tendermint34Client.blockSearch` and
  `Tendermint34Client.blockSearchAll` were added to allow searching blocks in
  Tendermint 0.34.9+ backends.
- @cosmjs-rn/tendermint-rpc: `Tendermint33Client` has been added to provide support
  for Tendermint v0.33.
- @cosmjs-rn/tendermint-rpc: Exports relating to `Tendermint33Client` are now
  available under `tendermint33`.
- @cosmjs-rn/proto-signing and @cosmjs-rn/stargate: Create a Stargate-ready
  `parseCoins` that replaces the `parseCoins` re-export from `@cosmjs-rn/amino`.
- @cosmjs-rn/cosmwasm-stargate: Export `isValidBuilder`, which is a clone of
  `isValidBuilder` from @cosmjs-rn/cosmwasm-launchpad.
- @cosmjs-rn/cosmwasm-stargate: Copy symbols `Code`, `CodeDetails`, `Contract`,
  `ContractCodeHistoryEntry` and `JsonObject` from @cosmjs-rn/cosmwasm-launchpad
  and remove dependency on @cosmjs-rn/cosmwasm-launchpad.
- @cosmjs-rn/faucet: Add new configuration variable `FAUCET_PATH_PATTERN` to
  configure the HD path of the faucet accounts ([#832]).
- @cosmjs-rn/cosmwasm-stargate: Add field `ibcPortId` to `Contract` ([#836]).
- @cosmjs-rn/stargate: Add `GovExtension` for query client.
- @cosmjs-rn/stargate: Add support for `MsgDeposit`, `MsgSubmitProposal` and
  `MsgVote`.

[#832]: https://github.com/bitsongofficial/cosmjs-rn/issues/832
[#836]: https://github.com/bitsongofficial/cosmjs-rn/issues/836

### Changed

- @cosmjs-rn/cosmwasm-launchpad: The `transferAmount` property on
  `InstantiateOptions` (accepted as a parameter to
  `SigningCosmWasmClient.instantiate`) has been renamed to `funds`.
- @cosmjs-rn/cosmwasm-stargate: The `transferAmount` property on
  `InstantiateOptions` (accepted as a parameter to
  `SigningCosmWasmClient.instantiate`) has been renamed to `funds`.
- @cosmjs-rn/cosmwasm-stargate: Default fee/gas values have been removed. Fees now
  need to be calculated and passed to `SigningCosmWasmClient` when calling any
  methods which submit transactions to the blockchain.
- @cosmjs-rn/stargate: Default fee/gas values have been removed. Fees now need to
  be calculated and passed to `SigningStargateClient` when calling any methods
  which submit transactions to the blockchain.
- @cosmjs-rn/tendermint-rpc: Make `tendermint34.Header.lastBlockId` and
  `tendermint34.Block.lastCommit` optional to better handle the case of height 1
  where there is no previous block.
- @cosmjs-rn/proto-signing: `makeAuthInfoBytes` now takes an array of pubkey
  sequence pairs in order to support different sequences for different signers.
- @cosmjs-rn/cosmwasm-stargate: Upgraded client to support wasmd 0.18 backends.
  Other backends are not supported anymore. Update proto types from
  `cosmwasm.wasm.v1beta1.*` to `cosmwasm.wasm.v1.*`. `MsgStoreCode.source` and
  `MsgStoreCode.builder` were removed; `MsgInstantiateContract.initMsg` and
  `MsgMigrateContract.migrateMsg` were renamed to `msg`; `Code.{source,builder}`
  and `CodeDetails.{source,builder}` were removed; `isValidBuilder` was removed;
  `UploadMeta` and the `meta` from `SigningCosmWasmClient.upload` were removed.
  ([#863])

[#863]: https://github.com/bitsongofficial/cosmjs-rn/pull/863

### Removed

- Node.js v10 is no longer supported. Please use v12 or later.
- @cosmjs-rn/cosmwasm-stargate: Remove `CosmWasmFeeTable` type and
  `defaultGasLimits` object.
- @cosmjs-rn/stargate: Remove types, objects and functions to do with default fees:
  `CosmosFeeTable`, `FeeTable`, `GasLimits`, `defaultGasLimits`,
  `defaultGasPrice` and `buildFeeTable`.
- @cosmjs-rn/tendermint-rpc: `Client` has been removed. Please use
  `Tendermint33Client` or `Tendermint34Client`, depending on your needs.
- @cosmjs-rn/cosmwasm: Package removed ([#786]).
- @cosmjs-rn/cosmwasm-launchpad: Package removed ([#786]).

[#786]: https://github.com/bitsongofficial/cosmjs-rn/issues/786

### Fixed

- @cosmjs-rn/socket: Upgrade dependency "ws" to version 7 to avoid potential
  security problems.

## [0.25.6] - 2021-07-26

### Fixed

- @cosmjs-rn/stargate: Fix types `AminoMsgTransfer` and `AminoHeight` as well as
  the encoding of `MsgTransfer` for Amino signing.

## [0.25.5] - 2021-06-23

### Added

- @cosmjs-rn/tendermint-rpc: `Tendermint34Client.blockSearch` and
  `Tendermint34Client.blockSearchAll` were added to allow searching blocks in
  Tendermint 0.34.9+ backends. This is a backport of [#815]. Note: Decoding
  blocks of height 1 is unsupported. This is fixed in [#815] and will be
  released as part of CosmJS 0.26.

[#815]: https://github.com/bitsongofficial/cosmjs-rn/pull/815

## [0.25.4] - 2021-05-31

### Fixed

- @cosmjs-rn/socket: Upgrade dependency "ws" to version 7 to avoid potential
  security problems.

## [0.25.3] - 2021-05-18

### Fixed

- @cosmjs-rn/cosmwasm-stargate, @cosmjs-rn/stargate: Fix error propagation in
  `CosmWasmClient.broadcastTx` and `StargateClient.broadcastTx` ([#800]). This
  bug was introduced with the switch from broadcast mode "commit" to "sync" in
  version 0.25.0.
- @cosmjs-rn/launchpad, @cosmjs-rn/stargate: Avoid the use of named capture groups in
  `GasPrice.fromString` to restore ES2017 compatibility and make the library
  work with Hermes ([#801]; thanks [@AlexBHarley]).
- @cosmjs-rn/launchpad: Adapt `GasPrice.fromString` denom pattern to Cosmos SDK
  0.39 rules: reduce denom length to 16 and allow digits in denom.
- @cosmjs-rn/stargate: Adapt `GasPrice.fromString` denom pattern to Cosmos SDK 0.42
  rules: allow lengths up to 128, allow upper case letters and digits.

[#800]: https://github.com/bitsongofficial/cosmjs-rn/issues/800
[#801]: https://github.com/bitsongofficial/cosmjs-rn/issues/801
[@alexbharley]: https://github.com/AlexBHarley

## [0.25.2] - 2021-05-11

### Added

- @cosmjs-rn/cosmwasm-stargate: Add `broadcastTimeoutMs` and
  `broadcastPollIntervalMs` options added to `SigningCosmWasmClientOptions`.
- @cosmjs-rn/proto-signing: Add `serialize` and `serializeWithEncryptionKey`
  methods to `DirectSecp256k1HdWallet`. Also add `deserialize` and
  `deserializeWithEncryptionKey` static methods.
- @cosmjs-rn/proto-signing: Export `extractKdfConfiguration` and `executeKdf`
  helper functions and `KdfConfiguration` type.
- @cosmjs-rn/proto-signing: Export `makeCosmoshubPath` helper.
- @cosmjs-rn/stargate: Export `makeCosmoshubPath` helper.
- @cosmjs-rn/stargate: Add `broadcastTimeoutMs` and `broadcastPollIntervalMs`
  options added to `SigningStargateClientOptions`.

## [0.25.1] - 2021-05-06

### Added

- @cosmjs-rn/cosmwasm-stargate: Export types `Code`, `CodeDetails`, `Contract`,
  `ContractCodeHistoryEntry` and `JsonObject` which are response types of
  `CosmWasmClient` methods. Export types `ChangeAdminResult`, `ExecuteResult`,
  `InstantiateOptions`, `InstantiateResult`, `MigrateResult`, `UploadMeta` and
  `UploadResult` which are argument or response types of `SigningCosmWasmClient`
  methods.

### Fixed

- @cosmjs-rn/cosmwasm-stargate: Use `CosmWasmFeeTable` instead of `CosmosFeeTable`
  in `SigningCosmWasmClientOptions`; export type `CosmWasmFeeTable`.
- @cosmjs-rn/amino, @cosmjs-rn/cli, @cosmjs-rn/ledger-amino, @cosmjs-rn/proto-signing: Fix
  runtime error caused by passing explicitly undefined options.

## [0.25.0] - 2021-05-05

### Added

- @cosmjs-rn/cosmwasm-launchpad: Expose `SigningCosmWasmClient.fees`.
- @cosmjs-rn/cosmwasm-stargate: Expose `SigningCosmWasmClient.fees` and
  `SigningCosmWasmClient.registry`.
- @cosmjs-rn/launchpad: Expose `SigningCosmosClient.fees`.
- @cosmjs-rn/stargate: Expose `SigningStargateClient.fees` and
  `SigningStargateClient.registry`.
- @cosmjs-rn/stargate: Add support for different account types in `accountFromAny`
  and `StargateClient`. Added `ModuleAccount` and vesting accounts
  `BaseVestingAccount`, `ContinuousVestingAccount`, `DelayedVestingAccount` and
  `PeriodicVestingAccount`.
- @cosmjs-rn/stargate: Add codecs for IBC channel tx, client query/tx, and
  connection tx, as well as Tendermint.
- @cosmjs-rn/stargate: Add support for IBC message types in
  `SigningStargateClient`.
- @cosmjs-rn/stargate: Added new `logs` export with all the functionality from
  @cosmjs-rn/launchpad.
- @cosmjs-rn/stargate: Added new `Coin`, `coin`, `coins` and `parseCoins` exports
  which have the same functionality as already existed in @cosmjs-rn/launchpad.
- @cosmjs-rn/amino: New package created that contains the shared amino signing
  functionality for @cosmjs-rn/launchpad and @cosmjs-rn/stargate.
- @cosmjs-rn/amino: Split public key interfaces into `Pubkey`, `SinglePubkey` and
  `Secp256k1Pubkey` where `Pubkey` is a generalization of the old `PubKey` that
  supported nested pubkeys for multisig. `SinglePubkey` is the old `PubKey` in
  which the `value` is a base64 encoded string. And `Secp256k1Pubkey` is a
  single secp256k1 pubkey.
- @cosmjs-rn/utils: The new `arrayContentStartsWith` works similar to
  `arrayContentEquals` but only checks the start of an array.
- @cosmjs-rn/proto-signing: Added new `Coin`, `coin`, `coins` and `parseCoins`
  exports which have the same functionality as already existed in
  @cosmjs-rn/launchpad.
- @cosmjs-rn/stargate: Add `SigningStargateClient.sign`, which allows you to create
  signed transactions without broadcasting them directly. The new type
  `SignerData` can be passed into `.sign` to skip querying account number,
  sequence and chain ID
- @cosmjs-rn/cosmwasm-stargate: Add `SigningCosmWasmClient.sign`, which allows you
  to create signed transactions without broadcasting them directly. The new type
  `SignerData` from @cosmjs-rn/stargate can be passed into `.sign` to skip querying
  account number, sequence and chain ID.
- @cosmjs-rn/stargate: Add constructor `SigningStargateClient.offline` which does
  not connect to Tendermint. This allows offline signing.
- @cosmjs-rn/stargate: Add `makeMultisignedTx` which allows you to assemble a
  transaction signed by a multisig account.
- @cosmjs-rn/stargate: Add `delegateTokens`, `undelegateTokens` and
  `withdrawRewards` methods to `SigningStargateClient`.
- @cosmjs-rn/stargate: Export `defaultGasLimits` and `defaultGasPrice`.
- @cosmjs-rn/cosmwasm-stargate: Export `defaultGasLimits`.
- @cosmjs-rn/stargate: `SigningStargateClient` constructor is now `protected`.
- @cosmjs-rn/cosmwasm-stargate: `SigningCosmWasmClient` constructor is now
  `protected`.
- @cosmjs-rn/cosmwasm-stargate: Add `SigningCosmWasmClient.offline` static method
  for constructing offline clients without a Tendermint client.
- @cosmjs-rn/stargate: Add `SigningStargateClient.sendIbcTokens` method.
- @cosmjs-rn/amino: Export `Secp256k1HdWalletOptions` interface.
- @cosmjs-rn/amino: Add `bip39Password` option to `Secp256k1HdWallet` options.
- @cosmjs-rn/proto-signing: Export `DirectSecp256k1HdWalletOptions` interface.
- @cosmjs-rn/proto-signing: Add `bip39Password` option to `DirectSecp256k1HdWallet`
  options.
- @cosmjs-rn/amino: Add `rawEd25519PubkeyToRawAddress` helper function.
- @cosmjs-rn/tendermint-rpc: Add `pubkeyToAddress`, `pubkeyToRawAddress`,
  `rawEd25519PubkeyToRawAddress`, and `rawSecp256k1PubkeyToRawAddress` helper
  functions.
- @cosmjs-rn/stargate: `StargateClient.broadcastTx` and `.getTx` results now
  include `gasUsed` and `gasWanted` properties.
- @cosmjs-rn/cosmwasm-stargate: `CosmWasmClient.broadcastTx` and `.getTx` results
  now include `gasUsed` and `gasWanted` properties.
- @cosmjs-rn/proto-signing: Export `DecodeObject` and `TxBodyEncodeObject`
  interfaces as well as `isTxBodyEncodeObject` helper function.
- @cosmjs-rn/stargate: Add `MsgDelegateEncodeObject`, `MsgSendEncodeObject`,
  `MsgTransferEncodeObject`, `MsgUndelegateEncodeObject` and
  `MsgWithdrawDelegatorRewardEncodeObject` interfaces as well as
  `isMsgDelegateEncodeObject` etc helpers.
- @cosmjs-rn/cosmwasm-stargate: Add `MsgClearAdminEncodeObject`,
  `MsgExecuteContractEncodeObject`, `MsgInstantiateContractEncodeObject`,
  `MsgMigrateContractEncodeObject`, `MsgStoreCodeEncodeObject` and
  `MsgUpdateAdminEncodeObject` interfaces as well as
  `isMsgClearAdminEncodeObject` etc helpers.
- @cosmjs-rn/stargate: Add transfer queries codec, as well as transfer query
  methods to IBC query extension.
- @cosmjs-rn/tendermint-rpc: Export `ValidatorSecp256k1Pubkey` interface.
- @cosmjs-rn/proto-signing: Add transaction decoder `decodeTxRaw` for decoding
  transaction bytes returned by Tendermint (e.g. in `IndexedTx.tx`).

### Changed

- @cosmjs-rn/cosmwasm-stargate: Codec adapted to support wasmd 0.16. Older versions
  of wasmd are not supported anymore.
- @cosmjs-rn/stargate: Let `AuthExtension.account` and
  `AuthExtension.unverified.account` return an account of type `Any`. This makes
  the caller responsible for decoding the type.
- @cosmjs-rn/stargate: Remove `accountFromProto` in favour of `accountFromAny`.
- @cosmjs-rn/stargate: Rename `Rpc` interface to `ProtobufRpcClient` and
  `createRpc` to `createProtobufRpcClient`.
- @cosmjs-rn/stargate: Reorganize nesting structure of IBC query client and add
  support for more methods.
- @cosmjs-rn/tendermint-rpc: The fields `CommitSignature.validatorAddress`,
  `.timestamp` and `.signature` are now optional. They are unset when
  `blockIdFlag` is `BlockIdFlag.Absent`. The decoding into `CommitSignature` is
  only updated for the class `Tendermint34Client`, not for `Client`. Please
  migrate to the former.
- @cosmjs-rn/launchpad: `rawSecp256k1PubkeyToAddress` was removed. Instead use
  `Bech32.encode(prefix, rawSecp256k1PubkeyToRawAddress(pubkeyRaw))` with
  `rawSecp256k1PubkeyToRawAddress` from @cosmjs-rn/amino.
- @cosmjs-rn/stargate: `parseRawLog` is now nested under the `logs` export.
- @cosmjs-rn/stargate: Query extensions now have unverified queries at the root and
  verified queries nested under `.verified`.
- @cosmjs-rn/cosmwasm-stargate: `wasm` extension now has unverified queries at the
  root.
- @cosmjs-rn/stargate: `StargateClient.getAccount` now uses an unverified query and
  `StargateClient.getAccountUnverified` has been removed.
  `StargateClient.getAccountVerified` has been added, which performs a verified
  query.
- @cosmjs-rn/cosmwasm-stargate: `CosmWasmClient.getAccount` now uses an unverified
  query and `CosmWasmClient.getAccountUnverified` has been removed.
  `CosmWasmClient.getAccountVerified` has been added, which performs a verified
  query.
- @cosmjs-rn/stargate: `StargateClient.getSequence` now rejects if the account is
  not found, instead of returning null.
- @cosmjs-rn/stargate: `StargateClient.getBalance` now returns a 0 balance instead
  of null.
- @cosmjs-rn/stargate: `StargateClient.getAllBalancesUnverified` has been renamed
  `.getAllBalances`.
- @cosmjs-rn/cosmwasm-stargate: `CosmWasmClient.getSequence` now rejects if the
  account is not found, instead of returning null.
- @cosmjs-rn/cosmwasm-stargate: `CosmWasmClient.getBalance` now returns a 0 balance
  instead of null.
- @cosmjs-rn/amino: Options for `Secp256k1HdWallet.fromMnemonic` are now passed via
  a `Secp256k1HdWalletOptions` object.
- @cosmjs-rn/proto-signing: Options for `DirectSecp256k1HdWallet.fromMnemonic` are
  now passed via a `DirectSecp256k1HdWalletOptions` object.
- @cosmjs-rn/stargate: `StargateClient.broadcastTx` now uses sync mode and then
  polls for the transaction before resolving. The timeout and poll interval can
  be configured.
- @cosmjs-rn/cosmwasm-stargate: `CosmWasmClient.broadcastTx` now uses sync mode and
  then polls for the transaction before resolving. The timeout and poll interval
  can be configured.
- @cosmjs-rn/tendermint-rpc: Tendermint v34 `TxData` type now includes `codeSpace`,
  `gasWanted`, and `gasUsed` properties.
- @cosmjs-rn/amino: `Secp256k1HdWallet.fromMnemonic` now accepts a
  `Secp256k1HdWalletOptions` argument which includes an array of `hdPaths`
  instead of a single `hdPath`. `Secp256k1HdWallet.generate` now also accepts
  options via this interface. This adds support for multiple accounts from the
  same mnemonic to `Secp256k1HdWallet`.
- @cosmjs-rn/proto-signing: `DirectSecp256k1HdWallet.fromMnemonic` now accepts a
  `DirectSecp256k1HdWalletOptions` argument which includes an array of `hdPaths`
  instead of a single `hdPath`. `DirectSecp256k1HdWallet.generate` now also
  accepts options via this interface. This adds support for multiple accounts
  from the same mnemonic to `DirectSecp256k1HdWallet`.
- @cosmjs-rn/tendermint-rpc: `ValidatorPubkey` is now a union of
  `ValidatorEd25519Pubkey` and the newly exported `ValidatorSecp256k1Pubkey`
  interface.
- @cosmjs-rn/tendermint-rpc: `decodePubkey` now supports secp256k1 public keys.

### Deprecated

- @cosmjs-rn/tendermint-rpc: `Client` has been deprecated. Launchpad applications
  do not need a Tendermint RPC client and Stargate applications should use
  `Tendermint34Client`.

### Removed

- @cosmjs-rn/stargate: `coinFromProto` helper has been removed as it is no longer
  needed after the `ts-proto` migration.

## [0.24.1] - 2021-03-12

CHANGELOG entries missing. Please see [the diff][0.24.1].

## [0.24.0] - 2021-03-11

- @cosmjs-rn/cosmwasm: This package is now deprecated. The same functionality is
  now available in @cosmjs-rn/cosmwasm-launchpad.
- @cosmjs-rn/cosmwasm: `logs` is no longer exported. Use `logs` from
  @cosmjs-rn/launchpad instead.
- @cosmjs-rn/cosmwasm: Export `JsonObject`, `ChangeAdminResult` and `WasmData`
  types as well as `isValidBuilder` and `parseWasmData` functions.
- @cosmjs-rn/cosmwasm: Add `CosmWasmClient.getTx` method for searching by ID and
  remove such functionality from `CosmWasmClient.searchTx`.
- @cosmjs-rn/cosmwasm: Rename `SigningCosmWasmClient.senderAddress` to
  `.signerAddress`.
- @cosmjs-rn/cosmwasm-stargate: Add new package for CosmWasm Stargate support.
- @cosmjs-rn/crypto: Change `Secp256k1Keypair` from tagged type to simple
  interface.
- @cosmjs-rn/launchpad: Add `Secp256k1Wallet` to manage a single raw secp256k1
  keypair.
- @cosmjs-rn/launchpad: `OfflineSigner` type’s `sign` method renamed `signAmino`
  and `SignResponse` type renamed `AminoSignResponse`.
- @cosmjs-rn/launchpad: `Secp256k1HdWallet.sign` method renamed `signAmino`.
- @cosmjs-rn/launchpad: Add `CosmosClient.getTx` method for searching by ID and
  remove such functionality from `CosmosClient.searchTx`.
- @cosmjs-rn/launchpad: Add `SigningCosmosClient.sign` method for signing without
  broadcasting.
- @cosmjs-rn/launchpad: Add `SigningCosmosClient.appendSignature` method creating
  transactions with multiple signatures.
- @cosmjs-rn/launchpad: Add support for undefined memo in `makeSignDoc`.
- @cosmjs-rn/launchpad: Rename `SigningCosmosClient.senderAddress` to
  `.signerAddress`.
- @cosmjs-rn/proto-signing: Add new package for handling transaction signing with
  protobuf encoding.
- @cosmjs-rn/proto-signing: Expose `DirectSignResponse` interface.
- @cosmjs-rn/stargate: Add new package for Cosmos SDK Stargate support.
- @cosmjs-rn/tendermint-rpc: Make `Client.detectVersion` private and let it return
  a version instead of a client.
- @cosmjs-rn/tendermint-rpc: Make the constructor of `Client` private. Add
  `Client.create` for creating a Tendermint client given an RPC client and an
  optional adaptor.
- @cosmjs-rn/tendermint-rpc: Add an optional adaptor argument to `Client.connect`
  which allows skipping the auto-detection.
- @cosmjs-rn/tendermint-rpc: Remove export `v0_33` in favour of `adaptor33` and
  `adaptor34`. Export the `Adaptor` type.
- @cosmjs-rn/tendermint-rpc: Export `DateTime` class.
- @cosmjs-rn/tendermint-rpc: Remove types `QueryString`, `Base64String`,
  `HexString`, `IntegerString` and `IpPortString`. Use `string` instead.
- @cosmjs-rn/tendermint-rpc: Remove types `BlockHash`, `TxBytes` and `TxHash`. Use
  `Uint8Array` instead.

### Added

- @cosmjs-rn/launchpad: Export distribution module msg types
  `MsgFundCommunityPool`, `MsgSetWithdrawAddress`, `MsgWithdrawDelegatorReward`,
  `MsgWithdrawValidatorCommission` and type checker helper functions.
- @cosmjs-rn/utils: Added `assertDefinedAndNotNull`.
- @cosmjs-rn/tendermint-rpc: The new `Tendermint34Client` is a copy of the old
  `Client` but without the automatic version detection. Its usage is encouraged
  over `Client` if you connect to a Tendermint 0.34 backend.

### Changed

- @cosmjs-rn/encoding: Change return type of `fromRfc3339` from `ReadonlyDate` to
  `Date` as the caller becomes the owner of the object and can safely mutate it
  in any way.
- @cosmjs-rn/launchpad-ledger: Renamed to @cosmjs-rn/ledger-amino.
- @cosmjs-rn/ledger-amino: `LedgerSigner.sign` method renamed `signAmino`.

### Deprecated

- @cosmjs-rn/tendermint-rpc: Deprecate `DateTime` in favour of the free functions
  `fromRfc3339WithNanoseconds` and `toRfc3339WithNanoseconds`.

## 0.23.2 (2021-01-06)

### Security

- @cosmjs-rn/cli: Update vulnerable axios dependency.
- @cosmjs-rn/faucet-client: Update vulnerable axios dependency.
- @cosmjs-rn/launchpad: Update vulnerable axios dependency.
- @cosmjs-rn/tendermint-rpc: Update vulnerable axios dependency.

## 0.23.1 (2020-10-27)

- @cosmjs-rn/crypto: Export new convenience functions `keccak256`, `ripemd160`,
  `sha1`, `sha256` and `sha512`.
- @cosmjs-rn/faucet-client: Add new package which exports `FaucetClient` class.

## 0.23.0 (2020-10-09)

- @cosmjs-rn/cli: Expose `HdPath` type.
- @cosmjs-rn/cosmwasm: Rename `CosmWasmClient.postTx` method to `.broadcastTx`.
- @cosmjs-rn/cosmwasm: Rename `FeeTable` type to `CosmWasmFeeTable`.
- @cosmjs-rn/cosmwasm: `SigningCosmWasmClient` constructor now takes optional
  arguments `gasPrice` and `gasLimits` instead of `customFees` for easier
  customization.
- @cosmjs-rn/cosmwasm: Rename `SigningCosmWasmClient.signAndPost` method to
  `.signAndBroadcast`.
- @cosmjs-rn/cosmwasm: Use stricter type `Record<string, unknown>` for smart query,
  init, migrate and handle messages (in `WasmExtension.wasm.queryContractSmart`,
  `CosmWasmClient.queryContractSmart`, `SigningCosmWasmClient.instantiate`,
  `SigningCosmWasmClient.migrate`, `SigningCosmWasmClient.execute`).
- @cosmjs-rn/crypto: Export new type alias `HdPath`.
- @cosmjs-rn/crypto: Add `Secp256k1Signature.toFixedLength` method.
- @cosmjs-rn/demo-staking: Remove package and supporting scripts.
- @cosmjs-rn/encoding: Add `limit` parameter to `Bech32.encode` and `.decode`. The
  new default limit for decoding is infinity (was 90 before). Set it to 90 to
  create a strict decoder.
- @cosmjs-rn/faucet: Environmental variable `FAUCET_FEE` renamed to
  `FAUCET_GAS_PRICE` and now only accepts one token. Environmental variable
  `FAUCET_GAS` renamed to `FAUCET_GAS_LIMIT`.
- @cosmjs-rn/faucet: `/credit` API now expects `denom` (base token) instead of
  `ticker` (unit token). Environmental variables specifying credit amounts now
  need to use uppercase denom.
- @cosmjs-rn/launchpad: Rename `FeeTable` type to `CosmosFeeTable` and export a new
  more generic type `FeeTable`.
- @cosmjs-rn/launchpad: Add new class `GasPrice`, new helper type `GasLimits` and
  new helper function `buildFeeTable` for easier handling of gas prices and
  fees.
- @cosmjs-rn/launchpad: Rename `CosmosClient.postTx` method to `.broadcastTx`.
- @cosmjs-rn/launchpad: `SigningCosmosClient` constructor now takes optional
  arguments `gasPrice` and `gasLimits` instead of `customFees` for easier
  customization.
- @cosmjs-rn/launchpad: Rename `SigningCosmosClient.signAndPost` method to
  `.signAndBroadcast`.
- @cosmjs-rn/launchpad: Rename `PostTx`-related types to `BroadcastTxResult`,
  `BroadcastTxSuccess` and `BroadcastTxFailure` respectively, as well as helper
  functions `isBroadcastTxFailure`, `isBroadcastTxSuccess` and
  `assertIsBroadcastTxSuccess`.
- @cosmjs-rn/launchpad: Export `isSearchByIdQuery`, `isSearchByHeightQuery`,
  `isSearchBySentFromOrToQuery` and `isSearchByTagsQuery`.
- @cosmjs-rn/launchpad: Change type of `TxsResponse.logs` and
  `BroadcastTxsResponse.logs` to `unknown[]`.
- @cosmjs-rn/launchpad: Export `StdSignDoc` and create helpers to make and
  serialize a `StdSignDoc`: `makeSignDoc` and `serializeSignDoc`.
- @cosmjs-rn/launchpad: Let `OfflineSigner.sign` take an `StdSignDoc` instead of an
  encoded message and return a `SignResponse` that includes the document which
  was signed.
- @cosmjs-rn/launchpad: Remove `PrehashType` and the prehash type argument in
  `OfflineSigner.sign` because the signer now needs to know how to serialize an
  `StdSignDoc`.
- @cosmjs-rn/launchpad: Remove `makeSignBytes` in favour of `makeSignDoc` and
  `serializeSignDoc`.
- @cosmjs-rn/launchpad: Create `WrappedTx`, `WrappedStdTx` and `isWrappedStdTx` to
  better represent the Amino tx interface. Deprecate `CosmosSdkTx`, which is an
  alias for `WrappedStdTx`.
- @cosmjs-rn/launchpad: Add `makeStdTx` to create an `StdTx`.
- @cosmjs-rn/launchpad: Rename `Secp256k1Wallet` to `Secp256k1HdWallet`. Later on,
  we'll use `Secp256k1Wallet` for single key wallets.
- @cosmjs-rn/launchpad-ledger: Add package supporting Ledger device integration for
  Launchpad. Two new classes are provided: `LedgerSigner` (for most use cases)
  and `LaunchpadLedger` for more fine-grained access.
- @cosmjs-rn/math: Add `.multiply` method to `Decimal` class.
- @cosmjs-rn/math: Deprecate `Uint32.fromBigEndianBytes` in favour of
  `Uint32.fromBytes`, which supports both big and little endian.
- @cosmjs-rn/math: Deprecate `Uint64.fromBytesBigEndian` in favour of
  `Uint64.fromBytes`, which supports both big and little endian.
- @cosmjs-rn/math: Add `Uint32.fromString`.
- @cosmjs-rn/tendermint-rpc: Make `BroadcastTxCommitResponse.height` non-optional.
- @cosmjs-rn/tendermint-rpc: Make `TxProof.proof.leafHash` non-optional because it
  is always set.
- @cosmjs-rn/tendermint-rpc: Change type of `GenesisResponse.appState` to
  `Record<string, unknown> | undefined`.
- @cosmjs-rn/tendermint-rpc: Remove obsolete `TxData.tags` and make `TxData.events`
  non-optional. Rename `Tag` to `Attribute`.
- @cosmjs-rn/tendermint-rpc: Remove obsolete `BlockResultsResponse.beginBlock` and
  `.beginBlock`. The new `.beginBlockEvents` and `.endBlockEvents` now parse the
  events correctly.
- @cosmjs-rn/tendermint-rpc: Remove trivial helpers `getTxEventHeight`,
  `getHeaderEventHeight` and `getBlockEventHeight` because they don't do
  anything else than accessing an object member.
- @cosmjs-rn/tendermint-rpc: Add support for connecting to Tendermint RPC 0.34.
- @cosmjs-rn/tendermint-rpc: Make `TxEvent.index` optional and deprecate it because
  it is not set anymore in Tendermint 0.34.
- @cosmjs-rn/utils: Add `assertDefined`.
- @cosmjs-rn/faucet: Rename binary from `cosmwasm-faucet` to `cosmos-faucet`.

## 0.22.3 (2020-09-15)

- @cosmjs-rn/math: Add `Decimal.minus`.

## 0.22.2 (2020-08-11)

- @cosmjs-rn/faucet: Log errors for failed send transactions.
- @cosmjs-rn/faucet: Add config variable `FAUCET_MEMO`.
- @cosmjs-rn/faucet: Add config variables `FAUCET_FEE` and `FAUCET_GAS`.
- @cosmjs-rn/launchpad: Add `parseCoins` helper.

## 0.22.1 (2020-08-11)

- @cosmjs-rn/cli: Import `encodeAminoPubkey`, `encodeBech32Pubkey`,
  `decodeAminoPubkey` and `decodeBech32Pubkey` by default.
- @cosmjs-rn/launchpad: Add ed25519 support to `encodeBech32Pubkey`.
- @cosmjs-rn/launchpad: Add `encodeAminoPubkey` and `decodeAminoPubkey`.
- @cosmjs-rn/utils: Add `arrayContentEquals`.
- @cosmjs-rn/faucet: Add config variables `FAUCET_ADDRESS_PREFIX` and
  `FAUCET_TOKENS`.
- @cosmjs-rn/faucet: Remove broken chain ID from `cosmwasm-faucet generate`.

## 0.22.0 (2020-08-03)

- @cosmjs-rn/cli: Now supports HTTPs URLs for `--init` code sources.
- @cosmjs-rn/cli: Now supports adding code directly via `--code`.
- @cosmjs-rn/cosmwasm: Rename `CosmWasmClient.getNonce` method to `.getSequence`.
- @cosmjs-rn/cosmwasm: Remove `RestClient` class in favour of new modular
  `LcdClient` class from @cosmjs-rn/sdk38.
- @cosmjs-rn/cosmwasm: Add `SigningCosmWasmClient.signAndPost` as a mid-level
  abstraction between `SigningCosmWasmClient.upload`/`.instantiate`/`.execute`
  and `.postTx`.
- @cosmjs-rn/cosmwasm: Use `*PostTx*` types and helpers from @cosmjs-rn/sdk38. Remove
  exported `PostTxResult`.
- @cosmjs-rn/cosmwasm: `ContractDetails` was removed in favour of just `Contract`.
  The missing `init_msg` is now available via the contract's code history (see
  `getContractCodeHistory`).
- @cosmjs-rn/cosmwasm: Remove `SigningCallback` in favour of the `OfflineSigner`
  interface.
- @cosmjs-rn/sdk38: Rename `CosmosClient.getNonce` method to `.getSequence`.
- @cosmjs-rn/sdk38: Remove `RestClient` class in favour of new modular `LcdClient`
  class.
- @cosmjs-rn/sdk38: Remove `Pen` type in favour of `OfflineSigner` and remove
  `Secp256k1Pen` class in favour of `Secp256k1Wallet` which takes an
  `OfflineSigner` instead of a `SigningCallback`.
- @cosmjs-rn/sdk38: Rename `CosmosSdkAccount` to `BaseAccount` and export the type.
- @cosmjs-rn/sdk38: `BaseAccount` now uses `number | string` as the type for
  `account_number` and `sequence`. The new helpers `uint64ToNumber` and
  `uint64ToString` allow you to normalize the mixed input.
- @cosmjs-rn/sdk38: `BaseAccount` now uses `string | PubKey | null` as the type for
  `public_key`. The new helper `normalizePubkey` allows you to normalize the
  mixed input.
- @cosmjs-rn/math: Add missing integer check to `Uint64.fromNumber`. Before
  `Uint64.fromNumber(1.1)` produced some result.
- @cosmjs-rn/sdk38: Add `SigningCosmosClient.signAndPost` as a mid-level
  abstraction between `SigningCosmosClient.sendTokens` and `.postTx`.
- @cosmjs-rn/sdk38: Export `PostTxFailure`/`PostTxSuccess` and type checkers
  `isPostTxFailure`/`isPostTxSuccess`; export `assertIsPostTxSuccess`.
- @cosmjs-rn/sdk38: `Secp256k1Wallet`s can now be generated randomly with
  `Secp256k1Wallet.generate(n)` where `n` is 12, 15, 18, 21 or 24 mnemonic
  words.
- @cosmjs-rn/sdk38: The new `Secp256k1Wallet.serialize` and `.deserialize` allow
  encrypted serialization of the wallet.
- @cosmjs-rn/sdk38: Remove the obsolete `upload`, `init`, `exec` properties from
  `FeeTable`. @cosmjs-rn/cosmwasm has its own `FeeTable` with those properties.
- @cosmjs-rn/sdk38: Rename package to @cosmjs-rn/launchpad.

[unreleased]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.27.1...HEAD
[0.27.1]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.27.0...v0.27.1
[0.27.0]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.26.6...v0.27.0
[0.26.6]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.26.5...v0.26.6
[0.26.5]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.26.4...v0.26.5
[0.26.4]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.26.3...v0.26.4
[0.26.3]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.26.2...v0.26.3
[0.26.2]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.26.1...v0.26.2
[0.26.1]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.26.0...v0.26.1
[0.26.0]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.25.6...v0.26.0
[0.25.6]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.25.5...v0.25.6
[0.25.5]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.25.4...v0.25.5
[0.25.4]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.25.3...v0.25.4
[0.25.3]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.25.2...v0.25.3
[0.25.2]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.25.1...v0.25.2
[0.25.1]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.25.0...v0.25.1
[0.25.0]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.24.1...v0.25.0
[0.24.1]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.24.0...v0.24.1
[0.24.0]: https://github.com/bitsongofficial/cosmjs-rn/compare/v0.23.0...v0.24.0
