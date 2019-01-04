# CMT QR Code

> A web component to generate QR codes for CMT payments.

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

- Lorenzo Caruso <lorenzo.caruso@outlook.com>

## License

CMT QRCode is licensed under the MIT License - see the [LICENSE](./LICENSE) file for details.