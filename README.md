# ontlogin-sdk-ui

OntLogin web component UI SDK for JavaScript provides easy integration for your application to OntLogin.

## Before start

- The backend api need to be implemented with defined specification.
- Check web component compatibility. -> https://caniuse.com/?search=Custom%20Elements
- Check [ontlogin-sdk-js](https://github.com/ontology-tech/ontlogin-sdk-js) if custom ui is required.

## Getting started

_via NPM [package](https://npmjs.com/package/ontlogin-ui):_

```
npm i ontlogin-ui
```

```js
import "ontlogin-ui";
```

```html
<ont-login
  url_of_get_challenge="server/requestChallenge"
  url_of_submit_response="server/submitChallenge"
/>
```

_via [js bundle](./dist/ontloginui.min.js):_

```html
<ont-login
  id="ontlogin"
  url_of_get_challenge="server/requestChallenge"
  url_of_submit_response="server/submitChallenge"
/>
<script src="ontloginui.min.js"></script>
<script>
  // add event listener to custom event
  const target = document.querySelector("#ontlogin");
  target.addEventListener("success", (e) => {
    console.log(e.detail);
  });
  target.addEventListener("error", (e) => {
    console.log(e.detail);
  });
  target.addEventListener("cancel", (e) => {
    console.log(e.detail);
  });
</script>
```

## Api

### Params

| Name                   | Type   | Des                                                          |
| ---------------------- | ------ | ------------------------------------------------------------ |
| url_of_get_challenge   | string | Api url of get challenge(implement with api definition below). |
| url_of_submit_response | string | Api url of submit response(implement with api definition below). |
| show_vc_list           | string | 'true'\|'false'.Show vc list in dialog if exist.             |
| test                   | string | 'true' \| 'false'.Add a button to mock use scan success(test only). |
| action                 | string | '0' \| '1'. Action type in string,Refer to action of [authentication-request](https://docs.ont.io/decentralized-identity-and-data/ontid/ont-login/protocol-specification#authentication-request) . |

### Events

| Name    | Type        | Des                                                                          |
| ------- | ----------- | ---------------------------------------------------------------------------- |
| success | CustomEvent | Submit success callback,with response of url_of_submit_response in e.detail. |
| error   | CustomEvent | Error callback.                                                              |
| cancel  | CustomEvent | User cancel callback.                                                        |

### Server api definition

#### url_of_get_challenge:

The Server api for get challenge with auth request.

_Request/Response content type_

`application/json`

_Request body_

request object refer to url-to-request-protocol

example:

`{"ver":"1.0","type":"ClientHello","action":0}`

_Response body_

challenge object refer to url-to-challenge-protocol

example:

`{"ver":"1.0","type":"ServerHello","nonce":"8125419d-0ba4-11ec-a4f0-441ca8e37c61","server":{"name":"testServcer","icon":"http://somepic.jpg","url":"https://ont.io","did":"did:ont:sampletest"},"chain":["ONT"],"alg":["ES256"],"VCFilters":[{"type":"EmailCredential","trust_roots":["did:ont:testdid"],"required":true}]}`

#### url_of_submit_response:

The Server api for submit auth response to server.

_Request/Response content type_

`application/json`

_Request body_

Response object refer to url-to-response-protocal

example:

`{"ver":"1.0","type":"ClientResponse","nonce":"221b111a-0ba5-11ec-a4f0-441ca8e37c61","did":"did:ont:AR9NDnK3iMSZodbENnt7eX5TJ2s27fnHra","proof":{"type":"Ed25519","verificationMethod":"did:ont:AR9NDnK3iMSZodbENnt7eX5TJ2s27fnHra#key-1","created":1630556445,"value":"01c3841e922884df9288dde3c1fecbb575482c834560781454c44192b54140d3a7413d116fe81b76e3e74f88e2eb1351c120854d47189241545f66d7702cab8523"},"VPs":[]}`

_Response body_

Anything in json

## Example apps

- [vue](https://github.com/ontology-tech/ontlogin-sdk-ui/tree/main/examples/vue)

- [pure HTML](https://github.com/ontology-tech/ontlogin-sdk-ui/tree/main/examples/html)
