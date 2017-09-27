# My BTC Wallet

![alt text](https://user-images.githubusercontent.com/568566/30913634-982d3656-a399-11e7-98df-1ef8b3dbb925.jpg)

> Just for fun

## TODO

* Transaction prio selection Low (within 6 blocks) / High (within 2 blocks)
* Calculate optimal fee at the moment
* Replace by Fee ?
* Reject transactions with minrelaytxfee * 3 (and charge lower then same amount)
* Do not create outputs that are smaller than fee (check is it "dust")
* List transactons filter: Incoming, Outgoing, In Mempool
* HD wallet, check 20 addresses, and 1 account
* BIP39 external lib to support seed from mnemonic decode




## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test
```

For detailed explanation on how things work, checkout the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).
