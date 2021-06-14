---
title: Unqueue API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>

includes:
  - errors

search: true

code_clipboard: true
---

# Introduction

## Overview

Welcome to the Unqueue API! You can use our API to access Unqueue API endpoints, which can get information on various orders, companies, and more.

We have language bindings in JavaScript! You can view code examples in the dark area to the right, and you can switch the programming language of the examples (if available) with the tabs in the top right.

## Authentication

> To authorize, use this code:

```javascript
const kittn = require("kittn");

let api = kittn.authorize("meowmeowmeow");
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

## Requests

The base URL for all requests to the Unqueue API is:
`https://us-central1-unqueue-staging.cloudfunctions.net/`

# Orders

### Request

| Prop                 |                 Type                 |                              Description                              |
| :------------------- | :----------------------------------: | :-------------------------------------------------------------------: |
| accepted             |                `bool`                |                 Whether or not the order was accepted                 |
| cancelled            |                `bool`                |                Whether or not the order was cancelled                 |
| carDetails           |               `string`               |   Description of the shopper's car, optionally entered at checkout    |
| cashAmount           |               `number`               |  The amount of cash the shopper is paying with, entered at checkout   |
| completed            |                `bool`                |                                                                       |
| count                |               `number`               |                   The number of items in the order                    |
| createdAt            |             `Timestamp`              |                      When the order was created.                      |
| customerEmail        |               `string`               |                          The shopper's email                          |
| customerLicense      |               `string`               |           The shopper's license plate, entered at checkout            |
| customerPhone        |               `string`               |                      The shopper's phone number                       |
| deliveryAddress      |               `object`               |                Saved from the associated user document                |
| deliveryFee          |               `number`               |                                                                       |
| deliveryWindow       |            `dddd Do MMMM`            |            The selected date for delivery in string format            |
| driverEnRoute        |                `bool`                |                                                                       |
| onHiredDriverNetwork |                `bool`                |          True if this order is on the Unqueue Driver network          |
| orderNumber          |               `string`               |                                                                       |
| owner                |               `string`               |                                                                       |
| ownerId              |               `string`               |                                                                       |
| packTimeInMinutes    |               `number`               |                                                                       |
| packed               |                `bool`                |                                                                       |
| packedAt             |             `Timestamp`              |                        Automatically generated                        |
| paymentMethod        |               `string`               |                                                                       |
| pickupTimeDate       |            `bool/object`             |     False if shopper picking up ASAP. Object if it is a pre-order     |
| requiresPayment      |                `bool`                |                                                                       |
| source               |             `web \| app`             |                The platform the order was placed from                 |
| specialNotes         |               `string`               |          Special notes attached to the order by the shopper           |
| status               |               `string`               |                         Defaults to 'Pending'                         |
| storeAddress         |               `object`               |              Saved from the associated company document               |
| storeHours           |               `object`               |              Saved from the associated company document               |
| storeId              |               `string`               |              Saved from the associated company document               |
| storeLogo            |               `string`               |          The logo of the company this order was placed from           |
| storeName            |               `string`               |              Saved from the associated company document               |
| storePhone           |               `string`               |              Saved from the associated company document               |
| timeWindow           | `daytimeDelivery \| eveningDelivery` |                                                                       |
| total                |               `float`                | The total cost of the order including delivery, addons and variations |
| type                 |               `string`               |                    The pickup method of the order                     |
| unavailableItems     |                `bool`                |                                                                       |

## Get an o

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
curl "http://example.com/api/kittens" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require("kittn");

let api = kittn.authorize("meowmeowmeow");
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

| Parameter    | Default | Description                                                                      |
| ------------ | ------- | -------------------------------------------------------------------------------- |
| include_cats | false   | If set to true, the result will also include cats.                               |
| available    | true    | If set to false, the result will include kittens that have already been adopted. |

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
curl "http://example.com/api/kittens/2" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require("kittn");

let api = kittn.authorize("meowmeowmeow");
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

| Parameter | Description                      |
| --------- | -------------------------------- |
| ID        | The ID of the kitten to retrieve |

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
curl "http://example.com/api/kittens/2" \
  -X DELETE \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require("kittn");

let api = kittn.authorize("meowmeowmeow");
let max = api.kittens.delete(2);
```

> The above command returns JSON structured like this:

```json
{
  "id": 2,
  "deleted": ":("
}
```

This endpoint deletes a specific kitten.

### HTTP Request

`DELETE http://example.com/kittens/<ID>`

### URL Parameters

| Parameter | Description                    |
| --------- | ------------------------------ |
| ID        | The ID of the kitten to delete |
