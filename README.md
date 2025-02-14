<h1 align="center">
  <a href="https://example.com/"><img src="https://example.com/uploads/2022/08/logo.svg" alt="IPSP JS SDK" width="109" height="25"></a>
  <br>
  IPSP JS SDK
  <br>
</h1>

<h4 align="center"></h4>

<p align="center">
<a href="https://www.npmjs.com/package/ipsp-js-sdk"><img src="https://img.shields.io/npm/v/ipsp-js-sdk.svg" /></a>
<a href="https://www.npmjs.com/package/ipsp-js-sdk"><img src="https://img.shields.io/npm/dt/ipsp-js-sdk.svg" /></a>
<a href="https://github.com/cloudipsp/ipsp-js-sdk"><img src="https://img.shields.io/bower/v/ipsp-js-sdk.svg" /></a>
<a href="https://github.com/cloudipsp/ipsp-js-sdk"><img src="https://img.shields.io/github/license/cloudipsp/ipsp-js-sdk.svg" /></a>
<a href="https://example.com/"><img src="https://img.shields.io/badge/official-website-green.svg" /></a>
</p>


## Installation

### Node

If you’re using [Npm](https://npmjs.com/) in your project, you can add `ipsp-js-sdk` dependency to `package.json` 
with following command:

```cmd
npm i --save ipsp-js-sdk
```

or add dependency manually:

```json
{
  "dependency": {
    "ipsp-js-sdk":"^2.0"
  }
}
```

### Bower

If you’re using [Bower](https://bower.io/) in your project, you can run the following command:

```cmd
bower install ipsp-js-sdk
```

### Manual installation

If you do not use NodeJS, you can download the
[latest release](https://github.com/cloudipsp/ipsp-js-sdk/releases).
Or clone from GitHub the latest developer version
```cmd
git clone git@github.com:cloudipsp/ipsp-js-sdk.git
```


## Quick start

```html
<script src="https://unpkg.com/ipsp-js-sdk@latest/dist/checkout.min.js"></script>
```

## Basic template

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  </head>
  <body>
    <script src="https://unpkg.com/ipsp-js-sdk"></script>
    <script>
    $checkout('Api').scope(function(){
        this.request('api.checkout.form','request', { Parameters } ).done(function(model){
            model.sendResponse();
            console.log(model.attr('order'));
        }).fail(function(model){
            console.log(model.attr('error'));
        });
    });
    </script>
  </body>
</html>
```

## PaymentButton template (ApplePay/GooglePay)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  </head>
  <body>
    <script src="https://unpkg.com/ipsp-js-sdk"></script>
    <div class="payment-button-container"></div>
    <script>
    $checkout.get('PaymentButton', {
      element: '.payment-button-container',
      style: {
        type: 'long', // short|long
        color: 'black', // black|white
        height: 38 // button height
      },
      data: { Parameters }
    }).on('success', function(model) {
      console.log('success', model);
    }).on('error', function(model) {
      console.log('error', model);
    });
    </script>
  </body>
</html>
```

## Parameters

### Host-to-host token


```json
{
  "payment_system":"Supported payment systems: card, p24",
  "token":"host-to-host generated token",
  "card_number":"16/19-digits number",
  "expiry_date":"Supported formats: MM/YY, MM/YYYY, MMYY, MMYYYY",
  "cvv2":"3-digits number"
}
```

Where token is value, returned in paymentgateway response from API enpoint /api/checkout/token (more details in API documentation: https://documentation.albpay.io/docs/page/3/ )

request example:

```
curl -i -X POST \
   -H "Content-Type:application/json" \
   -d \
'{
  "request": {
    "server_callback_url": "http://myshop/callback/",
    "order_id": "TestOrder1",
    "currency": "USD",
    "merchant_id": 1545859,
    "order_desc": "Test payment",
    "amount": 1000
  }
}' \
 'https://payment.albpay.io/api/checkout/token'
```

response example:
```json
{
    "response": {
        "response_status": "success",
        "token": "7ddb3fbb03d60787b3972ef8d6fad0f97f7d2f86"
    }
}
```



### Client-side merchant ID

```json
{
  "payment_system":"Supported payment systems: card, p24",
  "merchant_id":"1545859",
  "currency":"USD",
  "amount":"100.20",
  "card_number":"16/19-digits number",
  "expiry_date":"Supported formats: MM/YY, MM/YYYY, MMYY, MMYYYY",
  "cvv2":"3-digits number"
}
```

optional merchant parameters:


```json
{
  "email":"customer email address",
  "phone":"customer phone number"
}
```
## JS SDK usage example

https://jsfiddle.net/fondyeu/jdc9o5cx/


## License

[MIT](https://github.com/cloudipsp/ipsp-js-sdk/blob/HEAD/LICENSE)

