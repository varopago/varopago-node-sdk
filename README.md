![Varopago nodejs](http://www.varopago.mx/img/github/nodejs.jpg)

## Installation

`npm install varopago`

## Documentation

Full API documentation available at http://docs.varopago.mx/.

## Overview

```js
//class
var Varopago = require('varopago');
//instantiation
var varopago = new Varopago(' your merchant id ', ' your private key ', [ isProduction ]);
//use the api
varopago.< resource_name >.< method_name >( ... )
```

All methods accept an optional callback as last argument. 

The callback function should follow the format: function(error, body) {...}.
* error: null if the response status code is 200, 201, 204
* body: null if the response status code is different from 200, 201, 204

## Examples

### Creating a customer
```js
var newCustomer = {
  "name":"John",
  "email":"johndoe@example.com",
  "last_name":"Doe",
  "address":{
    "city":"Queretaro",
    "state":"Queretaro",
    "line1":"Calle Morelos no 10",
    "line2":"col. san pablo",
    "postal_code":"76000",
    "country_code":"MX"
  },
  "phone_number":"44209087654"
};

varopago.customers.create(newCustomer, function(error, body) {
    error;    // null if no error occurred (status code != 200||201||204)
    body;     // contains the object returned if no error occurred (status code == 200||201||204)
});
```

### Charging
```js
var newCharge = {
  "method": "card",
  "card": {
    "card_number": "4111111111111111",
    "holder_name": "John Doe",
    "expiration_year": "20",
    "expiration_month": "12",
    "cvv2": "110",
  },
  "amount" : 200.00,
  "description" : "Service Charge",
  "order_id" : "oid-00721"
};
varopago.charges.create(testCreateCharge, function (error, body){
  // ...
});
```

### Payout
```js
var payout = {
  "method": "bank_account",
  "bank_account":{
    "clabe":"012298026516924616",
    "holder_name": "John Doe"
  },
  "amount" : 10.50,
  "description" : "Monthly payment"
};
varopago.payouts.create(payout, function (error, body){
  // ...
});
```

## Configuration

 * `varopago.setTimeout(20000); // in ms (default is 90000ms)`
 * `varopago.setMerchantId(' your merchant id ');`
 * `varopago.setPrivateKey(' your private key ');`
 * `varopago.setProductionReady(true);`

## Development

To run the tests you'll need your sandbox credentials: merchant id and private key from your [Dashboard](https://sandbox-dashboard.varopago.mx/):

```bash
$ npm install -g mocha
$ npm test
```
