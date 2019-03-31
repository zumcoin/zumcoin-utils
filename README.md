<p align="center"><img src="https://raw.githubusercontent.com/zumcoin/zum-assets/master/ZumCoin/zumcoin_logo_design/3d_green_lite_bg/ZumLogo_800x200px_lite_bg.png" width="400"></p><br><br>

[![NPM](https://nodei.co/npm/zumcoin-utils.png?downloads=true&stars=true)](https://nodei.co/npm/zumcoin-utils/)

#### Master Build Status
[![Build Status](https://travis-ci.org/zumcoin/zumcoin-utils.svg?branch=master)](https://travis-ci.org/zumcoin/zumcoin-utils)

# ZumCoin Javascript Utilities

## Disclaimer

***Use of this code in its current state may lead to unexpected results***

This repository contains highly experimental code  with the goal of making it possible to interact with a daemon including wallet functionaity (sending/receiving transactions) without the need for `zum-service` or `wallet-api` using Node.js. By using the code in this repo, you understand that some functions may not work, others may work but be untested, while others may upset you.

The best way to address such situations is to submit a Pull Request to resolve the issue you're running into.

## Installation

```bash
npm i git+https://github.com/zumcoin/zumcoin-utils
```

## Initialization

### JavaScript

```javascript
const ZumCoinUtils = require('zumcoin-utils').CryptoNote
const coinUtils = new ZumCoinUtils()
```

### TypeScript

```typescript
import { CryptoNote } from 'zumcoin-utils'
const coinUtils = new CryptoNote()
```

You can find TypeScript type definitions [here](index.d.ts)


## Public Methods

#### createNewSeed([entropy], [iterations])

Creates a new address seed using the provided entropy or if entropy is undefined, uses a randomly selected entropy source.

#### createNewAddress([entropy], [language], [addressPrefix])

Creates a new [address](#address) using the provided entropy, language (for the mnemonic), and address prefix if supplied.

#### createAddressFromSeed(seed, [language], [addressPrefix])

Creates a new [address](#address) using the provided seed, language (for the mnemonic), and address prefix if supplied.

#### createAddressFromMnemonic(mnemonic, [language], [addressPrefix])

Creates a new [address](#address) using the provided mnemonic, language (for the mnemonic), and address prefix if supplied.

#### createAddressFromKeys(privateSpendKey, privateViewKey, [addressPrefix])

Creates a new [address](#address) using the provided private spend key, private view key, and address prefix if supplied.

#### decodeAddressPrefix(address)

Decodes the [address prefix](#decoded-address-prefix) from the specified CryptoNote public address.

#### decodeAddress(address, [addressPrefix])

Decodes the address into the public key pairs, prefix, payment ID, etc. Returns a [decoded address](#decoded-address) object.

#### encodeRawAddress(rawAddress)

Encodes the rawAddress using CN-Base58 encoding.

#### encodeAddress(publicViewKey, publicSpendKey, [paymentId], [addressPrefix])

Encodes the publicViewKey, publicSpendKey, and payment ID into a standard CryptoNote address (or Integrated address if payment ID is supplied)

#### createIntegratedAddress(address, paymentId, [addressPrefix])

Creates an Integrated Address using the supplied address and payment ID.

#### privateKeyToPublicKey(privateKey)

Gets the corresponding private key from the given public key.

#### scanTransactionOutputs(transactionPublicKey, outputs, privateViewKey, publicSpendKey, [privateSpendKey])

*Documentation In Progress*

#### isOurTransactionOutput(transactionPublicKey, output, privateViewKey, publicSpendKey, [privateSpendKey])

*Documentation In Progress*

#### generateKeyImage(transactionPublicKey, privateViewKey, publicSpendKey, privateSpendKey, outputIndex)

*Documentation In Progress*

#### generateKeyImagePrimative(publicSpendKey, privateSpendKey, outputIndex, derivation)

The same as generateKeyImage, but allows you to reuse a derivation you have previously created, instead of re-deriving it. Returns [keyImage, privateEphemeral].

#### createTransaction(transfers, ourOutputs, randomOuts, mixin, feeAmount, [paymentId], [unlockTime])

*Documentation In Progress*

#### createTransactionAsync(transfers, ourOutputs, randomOuts, mixin, feeAmount, [paymentId], [unlockTime])

Functions as `createTransaction`, but runs asynchronously, and additionaly, supports user provided async functions.
The regular code only supports synchronous provided funcs, so ensure any async user provided functions are not being used in other calls you make.

#### serializeTransaction(transaction)

*Documentation In Progress*

#### generateKeyDerivation(transactionPublicKey, privateViewKey)

Creates the key 'derivation' given a transaction public key, and the private view key.
Can then be supplied to underivePublicKey, to determine if the transaction output belongs to you.
Returns a string.

#### underivePublicKey(derivation, outputIndex, outputKey)

Given the output index in the transaction, and the outputs key, along with a
derivation from `generateKeyDerivation`, this method will return a public spend key.
If the public spend key matches your public spend key, the transaction output is yours.
Returns a string.

## Common Data Structures

#### Address

```javascript
{ spend:
   { privateKey: '6768d7d4a3a8b07f8f5f102c2eeef2f060dfbcdb882d2e548ac030ab486e7f0a',
     publicKey: 'c8953c45c0e7f1b1253d6ff16a6f62c7bbb87389139abee07aa4627ca0219321' },

  view:
   { privateKey: '9619bc6482ad14fdba4a55e1a9da01f9535ceebda0ae71218b15cde14c0b870c',
     publicKey: '1ff2b174c8d0df2e26bc965e8c9424eb9564d5e65592b0e0ffcea9937518cb41' },

  address: 'Zum1ykEo4JYZGRx2f6W5cUJoZ81B4fCcp4HBuKLNCmq5TnURMK9UMxwabAcsSJdyPsQWnnTAUWZ7sFKAbRMYVEz6LazCNn5wn49',

  mnemonic: 'gables vivid sieve somewhere avoid nobody vein movement rhythm cottage cistern banjo joyous tawny rage textbook aimless guru maps tell lukewarm adjust oven point tawny',
  seed: null }
```

#### Decoded Address

```javascript
{ publicViewKey: '1ff2b174c8d0df2e26bc965e8c9424eb9564d5e65592b0e0ffcea9937518cb41',
  publicSpendKey: 'c8953c45c0e7f1b1253d6ff16a6f62c7bbb87389139abee07aa4627ca0219321',
  paymentId: '',
  encodedPrefix: 'c4c0fd01',
  prefix: 4153412,
  rawAddress: 'c4c0fd01c8953c45c0e7f1b1253d6ff16a6f62c7bbb87389139abee07aa4627ca02193211ff2b174c8d0df2e26bc965e8c9424eb9564d5e65592b0e0ffcea9937518cb4106296b9a' }
```

#### Decoded Address Prefix

```javascript
{ prefix: 'c4c0fd01',
  base58: 'Zum1',
  decimal: 4153412,
  hexadecimal: '3f6044' }
```

### Credits

Special thanks goes out to:

* Lucas Jones
* Paul Shapiro
* Luigi111
* [The MyMonero Project](https://github.com/mymonero/mymonero-app-js)
* The Masari Project: [gnock](https://github.com/gnock)
* The Plentum Project: [DaveLong](https://github.com/DaveLong)
