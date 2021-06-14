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

If you are using our API using the Firebase SDK, there is no need to do any authentication as long as you have initialized using Unqueue's credentials.

If you are using our API via HTTP requests, ensure to add the `auth` header to your requests. You can register a new Unqueue auth key <a href='mailto:andel@agyei.design'>here</a>.

> Using Callable Firebase functions:

```javascript
const exampleCallableFunctionCall = async () => {
  try {
    const createOrder = firebase.functions().httpsCallable("createOrder");
    const request = await createOrder({
      foo: "bar",
    });
    console.log(request.data);
  } catch (err) {
    console.log(err.message);
  } finally {
    setLoading(false);
  }
};
```

> Using the auth header, an axios example

```javascript
const token = "..your token..";

axios.post(
  baseUrl,
  {
    //...data
  },
  {
    headers: {
      auth: token,
    },
  }
);
```

> Make sure to replace `token` with your own key.

## Requests

When using the auth key for requests, the base URL for all requests to the Unqueue API is:

`https://us-central1-unqueue-staging.cloudfunctions.net`

# Companies

The companies API allows you to create, view, and update individual companies.

## Company Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| acceptsCard             |              `bool`               |                                      True if the company accepts LINX/Debit payments                                      |
| acceptsCash             |              `bool`               |                                         True if the company accepts cash payments                                         |
| acceptsOrdersAfterHours |              `bool`               |                   True if the company accepts pre-orders. Shoppers can place orders after opening hours                   |
| acceptsPayouts          |              `bool`               |                                        True if the company accepts online payments                                        |
| acceptsPortableCard     |              `bool`               |  True if the company accepts portable LINX/Debit payments. This must be true to enable LINX payments on a curbside order  |
| active                  |              `bool`               |                                           True if the company can accept orders                                           |
| address                 | The address object of the company |
| categories              |            `string[]`             |                                     An array of category Id's the company belongs to                                      |
| chatEnabled             |              `bool`               |                             (Legacy) True if the company accepts chat messages from shoppers                              |
| createdAt               |            `Timestamp`            |                                            When the company was first created                                             |
| deliveryFee             |              `float`              | The cost of deliveries set by the store. Only applicable for stores offering Delivery and not on Unqueue's driver network |
| deliveryWindows         |        `DeliveryWindows[]`        |                                The days and time windows that the company offers delivery                                 |
| description             |             `string`              |                                            A short description of the company.                                            |
| doesCurbside            |              `bool`               |                                         True if the company does Curbside Pickups                                         |
| doesDelivery            |              `bool`               |                                   True if the company does Delivery as a pickup method.                                   |
| doesWalkin              |              `bool`               |                                         True if the company does in store pickups                                         |
| email                   |             `string`              |                                             The email address of the company                                              |
| emailVerified           |              `bool`               |                                     True if the company's email address is verified.                                      |
| expoToken               |             `string`              |                                        The push notification token of the company.                                        |
| handlesCloserDeliveries |              `bool`               |                                                         (Legacy).                                                         |
| hasCategories           |              `bool`               |                                True if the company has at least 1 category with products.                                 |
| headerImage             |             `string`              |                                           The URL of the company's header image                                           |
| headerThumb             |             `string`              |                               The URL of an optimized version of the company's header image                               |
| id                      |             `string`              |                                             The ID of the company in the DB.                                              |
| lastOpened              |            `Timestamp`            |                                 The last time the business app was opened by the Company                                  |
| lastStep                |             `string`              |                                                                                                                           |
| logo                    |             `string`              |                                              The URL of the company's logo.                                               |
| logoOtherThumb          |             `string`              |                                                                                                                           |
| logoThumb100            |             `string`              |                                                                                                                           |
| logoThumb300            |             `string`              |                                                                                                                           |
| logoThumb640            |             `string`              |                                                                                                                           |
| masterVerified          |              `bool`               |                                 True if the company account is enabled by Unqueue admin.                                  |
| maxDeliveryTime         |       `string (eg 60mins)`        |       A string representation of how far a business is willing to deliver. Only applies if not on Unqueue Delivery        |
| minForDelivery          |              `float`              |          The minimum that a shopper must spend to qualify for delivery. Only applies if not on Unqueue Delivery           |
| name                    |             `string`              |                                                  The name of the company                                                  |
| numRatings              |             `number`              |                                       The number of ratings received by the company                                       |
| onDriverNetwork         |              `bool`               |                                      True if on Unqueue's On Demand Delivery Network                                      |
| onHiredDriverNetwork    |              `bool`               |                                      True if on Unqueue's Pre-order Delivery Network                                      |
| onSaleCount             |             `number`              |                                         The number of items to store has on sale                                          |
| openingDays             |          `OpeningDays[]`          |                                        The days and times that the company is open                                        |
| ownerFirstName          |             `string`              |                                 The first name of the person running the company account.                                 |
| ownerLastName           |             `string`              |                                 The last name of the person running the company account.                                  |
| packingTime             |             (Legacy).             |
| phone                   |             `string`              |                                              The phone number of the company                                              |
| photoId                 |             `strinng`             |                                                                                                                           |
| rating                  |              `float`              |                                               The company's average rating                                                |
| storeOn                 |              `bool`               |                                      True if the store should be visible to shoppers                                      |
| storeOnFlagged          |              `bool`               |                              True if Unqueue has been alerted that this store has turned on                               |
| storeProductsView       |         `gallery or list`         |                            Whether to display the company's products in a list or gallery view                            |
| tags                    |            `string[]`             |                                                         (Legacy)                                                          |
| uniqueUsername          |             `string`              |                                                                                                                           |
| unreadCompanyMessages   |             `number`              |                                                                                                                           |
| unreadMessages          |             `number`              |                                                                                                                           |
| views                   |             `number`              |                                         The number of time the company was viewed                                         |

