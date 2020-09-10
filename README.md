bitcoin-live-transactions
=====

This module uses running [insight-api](https://github.com/Groestlcoin/insight-api) instances to get live groestlcoin transaction as they happen in the Groestlcoin P2P network.

How to use it
--

Create a **GLT** (Groestlcoin Live Transactions) instance:
```javascript
var GLT = require("groestlcoin-live-transactions")
var groestlcoin = new GLT()
```

Connect to the Groestlcoin P2P network:
```javasctript
groestlcoin.connect()
```

Get a notification when successfully connected to the  groestlcoin P2P network.
```javascript
groestlcoin.events.on('connected', function() {
   // start listening to addresses
})
```

Check an address
--
Check uGRS balance for a given groestlcoin address:
```javascript
groestlcoin.getBalance('FnQZTzpY3c7BTrQ2SPDcFftxWjJRwhFDXQ').then(function(balance) {
  console.log('balance:', balance);
})
```

Will output:

```javascript
balance: {
  address: 'FnQZTzpY3c7BTrQ2SPDcFftxWjJRwhFDXQ',
  in: 18180000668784.2,
  out: 16979999859174.8,
  curr: 'groestls(uGRS)',
  balance: 1200000809609.3984,
  txs: 14
}
```

That can be checked here:
[https://groestlsight.groestlcoin.org/address/FnQZTzpY3c7BTrQ2SPDcFftxWjJRwhFDXQ](https://groestlsight.groestlcoin.org/address/FnQZTzpY3c7BTrQ2SPDcFftxWjJRwhFDXQ)

To get all the detailed information about an address, use **groestlcoin.getTxs** instead of **groestlcoin.getBalance**

Live stream
--

To Listen to live transaction events on the Groestlcoin P2P network for a given address, the event is called as the address itself:
```javascript
groestlcoin.events.on('FnQZTzpY3c7BTrQ2SPDcFftxWjJRwhFDXQ',function(tx){
  console.log('Transaction detected!', tx);
})
```
Will trigger the event in real time if a payment is done to that address:
```javascript
Transaction detected! { address: 'FnQZTzpY3c7BTrQ2SPDcFftxWjJRwhFDXQ',
  amount: 381000 }
```

Show everything live
--

If you want to see **ALL** transactions happening live, use the **tx** event:



```javascript
groestlcoin.events.on('tx',function(tx){
  console.log('>> Transaction detected:', tx);
})
```
Will trigger the event in real time if a payment is done to that address:
```javascript
>> Transaction detected: {
  txid: 'dd6b910912c18514e3763ccbbedd020e133441a32c8fa11c7040d48cefc43a71',
  valueOut: 9489.7999666
}
```

Testnet
--

To use test-net add *{testnet:true}* when instantiating the module, as follows:

```javascript
var GLT = require("groestlcoin-live-transactions")
var groestlcoin = new GLT({testnet: true})
```
