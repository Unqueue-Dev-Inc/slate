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

If you are using our API via HTTP requests, ensure to add the `Authorization` header to your requests. We will provide you with a token. You can register a new Unqueue token by sending an email <a href='mailto:andel@agyei.design'>here</a>.

> Using the Authorization header, an axios example

```javascript
const token = "..your token..";

axios.post(
  baseUrl,
  {
    //...data
  },
  {
    headers: {
      Authorization: `Bearer ${token}`,
    },
  }
);
```

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

> Make sure to replace `token` with your own key.

## Requests

When using the auth key for requests, the base URL for all requests to the Unqueue API is:

### Testing

`https://us-central1-unqueue-staging.cloudfunctions.net`

### Live

You will be provided with a live URL after your API request.

# Categories

<!-- The categories API allows you to create, view, and update individual categories. -->

## Category Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| active                  |              `bool`               |                                           True if the category is visible                                           |
| createdAt               |            `Timestamp`            |                                            The timestamp of the category creation.                                             |
| description              |            `string`             |                                     A short description of the category.                                      |
| id             |              `string`               |                             The unique ID of the category.                              |
| image             |              `string`              | The cover image of the category.
| title             |              `string`              | The name of the category. 
| type             |              <code>default &#124; leaderboard &#124; featured</code>              | The type of a category determines where it is shown on the website. 
| updatedAt             |              `Timestamp`              | The timestamp of the last category update. 
| views             |              `number`              | The number of times the category has been viewed.

# Chats

<!-- The chats API allows you to create, view, and update individual chats. -->
## Chat Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| id             |              `string`               |                             The unique ID of the chat.                              |
| companyId                  |              `string`               |                                           The ID of the company this chat belongs to. |
| companyName              |            `string`             |                                     The name of the company this chat belongs to.                                      |
| createdAt               |            `Timestamp`            |                                            The timestamp of the chat creation.                                             |
| currentAdmin             |              <code>string &#124; null</code>              | The name of the admin managing the chat. (For Unqueue Support chat).
| lastMessageSentAt             |              `Timestamp`              | The timestamp of the last sent message.
| latestMessage             |              `Object`              | An object representing the last message sent. 
| logo             |              `string`             | The company logo. 
| shopperName             |              `string`              | The name of the user this chat belongs to.
| unreadCompanyMessages             |              `number`              | The number of unread messages in this chat for the company.
| unreadShopperMessages             |              `number`              | The number of unread messages in this chat for the user.
| userId             |              `string`              | The ID of the user this chat belongs to.
# Drivers

