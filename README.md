hasher-meowpow
==========

This is a Node module for simple hashing and verifying inputs using the
MeowPOW proof-of-work algorithm as implemented by [Ravencoin](https://github.com/RavenProject/Ravencoin/releases/tag/v4.0.0). 
Most of the native code comes from or is adapted from [Ravencoin code](https://github.com/RavenProject/Ravencoin).



## Install ##
__Install as Dependency in NodeJS Project__
```bash
# Install from Github git package

sudo apt-get install build-essential
npm install zachchan105/hasher-meowpow --save
```
-or-
```bash
# Install from Github NPM repository

sudo apt-get install build-essential
npm config set @zachchan105:registry https://npm.pkg.github.com/zachchan105
npm config set //npm.pkg.github.com/:_authToken <MY_GITHUB_AUTH_TOKEN>

npm install @zachchan105/hasher-meowpow@1.0.0 --save
```

__Install & Test__
```bash
# Install nodejs v10
curl -sL https://deb.nodesource.com/setup_10.x | sudo -E bash -
sudo apt-get install nodejs -y

# Download hasher-meowpow
git clone https://github.com/MintPond/hasher-meowpow

# build
cd hasher-meowpow
sudo apt-get install build-essential
npm install

# test
npm test
``` 

## Usage ##
__Hash__
```javascript
const meowpow = require('@zachchan105/hasher-meowpow');

const mixOutBuf = Buffer.alloc(32);
const hashOutBuf = Buffer.alloc(32);

/**
 * Hash using a single nonce and place results into the specified output Buffers.
 *
 * Note that all input values are expected to be in little-endian format.
 *
 * All output values are in little endian format
 *
 * @param headerHashBuf {Buffer} 32-byte header hash
 * @param nonceBuf {Buffer} 8-byte nonce value (64-bits)
 * @param blockHeight {number} Block height integer
 * @param mixOutBuf {Buffer} Mix hash result output Buffer
 * @param hashOutBuf {Buffer} Hash result output Buffer
 */
meowpow.hashOne(headerHashBuf, nonceBuf, blockHeight, mixOutBuf, hashOutBuf);

console.log(mixHashBuf.toString('hex'));
console.log(hashOutBuf.toString('hex'));

```

__Verify__
```javascript
const meowpow = require('@zachchan105/hasher-meowpow');

const hashValueOut = Buffer.alloc(32);

/**
 * Verify a mix hash.
 *
 * Note that all input values are expected to be in little-endian format.
 *
 * All output values are in little endian format.
 *
 * @param headerHashBuf {Buffer} 32-byte header hash
 * @param nonceBuf {Buffer} 8-byte nonce value (64-bits)
 * @param blockHeight {number} Block height integer
 * @param mixHashBuf {Buffer} Mix hash for verification
 * @param hashOutBuf {Buffer} Hash result output Buffer
 * @returns {boolean} True if valid, otherwise false.
 */
const isValid = meowpow.verify(headerHashBuf, nonceBuf, blockHeight, mixHashBuf, hashValueOut);

if (isValid) {
    console.log(hashValueOut.toString('hex'));
}
else {
    console.log('Invalid');
}
```

## Dependencies ##
In Ubuntu:
```
   sudo apt-get install build-essential
```