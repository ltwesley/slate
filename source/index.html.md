---
title: API Reference

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

The `RPM Wrapper` API is organized around REST. It accepts form-encoded request bodies, returns JSON-encoded responses, and uses standard HTTP response codes, authentication, and verbs.

# Authentication

Access to the `RPM Wrapper` API expects a Basic Auth header to be included in all API requests to the server that looks like the following:

`authorization: Basic YXBwd2F5OkNpZnVuZHMxMjM=`

> Example of an authorize request:

```shell
curl -X GET "http://localhost:5000/new_rpm_session" 
  -H "authorization: Basic YXBwd2F5OkNpZnVuZHMxMjM="
```

# RPM Session Token
Requests to the **RPM Native** API requires a RPM session token in the header `X-RPM-Session-Token`.
`/new_rpm_session` API endpoint will return such token.

The token will expire after 20 mins ??

```shell
# Request for a RPM Session Token. Username is required in the Header
curl -X GET "http://localhost:5000/new_rpm_session" 
  -H "accept: application/json" 
  -H "authorization: Basic YXBwd2F5OkNpZnVuZHMxMjM="
  -H "X-User-ID: dsmith" 
```

```javascript
# Sample Response 
{
  "RpmSessionToken": "295810190713-1006842051-100003828599"
}
```
# RPM Objects

## Address

Parameter | Type | Default | Description
--------- | ---- | ------  | -----------
AddressId | integer | |
Addr1 | string | |
Addr2 | string | |
Addr3 | string | |
City | string | |
Province| string | |
Country | string | |
Postal | string | |
Status | | |
Attn | string | |


## AddressUsage

Parameter | Type | Default | Description
--------- | ---- | ------- | -----------
AddressUsageId | | |
AddressUsageType | | |
Address | Object | |
AddressVerified | boolean | |
ReturnedMail | | |
HoldMail | | |
InCareOf | | |
GeneralDeliveryPOBox | | |

## Agent

Parameter | Type | Description
--------- | ---- |  -----------
AgentId | number | 
Branch | number | 
BranchDescription | | 
Code | number |  
Dealer | Object?Number |
DealerDescription | Object | 
DealerId | number |  
FirstName | string |
LastName | string | 
Status | number |  
UserSuppliedKYC | boolean | 
Email | string |
Phone | Object | 
Region | string |  

```javascript
"Agent": {
  "AgentId": "1012401",
  "Branch": "4003",
  "BranchDescription": {
    "DescriptionId": "2449249",
    "English": "Dorval 1",
    "French": "Dorval 1",
    "RowVer": "4"
  },
  "Code": "2398",
  "CustodianSettlement": "1",
  "Dealer": "9721",
  "DealerDescription": {
    "DescriptionId": "1000713",
    "English": "Assante Capital Management Ltd.",
    "French": "Gestion de capital Assante ltée",
    "RowVer": "1"
  },
  "DealerId": "1000001",
  "Email": "SelChaer@assante.com / AArgento@Assante.com",
  "FirstName": "Sam El-Chaer",
  "Internal": "true",
  "LastName": "and Alex Argento",
  "MandatoryKYCFields": "false",
  "Phone": {
    "PhoneId": "1795518",
    "PhoneNo": "8325100",
    "RouteCode": "514",
    "RowVer": "0",
    "Status": "0"
  },
  "Region": "003",
  "RegionDescription": {
    "English": "ACM Eastern Canada",
    "French": "GCA Canada du Est"
  },
  "Status": "0",
  "UsePOSFundFactsDelivery": "false",
  "UserSuppliedKYC": "false"
},
```

# API Endpoints

## Get All Kittens

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get()
```

```shell
curl "http://example.com/api/kittens"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let kittens = api.kittens.get();
```

> The above command returns JSON structured like this:

```json
[
  {
    "id": 1,
    "name": "Fluffums",
    "breed": "calico",
    "fluffiness": 6,
    "cuteness": 7
  },
  {
    "id": 2,
    "name": "Max",
    "breed": "unknown",
    "fluffiness": 5,
    "cuteness": 10
  }
]
```

This endpoint retrieves all kittens.

### HTTP Request

`GET http://example.com/api/kittens`

### Query Parameters

Parameter | Default | Description
--------- | ------- | -----------
include_cats | false | If set to true, the result will also include cats.
available | true | If set to false, the result will include kittens that have already been adopted.

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>

## Get a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "name": "Max",
  "breed": "unknown",
  "fluffiness": 5,
  "cuteness": 10
}
```

This endpoint retrieves a specific kitten.

<aside class="warning">Inside HTML code blocks like this one, you can't use Markdown, so use <code>&lt;code&gt;</code> blocks to denote code.</aside>

### HTTP Request

`GET http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to retrieve

## Delete a Specific Kitten

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.delete(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.delete(2)
```

```shell
curl "http://example.com/api/kittens/2"
  -X DELETE
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted" : ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

Parameter | Description
--------- | -----------
ID | The ID of the kitten to delete