<!-- The chats API allows you to create, view, and update individual chats. -->
## Driver Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| storeId                  |              <code>string &#124; null</code>               |                                           The id of the company this driver belongs to. |
| createdAt               |            `Timestamp`            |                                            The timestamp of the driver creation.                                             |
| storeName              |            <code>string &#124; null</code>             |                                     The name of the company this driver belongs to.                                      |
| id             |              `string`               |                             The unique ID of the driver                              |
| active             |              `bool`              | True if the driver is cleared to drive for Unqueue for the Company.
| carDetails             |              `string`              | A description of the driver's current vehicle.
| currentTripId             |              `string`              | The ID of the [Driver Trip](#driver-trip-properties) the driver is currently on. 
| expoToken             |              `string`             | The push notification token for the driver. 
| fullTimeDriver             |              `bool`              | True if the driver does deliveries for Unqueue. 
| licensePlate             |              `string`              | The driver's car license plate.
| location             |              `GeoPoint`              | The last recorded location of the driver.
| name             |              `string`              | The name of the driver.
| onTrip             |              `bool`              | True if the driver is currently on a delivery trip.
| online             |              `bool`              | True if the driver is online and accepting orders.
| phoneNumber             |              `string`              | The phone number of the driver.
| registered             |              `bool`              | True if the driver has finished registration.
| updatedAt             |              `Timestamp`              | The timestamp of the last driver profile update.
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
| address                 | [CompanyAddress](#company-address-properties) | An object representing the company address
| categories              |            `string[]`             |                                     An array of category Id's the company belongs to                                      |
| chatEnabled             |              `bool`               |                             (Legacy) True if the company accepts chat messages from shoppers                              |
| customCheckoutEnabled             |              `bool`               |                             True if the company is using the custom checkout version of Unqueue                              |
| createdAt               |            `Timestamp`            |                                            When the company was first created                                             |
| deliveryFee             |              `float`              | The cost of deliveries set by the store. Only applicable for stores offering Delivery and not on Unqueue's driver network |
| deliveryWindows         |        [DeliveryWindows[]](#delivery-window-properties)        |                                The days and time windows that the company offers delivery                                 |
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
| lastStep                |            `string` |   A string representing the user's last step while still completing the sign up process.                                                                                                                        |
| logo                    |             `string`              |                                              The URL of the company's logo.                                               |
| logoOtherThumb          |             `string`              |                                                                                                                           |
| logoThumb100            |             `string`     | The URL of the company's logo with dimensions 100 x 100.                                                                                                                           |
| logoThumb300            |             `string` | The URL of the company's logo with dimensions 300 x 300                                                                                                                           |
| logoThumb640            |             `string`  | The URL of the company's logo with dimensions 640 x 640                                                                                                                           |
| mailingInfo          |             [MailingInfo](#company-mailing-info)               |                                 The mailing address of the company. This is used to determine where to send packages to.                                  |
| masterVerified          |              `bool`               |                                 True if the company account is enabled by Unqueue admin.                                  |
| maxDeliveryTime         |       <code>20 Mins &#124; 30 Mins &#124; 40 Mins &#124; 60 Mins</code>        |       A string representation of how far a business is willing to deliver. Only applies if not on Unqueue Delivery        |
| minForDelivery          |              `float`              |          The minimum that a shopper must spend to qualify for delivery. Only applies if not on Unqueue Delivery           |
| name                    |             `string`              |                                                  The name of the company                                                  |
| numRatings              |             `number`              |                                       The number of ratings received by the company                                       |
| onDriverNetwork         |              `bool`               |                                      True if on Unqueue's On Demand Delivery Network                                      |
| onHiredDriverNetwork    |              `bool`               |                                      True if on Unqueue's Pre-order Delivery Network                                      |
| onSaleCount             |             `number`              |                                         The number of items to store has on sale                                          |
| openingDays             |          [OpeningDay[]](#opening-days-properties)          |                                        The days and times that the company is open                                        |
| ownerFirstName          |             `string`              |                                 The first name of the person running the company account.                                 |
| ownerLastName           |             `string`              |                                 The last name of the person running the company account.                                  |
| packingTime             |             (Legacy).             |
| phone                   |             `string`              |                                              The phone number of the company                                              |                                                                                                                          |
| rating                  |              `float`              |                                               The company's average rating                                                |
| storeOn                 |              `bool`               |                                      True if the store should be visible to shoppers                                      |
| storeOnFlagged          |              `bool`               |                              True if Unqueue has been alerted that this store has turned on                               |
| storeProductsView       |         <code>gallery &#124; list</code>         |                            Whether to display the company's products in a list or gallery view                            |
| tags                    |            `string[]`             |                                                         (Legacy)                                                          |
| uniqueUsername          |             `string`              |                                                                                                                           |
| unreadCompanyMessages   |             `number`              |                                                                                                                           |
| unreadMessages          |             `number`              |                                                                                                                           |
| views                   |             `number`              |                                         The number of time the company was viewed                                         |

## Company Mailing Info

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| city             |              `string`               |                                                        |
| line1             |              `string`               |                                                                               |
| line2 |              `string`               |                                |
## Company Address Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| address             |              `string`               |                                      The full address of the company.                                      |
| addressLastUpdated             |              `Timestamp`               |                                         When last the company address has been updated.                                         |
| location |              `GeoPoint`               |                   The coordinates of the company address.                   |
| streetName          |              `string`               |                                        A shortened version of the company address.   
| buildingNumber          |              `string`               |                                        The company's building number.   

## Delivery Window Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| closingTime             |              `Timestamp`               |                                      The time the company closes for business on this day.                                      |
| day             |              `string`               |                                         The day of the week.                                         |
| eveningPickup |              `bool`               |                   True if the company facilitates evening delivery.                   |
| eveningPickupCutoffTime          |              `Timestamp`               |                                        The time a shopper must place an order by to have access to evening pickup for that day.   
| label          |              `string`               |                                        A letter representation label of the day of the week.   
| morningPickup          |              `bool`               |                                        True if the company facilitates morning delivery.   
| morningPickupCutoffTime          |              `Timestamp`               |                                        The time a shopper must place an order by to have access to morning pickup for that day.   
| open          |              `bool`               |                                        True if the company facilitates deliveries on this day.   
| openingTime          |              `Timestamp`               |                                        The time the company opens for business on this day.   
## Opening Days Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| closingTime             |              `Timestamp`               |                                      The time the company closes for business on this day.                                      |
| day             |              `string`               |                                         The day of the week.                                         |
| label          |              `string`               |                                        A letter representation label of the day of the week.   
| open          |              `bool`               |                                        True if the company is open for business on this day.   
| openingTime          |              `Timestamp`               |                                        The time the company opens for business on this day.   

## Update Data Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| cashAmount          |              `number`              |                                        The amount of cash the shopper is paying with, entered at checkout.   
| deliveryAddress          |              `object`              |                                        An object representing the user address.   
| deliveryFee             |              `number`               |                                      The cost of delivery.                                      |
| deliveryWindow             |              `dddd Do MMMM`            |            The selected date for delivery in string format  |
| requestedBy          |              <code>Business &#124; Shopper</code>               |        Whoever requested the reschedule or change to the order.   
| timeWindow          |              `string`               |                                        Whether this order will be delivered as part of the morning or evening shift.   
| total          |              `bool`               |                                        The total cost of the order including delivery, addons and variations.   

## Company Variation Properties

`Path: /companies/{companyId}/variations/{variationId}`

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| freeSelections             |              `number`               |                                      The number of selections that can be made before a cost is applied                                      |
| maximumToSelect             |              `number`               |                                         The maximum number of options a user can select. 
| minimumToSelect             |              `number`               |                                         The minimum number of options a user must select. 0 means unlimited.  
| options             |              `string`               |                                         A string representation of the options for this variation group 
| title             |              `string`               |                                         The title of this variation.

## Option Properties
`Path: /companies/{companyId}/variations/{variationId}/options/{optionId}`

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| active             |              `bool`               |                                      True if the option is active and should be shown.                                      |
| name             |              `string`               |                                         The name of the option.
| order             |              `number`               |                                         The position of this option in the list.
| price             |              `number`               |                                         The additional price of the option.

## Verification Document Properties
`Path: /companies/{companyId}/verification/{verificationId}`

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| companyId             |              `string`               |                                      The company ID.                                      |
| createdAt             |              `Timestamp`               |                                         When the document was uploaded
| label             |              `string`               |                                         The label of the document.
| processing             |              `bool`               |                                         True if the document is currently being reviewed and processed
| url             |              `string`               |                                         A url pointing to the uploaded document.
| verified             |              `bool`               |                                         True if the document has been verified.

## Company Product Category Properties
`Path: /companies/{companyId}/product-categories/{productCategoryId}`
| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| availableDays             |              `string`               |                                      The available days for this category's products.                                      |
| createdAt             |              `Timestamp`               |                                         When the category was created.
| count             |              `string`               |                                         The number of products in the category.
| isShowing             |              `bool`               |                                         True if the category is visible.
| order             |              `string`               |                                         The order of this category in the list.
| title             |              `bool`               |                                         The name of the category.

## Company Products
`Path: /companies/{companyId}/product-categories/{productCategoryId}/products/{productId}`

| Attribute                      |     Type      |                                                       Description                                                        |
| :----------------------------- | :-----------: | :----------------------------------------------------------------------------------------------------------------------: |
| id                             |   `string`    |                                                  The ID of the product                                                   |
| categoryId                     |   `string`    |                                          The categoryId the product belongs to                                           |
| categoryName                   |   `string`    |                                           The category the product belongs to                                            |
| createdAt                      |  `Timestamp`  | The timestamp of the product's creation.                                                                                                                         |
| description                    |   `string`    |                                          Short description of the product                                           |
| hasAddons                      |    `bool`     |                                             True if the product has add-ons                                              |
| hasVariations                  |    `bool`     |                                            True if the product has variations                                            |
| image                          |   `string`    |                                         URL of the featured/first product image                                          |
| inStock                        |    `bool`     |                                             The stock status of the product                                              |
| onSale                        |    `bool`     |                                             True if the product is on sale.                                              |
| order                          |   `number`    |                                           The position of the product in list                                            |
| packingTime                    | `packingTime` |                               A representation of how long it takes to prepare the product                               |
| price                          |    `float`    |  The price of the product.                                                                                                                        |
| purchases                      |   `number`    |                                     The number of times the product has been bought                                      |
| salePrice                      |   `number`    |                                              The sale price of the product                                               |
| stockCount                     |   `number`    |                               The quantity of products. `null` if not tracking stock count                               |
| title                          |   `string`    |                                                 The name of the category                                                 |
| trackStock                     |    `bool`     |                        True if tracking inventory. Orders of this product will reduce stock count                        |
| views                          |   `number`    |                                     The number of times the product has been viewed                                      |

## Create Company

Create a new company.

### Callable Function Name

`createCompany`

### HTTP Request

`POST /api/v1/companies`

### Body

| Parameter | Description                     |
| --------- | ------------------------------- |
| id        | The ID of the company to update |
| acceptsCard   |         True if the company accepts LINX/Debit payments                                      |
| acceptsCash   |          True if the company accepts cash payments     |
|acceptsPayouts| True if the company accepts online payments |
|acceptsPortableCard| True if the company accepts portable LINX/Debit payments. This must be true to enable LINX payments on a curbside order|
|deliveryFee| The cost of deliveries set by the store. Only applicable for stores offering Delivery and not on Unqueue's driver network|
|description| A short description of the company.|
|doesCurbside| True if the company facilitates curbside pickups.|
|doesDelivery| True if the company does Delivery as a pickup method. |
|doesWalkin| True if the company facilitates in store pickups|
|email| The email address of the company|
|emailVerified| True if the company's email address is verified.|
|logo| The URL of the company's logo.|
|name| The name of the company|
|ownerFirstName| The first name of the person running the company account.|
|ownerLastName| The last name of the person running the company account.|
|phone| The phone number of the company |
### Response

<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->

## Get Company

Retrieve details about a company.

### Callable Function Name

`getCompany`

### HTTP Request

`POST /companies`

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
| completed            |                `bool`                |            True if the order has been completed.                                                            |
| containsColdItems      |                `bool`                |                   True if the order contains cold items. Used as in indicator of whether to included ice packs or not.                                                    |
| count                |               `number`               |                   The number of items in the order                    |
| createdAt            |             `Timestamp`              |                      When the order was created.                      |
| customerEmail        |               `string`               |                          The shopper's email                          |
| customerLicense      |               `string`               |           The shopper's license plate, entered at checkout            |
| customerPhone        |               `string`               |                      The shopper's phone number                       |
| deliveryAddress      |               `object`               |                Saved from the associated user document                |
| deliveryFee          |               `number`               |           The cost of delivery.                                                            |
| deliveryWindow       |            `dddd Do MMMM`            |            The selected date for delivery in string format            |
| driverEnRoute        |                `bool`                |           True if the driver is on the way to the shopper to deliver the order.                                                            |
| onHiredDriverNetwork |                `bool`                |          True if this order is on the Unqueue Driver network          |
| orderNumber          |               `string`               |         A 4 digit number used to identify the order on pickup tags.                                                              |
| owner                |               `string`               |          The name of the shopper this order belongs to                                                             |
| ownerId              |               `string`               |          The userId this order belongs to                                                             |
| packed               |                `bool`                |      True if the items in the order are packed and ready for pickup or delivery.                                                                 |
| packedAt             |             `Timestamp`              |                        Automatically generated                        |
| packTimeInMinutes    |               `number`               |       The amount of minutes it will take to prepare this order.                                                                |
| paymentMethod        |      <code>Cash &#124; Credit Card &#124; Debit/Linx</code>               |                                                                       |
| pickupTimeDate       |            `bool/object`             |     False if shopper picking up ASAP. Object if it is a pre-order     |
| requiresPayment      |                `bool`                |    True if the order still needs to be paid for.                                                                   |
| source               |             <code>web &#124; app</code>             |                The platform the order was placed from                 |
| specialNotes         |               `string`               |          Special notes attached to the order by the shopper           |
| status               |               <code>pending &#124; claimed</code>               |                         Defaults to 'Pending'                         |
| storeAddress         |               `object`               |              Saved from the associated company document               |
| storeHours           |               `object`               |              Saved from the associated company document               |
| storeId              |               `string`               |              Saved from the associated company document               |
| storeLogo            |               `string`               |          The logo of the company this order was placed from           |
| storeName            |               `string`               |              Saved from the associated company document               |
| storePhone           |               `string`               |              Saved from the associated company document               |
| timeWindow           | <code>daytimeDelivery &#124; eveningDelivery</code> | Whether this order will be delivered as part of the morning or evening shift|                                                                       |
| total                |               `float`                | The total cost of the order including delivery, addons and variations |
| tripId                |               `string`                | The [Driver Trip](#driver-trip-properties) this order is a part of |
| tripOrder                |               `number`                | The position of this order in the [Driver Trip](#driver-trip-properties) |
| type                 |                <code>Delivery &#124; Curbside &#124; Walkin</code>               |                    The pickup method of the order                     |
| unavailableItems     |                `bool`                |   True if the company marked any of the items in the order as unavailable.                                                                    |
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

# Pack Times

<!-- The chats API allows you to create, view, and update individual chats. -->
## Pack Time Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| companyId                  |              `string`               |                                           The id of the company this order pack time belongs to. |
| orderCreatedAt               |            `Timestamp`            |                                            The timestamp of the order creation.                                             |
| orderPackedAt               |            `Timestamp`            |                                            The timestamp of when the order was packed.                                             |
| companyName              |            `string`             |                                     The name of the company this order pack time belongs to.                                      |
| id             |              `string`               |                             The unique ID of the pack time.                              |
| itemsInOrder            |         `Array`              | An array of the items that were in the order.
| orderId             |              `Timestamp`              | The unique ID of the order.
| packTime             |              `number`              | The pack time of the order in minutes. 


<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->
# Payees

<!-- The chats API allows you to create, view, and update individual chats. -->
## Payees Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| accountType                  |              `Unqueue Payouts`               |       Read only. |
| companyId                  |              `string`               |       The id of the company this payee belongs to. |
| bankAccountHolder                  |              `string`               |   The owner of the bank account. |
| bankAccountNumber                  |              `string`               |    The bank account number payments are made to. |
| createdAt               |            `Timestamp`            |       The timestamp of the payee creation.                                             |
| companyName              |            `string`             |   The name of the company this payee belongs to.                                      |
| bankName              |            `string`             |       The name of the banking institution.                                      |
| paymentSchedule              |            <code>Weekly &#124; Monthly</code>             |                                     The cycle which payments are sent at.                                      |
| id             |              `string`               |                             The unique ID of the payee.                              |
| verified             |              `number`              | True if the payee has been approved for Unqueue Payouts. 


<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->
# Products

The products API allows you to create, view, and update individual products.

## Product Properties

| Attribute                      |     Type      |                                                       Description                                                        |
| :----------------------------- | :-----------: | :----------------------------------------------------------------------------------------------------------------------: |
| id                             |   `string`    |                                                  The ID of the product                                                   |
| categoryAvailableDays          |    `Array`    |                               The available days object attached to the product's category                               |
| categoryId                     |   `string`    |                                          The categoryId the product belongs to                                           |
| categoryName                   |   `string`    |                                           The category the product belongs to                                            |
| categoryVisible                |    `bool`     |                                 True if the category this product belongs to is visible                                  |
| companyAcceptsCard             |    `bool`     |                                     True if the company accepts LINX/Debit payments                                      |
| companyAcceptsOrdersAfterHours |    `bool`     |                  True if the company accepts pre-orders. Shoppers can place orders after opening hours                   |
| companyAcceptsPayouts          |    `bool`     |                                       True if the company accepts online payments                                        |
| companyAcceptsPortableCard     |    `bool`     | True if the company accepts portable LINX/Debit payments. This must be true to enable linx payments on a curbside order  |
| companyCategories              |  `string[]`   |                                     An array of category Id's the company belongs to                                     |
| companyDeliveryFee             |   `number`    | The delivery cost set by the store. **Only** applicable for stores offering Delivery and not on Unqueue's driver network |
| companyDoesCurbside            |    `bool`     |                                        True if the company facilitates curbside pickups.                                         |
| companyDoesDelivery            |    `bool`     |                                  True if the company does Delivery as a pickup method.                                   |
| companyDoesWalkin              |    `bool`     |                                        True if the company does in store pickups                                         |
| companyId                      |   `string`    |                                          The company Id the product belongs to                                           |
| companyLogo                    |   `string`    |                                            A URL pointing to the company logo                                            |
| companyName                    |   `string`    |                                      The name of the company the product belongs to                                      |
| companyOnHiredDriverNetwork    |    `bool`     |                              True if the company is on Unqueue's Pre-order Delivery Network                              |
| companyVisible                 |    `bool`     |                                         True if the store is visible to shoppers                                         |
| createdAt                      |  `Timestamp`  | The timestamp of the product's creation.                                                                                                                         |
| description                    |   `string`    |                                          Short description of the product                                           |
| hasAddons                      |    `bool`     |                                             True if the product has add-ons                                              |
| hasVariations                  |    `bool`     |                                            True if the product has variations                                            |
| image                          |   `string`    |                                         URL of the featured/first product image                                          |
| inStock                        |    `bool`     |                                             The stock status of the product                                              |
| order                          |   `number`    |                                           The position of the product in list                                            |
| packingTime                    | `packingTime` |                               A representation of how long it takes to prepare the product                               |
| price                          |    `float`    |  The price of the product.                                                                                                                        |
| purchases                      |   `number`    |                                     The number of times the product has been bought                                      |
| salePrice                      |   `number`    |                                              The sale price of the product                                               |
| stockCount                     |   `number`    |                               The quantity of products. `null` if not tracking stock count                               |
| title                          |   `string`    |                                                 The name of the category                                                 |
| trackStock                     |    `bool`     |                        True if tracking inventory. Orders of this product will reduce stock count                        |
| views                          |   `number`    |                                     The number of times the product has been viewed                                      |
| visible                        |    `bool`     |                                       True if the product should be shown to users                                       |

## Create Product

Create a new product.

### Callable Function Name

`createProduct`

### HTTP Request

`POST /createProduct`

### Body

| Parameter | Description                     |
| --------- | ------------------------------- |
| id        | The ID of the product to create |

### Response

<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->

## Get Product

Retrieve details about a product.

### Callable Function Name

`getProduct`

### HTTP Request

`POST /getProduct`

### Body

| Parameter | Description                       |
| --------- | --------------------------------- |
| id        | The ID of the product to retrieve |

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

## Update Product

Update a product with new details.

### Callable Function Name

`updateProduct`

### HTTP Request

`POST /updateProduct`

### Body

| Parameter | Description                     |
| --------- | ------------------------------- |
| id        | The ID of the product to update |

### Response

<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->

# Driver Trips

The driver-trips API allows you to create, view, and update individual trips.

## Driver Trip Properties

| Attribute           |                                         Type                                          |                     Description                      |
| :------------------ | :-----------------------------------------------------------------------------------: | :--------------------------------------------------: |
| cashToCollect       |                                        `float`                                        | The total cash the driver has to collect on the trip |
| completed           |                                        `bool`                                         |              True if the trip has ended              |
| count               |                                       `number`                                        |           The count of orders in this trip           |
| createdAt           |                                      `Timestamp`                                      |              When the trip was created               |
| driver              |                                       `Driver`                                        |              When the trip was created               |
| driverId            |                                       `string`                                        |      The ID of the driver assigned to the trip       |
| driverTripEarnings  |                                       `number`                                        | The amount of money a driver will make on this trip  |
| orders              |                                       [Order[]](#order-properties)                                       |                          -                           |
| status              | <code>pending &#124; assigned &#124; ongoing &#124; completed &#124; cancelled</code> |                The status of the trip                |
| tripDuration        |                                       `number`                                        |       The total length of the trip in minutes        |
| tripEarnings        |                                        `float`                                        |                          -                           |
| tripLength          |                            <code>short &#124; long</code>                             |         A representation of the trip length          |
| tripNumber          |                                       `string`                                        |      A 5-digit number for referencing the trip       |
| unqueueTripEarnings |                                       `string`                                        |  The amount of money Unqueue will make on this trip  |

## Create Driver Trip

Create a new driver-trip.

### Callable Function Name

`createDriverTrip`

### HTTP Request

`POST /createDriverTrip`

### Response

```json
{
  "success": true,
  "tripId": "abc123"
}
```

<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->

## Get Driver Trip

Retrieve details about a driver-trip.

### Callable Function Name

`getDriverTrip`

### HTTP Request

`POST /getDriverTrip`

### Body

| Parameter | Description                           |
| --------- | ------------------------------------- |
| id        | The ID of the driver-trip to retrieve |

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

# Discount Codes

The discount-codes API allows you to create, view, and update individual discount-codes.

## Discount Code Properties

| Attribute |                 Type                 |                                    Description                                     |
| :-------- | :----------------------------------: | :--------------------------------------------------------------------------------: |
| active    |                `bool`                |                        True if the code is enabled for use                         |
| code      |               `string`               |                      The discount code that users will enter                       |
| companyId |               `string`               |                     The companyId the discount code belongs to                     |
| createdAt |             `Timestamp`              |                         When the discount code was created                         |
| id        |               `string`               |                         The unique ID of the discount code                         |
| name      |               `string`               |                      A description of the purpose of the code                      |
| type      | <code>percentage &#124; value</code> | The method of applying the discount, varies between a percentage and a fixed value |
| updatedAt |             `Timestamp`              |                           When the code was last updated                           |
| uses      |               `number`               |                     The number of times the code has been used                     |
| value     |               `number`               |                       The actual value of the discount code                        |


<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->

# Ratings

<!-- The chats API allows you to create, view, and update individual chats. -->
## Rating Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| companyId |               `string`               |                     The companyId the rating belongs to                     |
| userId |               `string`               |                     The userId the rating belongs to                     |
| createdAt               |            `Timestamp`            |       The timestamp of the rating creation.                                             |
| rating              |            `number`             |   The value of the rating.                                      |

<!-- ////////////////////////////////////////////////////////////////////////////////
// END SECTION
//////////////////////////////////////////////////////////////////////////////// -->

# Users

<!-- The chats API allows you to create, view, and update individual chats. -->
## User Properties

| Attribute               |               Type                |                                                        Description                                                        |
| :---------------------- | :-------------------------------: | :-----------------------------------------------------------------------------------------------------------------------: |
| createdAt               |            `Timestamp`            |       The timestamp of the user creation.                                             |
| email                  |              `string`               |       The user's email address. |
| expoToken                  |              `string`               |       The user's push notification token. |
| firstName                  |              `string`               |   The user's first name. |
| lastName                  |              `string`               |    The user's last name. |
| phoneNumber              |            `string`             |   The user's phone number.                                      |
| id             |              `string`               |                             The unique ID of the user.                              |

# Types

## Company Address

> Company Address Example

```json
  "storeAddress": {
      "address": "Some address"
      "addressLastUpdated": "FirebaseFirestore.Timestamp"
      "buildingNumber": "string"
      "location": "FirebaseFirestore.GeoPoint"
      "streetName": "string"
  }
```

| Attribute               |               Type                    |
| :---------------------- | :-------------------------------: |
| address               |            `string`            | 
| addressLastUpdated                  |              `Timestamp`               |  
| buildingNumber                  |              `string`               |  
| location                  |              `GeoPoint`               | 
| streetName                  |              `string`               |   

