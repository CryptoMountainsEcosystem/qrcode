
# CMT QR Code

> A web component to generate QR codes for CMT payments.

[![Built With Stencil](https://img.shields.io/badge/-Built%20With%20Stencil-16161d.svg?logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4KPCEtLSBHZW5lcmF0b3I6IEFkb2JlIElsbHVzdHJhdG9yIDE5LjIuMSwgU1ZHIEV4cG9ydCBQbHVnLUluIC4gU1ZHIFZlcnNpb246IDYuMDAgQnVpbGQgMCkgIC0tPgo8c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4IgoJIHZpZXdCb3g9IjAgMCA1MTIgNTEyIiBzdHlsZT0iZW5hYmxlLWJhY2tncm91bmQ6bmV3IDAgMCA1MTIgNTEyOyIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSI%2BCjxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI%2BCgkuc3Qwe2ZpbGw6I0ZGRkZGRjt9Cjwvc3R5bGU%2BCjxwYXRoIGNsYXNzPSJzdDAiIGQ9Ik00MjQuNywzNzMuOWMwLDM3LjYtNTUuMSw2OC42LTkyLjcsNjguNkgxODAuNGMtMzcuOSwwLTkyLjctMzAuNy05Mi43LTY4LjZ2LTMuNmgzMzYuOVYzNzMuOXoiLz4KPHBhdGggY2xhc3M9InN0MCIgZD0iTTQyNC43LDI5Mi4xSDE4MC40Yy0zNy42LDAtOTIuNy0zMS05Mi43LTY4LjZ2LTMuNkgzMzJjMzcuNiwwLDkyLjcsMzEsOTIuNyw2OC42VjI5Mi4xeiIvPgo8cGF0aCBjbGFzcz0ic3QwIiBkPSJNNDI0LjcsMTQxLjdIODcuN3YtMy42YzAtMzcuNiw1NC44LTY4LjYsOTIuNy02OC42SDMzMmMzNy45LDAsOTIuNywzMC43LDkyLjcsNjguNlYxNDEuN3oiLz4KPC9zdmc%2BCg%3D%3D&colorA=16161d&style=flat-square)]()

## Install

### Script tag

- Put this script tag `<script src='https://unpkg.com/CMT-qrcode@latest/dist/CMTqrcode.js'></script>` in the head of your index.html

### Node Modules
- Run `npm install CMT-qrcode --save`
- Put this script tag `<script src='node_modules/CMT-qrcode/dist/CMTqrcode.js'></script>` in the head of your index.html

### In a stencil-starter app
- Run `npm install CMT-qrcode --save`
- Add `{ name: 'CMT-qrcode' }` to your `collections`.

## Usage

Insert the element in your code and enter your custom properties:

```html
<CMT-qrcode address="DE6os4N86ef9bba6kVGurqxmhpBHKctoxY" amount="20.3"></CMT-qrcode>
```

## Examples

```html
<body>
<CMT-qrcode address="DE6os4N86ef9bba6kVGurqxmhpBHKctoxY" amount="10.5" vendor-field="Hello%20CMT!" size="200" show-logo="true">
<script>
  document.querySelector('CMT-qrcode').getURI();
  // => CMT:DE6os4N86ef9bba6kVGurqxmhpBHKctoxY?amount=10.5&vendorField=Hello%20CMT!
</script>
</body>
```

Generate this QR code:

<img src="https://i.imgur.com/VEGA4gO.png" width="15%">

## Properties

This package complies with the specifications described in [AIP-13](https://github.com/CMTEcosystem/AIPs/blob/master/AIPS/aip-13.md).

| Attribute | Description | Type | Required |
| --- | --- | --- | --- |
| address | CMT recipient address encoded in Base58. | String | Yes |
| amount | Amount in CMT (Ѧ) or DCMT (DѦ). | Number | No |
| label | Recipient label string. | String | No |
| size | Size of the QR code (pixels) | Number | No |
| show-logo | Display the CMT logo in QR code | Boolean | No |
| vendor-field | Vendor field string (encoded URI). | String | No |

## Methods

You can interact with the component data using the methods below:

### `getURI()`

Format the properties entered to the [CMT URI scheme](https://github.com/CMTEcosystem/AIPs/blob/master/AIPS/aip-13.md#simpler-syntax).

```javascript
document.querySelector('CMT-qrcode').getURI();
// => CMT:DE6os4N86ef9bba6kVGurqxmhpBHKctoxY?amount=20.3
```

### `getDataURL([mime])`

Generates a base64 encoded data URI for the QR code.

```javascript
document.querySelector('CMT-qrcode').getDataURL();
// => data:image/png;base64,iVBORw0KGgoAAAANSUhE...n6ofvMC4I9AAAAAElFTkSuQmCC
```

### `validateURI(uri)`

Validate an URI string.

```javascript
const uri = 'CMT:DE6os4N86ef9bba6kVGurqxmhpBHKctoxY?amount=10.5';
document.querySelector('CMT-qrcode').validateURI(uri);
// => ["CMT:DE6os4N86ef9bba6kVGurqxmhpBHKctoxY?amount=10.5", "DE6os4N86ef9bba6kVGurqxmhpBHKctoxY", "?amount=10.5"]
```

### `deserializeURI(uri)`

Deserialize the URI scheme to a JSON object.

```javascript
const uri = 'CMT:DE6os4N86ef9bba6kVGurqxmhpBHKctoxY?amount=10.5&vendorField=Hello%20CMT!';
document.querySelector('CMT-qrcode').deserializeURI(uri);
// => { address: 'DE6os4N86ef9bba6kVGurqxmhpBHKctoxY', amount: 10.5, label: null, vendorField: 'Hello CMT!' }
```

### `fromObject(obj)`

Instantiate a URI from an Object.

```javascript
const obj = { address: DE6os4N86ef9bba6kVGurqxmhpBHKctoxY, amount: 10.5 };
const element = document.querySelector('CMT-qrcode').fromObject(obj);
// => <CMT-qrcode address="DE6os4N86ef9bba6kVGurqxmhpBHKctoxY" amount="10.5">
```

## Authors

- Lúcio Rubens <lucio@CMT.io>

## License

CMT QRCode is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.