## Create Company

Create a new company.

### Callable Function Name

`createCompany`

### HTTP Request

`POST /createCompany`

### Body

| Parameter | Description                     |
| --------- | ------------------------------- |
| id        | The ID of the company to update |

### Response

<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->

## Get Company

Retrieve details about a company.

### Callable Function Name

`getCompany`

### HTTP Request

`POST /getCompany`

### Body

| Parameter | Description                       |
| --------- | --------------------------------- |
| id        | The ID of the company to retrieve |

### Response

```json
{
  "data": {
    "acceptsCard": true,
    "acceptsCash": true,
    "acceptsOrdersAfterHours": ,
    "acceptsPayouts": true,
    "acceptsPortableCard": false,
    "active": true,
    "address": {
      "address": "Street name",
      "buildingNumber": "24",
      "location": {
        "latitude": 62,
        "longitude": 31
      }
    },
    "categories": ["categoryId", "categoryId2"],
    "chatEnabled": true,
    "createdAt": 12,
    "deliveryFee": 30,
    "deliveryWindows": [{
      "foo": "bar"
    }],
    "description": "Some store description",
    "doesCurbside": true,
    "doesDelivery": true,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
  }
}
```

<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->

## Update Company

Update a company with new details.

### Callable Function Name

`updateCompany`

### HTTP Request

`POST /updateCompany`

### Body

| Parameter | Description                     |
| --------- | ------------------------------- |
| id        | The ID of the company to update |

### Response

<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->

# Orders

The orders API allows you to create, view, update, and delete individual orders.

## Order Properties

| Attribute            |                 Type                 |                              Description                              |
| :------------------- | :----------------------------------: | :-------------------------------------------------------------------: |
| id                   |               `string`               |                   Unique identifier for the order.                    |
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

## Create Order

Create a new draft order.

<aside class="notice">
    Draft orders must be completed in order to create an actual Order. Use the id returned from createOrder to pass to completeDraftOrder when completing the order.
</aside>

### Callable Function Name

`createOrder`

### HTTP Request

`POST /createOrder`

### Body

| Parameter | Description                     |
| --------- | ------------------------------- |
| id        | The ID of the company to update |

### Response

```json
{
  "data": {
    "order": {
      "cart": [
        {
          "addonsPrice": 0,
          "categoryId": "someId",
          "count": 1,
          "id": "someproductId",
          "title": "product 1",
          "note": "some note",
          "price": 659.99
        }
      ],
      "carDetails": "Dark Blue Mazda",
      "cashAmount": 20,
      "customerLicense": "PDC9543",
      "deliveryAddress": {
        "address": "Some address",
        "streetName": "Some sddress",
        "location": {
          "latitude": 12.123,
          "longitude": -61
        }
      },
      "paymentMethod": "Cash",
      "source": "web",
      "specialNotes": "Some special notes",
      "type": "Walkin",
      "total": 100
    },
    "shopperData": {
      "id": "PsoMpLhC7pTUXmIakdtreaZBWus1",
      "name": "Cyan Sylvester",
      "email": "johndoe@gmail.com",
      "phone": "+18687188625"
    },
    "store": {
      "id": "FBdbIxss6IT9TmiaUvnIAo17jLe2",
      "name": "Sunset Views",
      "address": {
        "address": "Some address",
        "streetName": "Some sddress",
        "location": {
          "latitude": 10.66131356208752,
          "longitude": -61.52237425545026
        }
      },
      "phone": "+18687188625",
      "logo": "https://firebasestorage.googleapis.com/v0/b/unqueue-staging.appspot.com/o/logos%2FFBdbIxss6IT9TmiaUvnIAo17jLe2%2Flogo.png?alt=media&token=f818be77-694d-482e-b963-8933eb2c6034",
      "openingDays": [
        {
          "closingTime": "July 7, 1995 at 8:00:00 PM UTC-4",
          "day": "Sunday",
          "label": "Su",
          "open": true,
          "openingTime": "July 7, 1995 at 7:00:00 AM UTC-4"
        }
      ]
    }
  }
}
```

<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->

## Get Order

Retrieve details about an order.

### Callable Function Name

`getOrder`

### HTTP Request

`POST /getOrder`

### Body

| Parameter | Description                     |
| --------- | ------------------------------- |
| id        | The ID of the order to retrieve |

### Response

```json
{
  "data": {
    "acceptsCard": true,
    "acceptsCash": true,
    "acceptsOrdersAfterHours": ,
    "acceptsPayouts": true,
    "acceptsPortableCard": false,
    "active": true,
    "address": {
      "address": "Street name",
      "buildingNumber": "24",
      "location": {
        "latitude": 62,
        "longitude": 31
      }
    },
    "categories": ["categoryId", "categoryId2"],
    "chatEnabled": true,
    "createdAt": 12,
    "deliveryFee": 30,
    "deliveryWindows": [{
      "foo": "bar"
    }],
    "description": "Some store description",
    "doesCurbside": true,
    "doesDelivery": true,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
    "": ,
  }
}
```

<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->

## Update Order

Update an order with new details.

### Callable Function Name

`updateOrder`

### HTTP Request

`POST /updateOrder`

### Body

| Parameter | Description                   |
| --------- | ----------------------------- |
| id        | The ID of the order to update |

### Response

<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->
