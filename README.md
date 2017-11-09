# fastify-compress

[![Build Status](https://travis-ci.org/fastify/fastify-compress.svg?branch=master)](https://travis-ci.org/fastify/fastify-compress) [![js-standard-style](https://img.shields.io/badge/code%20style-standard-brightgreen.svg?style=flat)](http://standardjs.com/)

Adds compression utils to the Fastify `reply` object.  
Support `gzip`, `deflate` and `brotli`.

## Install
```
npm i fastify-compress --save
```

## Usage
This plugin add a `compress` function to `reply` that accepts a stream, and compress it based on the `'accept-encoding'` header.  
Currently the following headers are supported:
- `'deflate'`
- `'gzip'`
- `'br'`

If an unsupported encoding is received, it will automatically return a `406` error, if the `'accept-encoding'` header is missing, it will return a `400` error.

```javascript
const fs = require('fs')
const fastify = require('fastify')

fastify.register(require('fastify-compress'))

fastify.get('/', (req, reply) => {
  reply.compress(fs.createReadStream('./package.json'))
})

fastify.listen(3000, function (err) {
  if (err) throw err
  console.log(`server listening on ${fastify.server.address().port}`)
})
```

## Acknowledgements
This project is kindly sponsored by:
- [LetzDoIt](http://www.letzdoitapp.com/)

## License

Licensed under [MIT](./LICENSE).
