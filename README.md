# iltorb

[![NPM Version][npm-badge]][npm-url]
[![Travis Build Status][travis-badge]][travis-url]
[![AppVeyor Build Status][appveyor-badge]][appveyor-url]
[![CircleCI Build Status][circleci-badge]][circleci-url]

[iltorb](https://www.npmjs.com/package/iltorb) is a [Node.js](https://nodejs.org) package offering native bindings for the [brotli](https://github.com/google/brotli) compression library.

## Install

This module uses `prebuild` to download a pre-compiled binary for your platform, if it exists. Otherwise, it will use `node-gyp` to build the module.

```
npm install iltorb
```

### Prerequisites for Building

The following is required to build from source or when a [pre-compiled binary](https://github.com/MayhemYDG/iltorb/releases) does not exist.

- Python 2.7
- GCC 4.8+ (Unix) or [windows-build-tools](https://github.com/felixrieseberg/windows-build-tools) (Windows), see [Node Building tools](https://github.com/nodejs/node-gyp#installation).

## Methods

### Async

#### compress(buffer[, brotliEncodeParams], callback)

```javascript
const compress = require('iltorb').compress;

compress(input, function(err, output) {
  // ...
});
```

#### decompress(buffer, callback)

```javascript
const decompress = require('iltorb').decompress;

decompress(input, function(err, output) {
  // ...
});
```

### Sync

#### compressSync(buffer[, brotliEncodeParams])

```javascript
const compressSync = require('iltorb').compressSync;

try {
  var output = compressSync(input);
} catch(err) {
  // ...
}
```

#### decompressSync(buffer)

```javascript
const decompressSync = require('iltorb').decompressSync;

try {
  var output = decompressSync(input);
} catch(err) {
  // ...
}
```

### Stream

#### compressStream([brotliEncodeParams])

```javascript
const compressStream = require('iltorb').compressStream;
const fs = require('fs');

fs.createReadStream('path/to/input')
  .pipe(compressStream())
  .pipe(fs.createWriteStream('path/to/output'));
```

##### compressionStream.flush()

Call this method to flush pending data. Don't call this frivolously, premature flushes negatively impact the effectiveness of the compression algorithm.

#### decompressStream()

```javascript
const decompressStream = require('iltorb').decompressStream;
const fs = require('fs');

fs.createReadStream('path/to/input')
  .pipe(decompressStream())
  .pipe(fs.createWriteStream('path/to/output'));
```

### brotliEncodeParams

The `compress`, `compressSync` and `compressStream` methods may accept an optional `brotliEncodeParams` object to define some or all of brotli's compression parameters:
- [type definition](https://github.com/google/brotli/blob/v1.0.2/c/enc/quality.h#L43-L52)
- [defaults](https://github.com/google/brotli/blob/v1.0.2/c/enc/encode.c#L672-L679)
- [explanations](https://github.com/google/brotli/blob/v1.0.2/c/include/brotli/encode.h#L128-L180)

```javascript
const brotliEncodeParams = {
  mode: 0,
  quality: 11,
  lgwin: 22,
  lgblock: 0,
  size_hint: 0, // automatically set for `compress` and `compressSync`
  disable_literal_context_modeling: false
};
```

[npm-badge]: https://img.shields.io/npm/v/iltorb.svg
[npm-url]: https://www.npmjs.com/package/iltorb
[travis-badge]: https://img.shields.io/travis/MayhemYDG/iltorb.svg
[travis-url]: https://travis-ci.org/MayhemYDG/iltorb
[appveyor-badge]: https://ci.appveyor.com/api/projects/status/ysib4o1bfey84lqk/branch/master?svg=true
[appveyor-url]: https://ci.appveyor.com/project/MayhemYDG/iltorb
[circleci-badge]: https://circleci.com/gh/MayhemYDG/iltorb/tree/master.svg?style=shield
[circleci-url]: https://circleci.com/gh/MayhemYDG/iltorb/tree/master
