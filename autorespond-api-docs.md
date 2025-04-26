# Autorespond REST API

## Rest API for Autorespond

* Version: 1.0.0

## Table of Contents
- [Administration](#administration)
- [ListManagers](#listmanagers)
- [Orders](#orders)
- [Relations](#relations)
- [Tags](#tags)

## Administration

### Get API Version

Get the current version of the API.

```
https://api.e-act.nl/api/1.0/version
```

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| version | String | The current version of the API |

### Get All Fields

Get all defined fields within an administration, both free fields as standard fields.

```
https://api.e-act.nl/api/1.0/fields
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| fields | Object | [ { code, name, type, options[] } ] |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Get All Tags

Get all defined tags within an administration.

```
https://api.e-act.nl/api/1.0/tags
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| tags | Object | [ { id, name } ] |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Load Admin

Load an administration with the given id.

```
https://api.e-act.nl/api/1.0/admins/{id}
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| id | Number | ID of admin to fetch |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| admin | Object | { company_id, accessCode, serviceLevel, locked, adminName, adminEmail} |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

## ListManagers

### Show Listmanagers

Returns a complete list of listmanagers within an administration.

```
https://api.e-act.nl/api/1.0/listmanagers
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| list | Object | List of listmanagers [ { id, name, category, code, groupId } ] |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Start Listmanager with GDPR Data

Start a listmanager for the given relation including GDPR consent (new EU privacy regulations).

```
https://api.e-act.nl/api/1.0/listmanagers/{listId}/gdpr_subscribe
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| listId | Number | id of listmanager to start |
| relId | Number | id of relation for whom the listmanager is started |
| skipOptin | String | if set to 'Y', skip the optin step |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |
| privacyText | String | text of privacy remark on the form |
| privacyAgreement | String | 'Y' or 'N' if relation agrees with privacy statement |
| privacyUrl | String | link to privacy statement as used in the form |
| consentText | String | text of consent remark on the form |
| consentAgreement | String | 'Y' or 'N' if relation agrees with consent text |
| ip | String | address of relation that submitted the form |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| TRUE | Boolean | if action succeeded. |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Start Listmanager

Start a listmanager for the given relation.

```
https://api.e-act.nl/api/1.0/listmanagers/{listId}/subscribe
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| listId | Number | id of listmanager to start |
| relId | Number | id of relation for whom the listmanager is started |
| skipOptin | String | if set to 'Y', skip the optin step |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| TRUE | Boolean | if action succeeded. |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Stop Listmanager

Stop a listmanager for the given relation. Note that this only removes from associated groups, creates an unsubscribe event and removes planned emails.

```
https://api.e-act.nl/api/1.0/listmanagers/{listId}/unsubscribe
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| listId | Number | id of listmanager to stop |
| relId | Number | id of relation for whom the listmanager is started |
| reason | String | reason to stop - will be added as 'contact' with the relation |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| TRUE | Boolean | if action succeeded. |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

## Orders

### End Existing Subscription

End an existing subscription with a given date.

```
https://api.e-act.nl/api/1.0/orders/subscriptions/{id}/end
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| endDate | Date | date that the subscription should end. Use format 'DD-MM-YYYY' |
| id | Number | of the existing subscription |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| result | Boolean | code |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Get PDF invoice for Given Invoice Number

Get PDF invoice for Given Invoice Number.

```
https://api.e-act.nl/api/1.0/invoices/{invoiceNumber}
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| invoiceNumber | String | the invoice number for which the PDF must be retrieved |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| Invoice | Object | PDF file (application/pdf) |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Show Individual Invoice

Get invoice details for the provided number. Credit invoice is not supported.

```
https://api.e-act.nl/api/1.0/invoice/{invoiceNumber}
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| invoiceNumber | String | the number of the requested invoice |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| Invoice | Object | details { lines: [ { discount, sku, description, quantity, amount, vatamount, vatpercentage, ledger } ], orderId, billingId, relationEmail, relationId, invoiceNumber, invoiceDate, isCreditInvoice, amountIncl, amountExcl, amountVat, fullName, address, postalCode, city, country, btwNummer, company } ] |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message |

### Show Invoices

Get invoices and credit invoices for the given period of time.

```
https://api.e-act.nl/api/1.0/invoices
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| dateFrom | String | use this to select all (credit and normal) invoices that are created AFTER this date. Use format 'YYYY-MM-DD' |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| List | Object | of invoices [ { relationEmail, invoiceNumber, description, invoiceDate, isCreditInvoice, amountIncl } ] |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message |

### Show Orders for Given Relation

Get all orders for the given relation.

```
https://api.e-act.nl/api/1.0/orders/relation/{id}
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| id | Number | the id of the relation for which orders must be collected |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| List | Object | of orders [ { orderId, invoiceNumber, orderlines [ {lineType, productId, productName, quantity, subscriptionId, subscriptionBilledUntil, subscriptionEndsAt } ], purchaseDate, paid, email } ] |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Show Orders

Get paid and/or non-paid orders for the given period of time.

```
https://api.e-act.nl/api/1.0/orders
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| paid | String | use 'Y' for paid orders, use 'N' for unpaid orders, use '-' for paid and non-paid orders (not required) |
| hours | Number | time-period, e.g. use 24 for all orders of the past 24 hours |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| List | Object | of orders [ { orderId, relationId, relationName, relationEmail, invoiceNumber, orderlines [ {lineType, productId, productName, quantity, subscriptionId, subscriptionBilledUntil, subscriptionEnds } ], purchaseDate, paid } ] |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message |

## Relations

### Add Relation To group

Add a relation to a group. If the relation is already member of the group, no action is taken.

```
https://api.e-act.nl/api/1.0/group/{grpId}/member/:relId
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| grpId | Number | id of the group |
| relId | Number | id of the relation to add |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| result | Boolean | code |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message |

### Create New Free Field within an Administration

Create a new free field. The provided fieldName must be unique.

```
https://api.e-act.nl/api/1.0/field
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| fieldName | String | A unique name of the field (only a..Z characters or underscore, no spaces, length < 60) |
| fieldLabel | String | Label of the field shown in the administration |
| fieldType | String | Use one of these values: [boolean,string,list] |
| fieldOptions | String | If the type is 'list', provide a comma separated list of values (total length < 2048) |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| id | Number | of created field |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Create or Update Relation

Create a new relation if the email is not known in the administration. Otherwise update the relation.

```
https://api.e-act.nl/api/1.0/relation
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| email | String | email address for relation to create. If a relation with this email already exists, the other fields are used to update the relation |
| firstName | String | first name for relation (not required) |
| suffix | String | suffix for relation (not required) |
| lastName | String | last name for relation (not required) |
| gender | String | relation gender, use M (male) or F (female) or - (not required) |
| type | String | 1-character relation type (not required) |
| password | String | relation password, must be minimal 6 and max 20 characters long (not required) |
| customer | String | flag indicating if the relation should be activated as customer in the system (not required). Values: 'y' or 'n' |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| relation | Object | { id, firstName, suffix, lastName, email, funnelState, gender } |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Get All Groups

Get all groups within an administration.

```
https://api.e-act.nl/api/1.0/groups
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| groups | Object | [ { id, title } ] |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Get Relations in Group

Get all relations that are member of the given group.

```
https://api.e-act.nl/api/1.0/groups/{grpId}/relations
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| grpId | Number | id of the group |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| relations | Object | [ { id, firstName, suffix, lastName, email, funnelState, gender } ] |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Load Relation by Email

Returns a relation details object for a given email address.

```
https://api.e-act.nl/api/1.0/relation
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| email | String | emailaddress of relation to search for |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| relation | Object | { id, firstName, suffix, lastName, email, funnelState, gender } |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Load Relation by Id

Returns a relation details object for a given id.

```
https://api.e-act.nl/api/1.0/relation/{id}
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| id | Number | id of relation to load |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| relation | Object | { id, firstName, suffix, lastName, email, funnelState, gender } |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Remove Relation From group

Remove a relation from a group. If the relation is not member of the group, no action is taken.

```
https://api.e-act.nl/api/1.0/group/{grpId}/member/{relId}
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| grpId | Number | id of the group |
| relId | Number | id of the relation to remove |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| result | Boolean | code |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Show subscriptions

Returns a list of listmanager-id's for which the given relation subscribed and/or unsubscribed.

```
https://api.e-act.nl/api/1.0/relation/{id}/subscriptions
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| id | Number | the id of the relation |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| List | Object | of (un)subscriptions [ { campaignId, relationId, subscribedFlag (U or S), eventDate } ] |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Update Relation Email

Update the email address of an existing relation.

```
https://api.e-act.nl/api/1.0/relation/{id}/email
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| newemail | String | new email address for the existing relation |
| id | Number | of the existing relation |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| result | Boolean | code |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

## Tags

### Add Tag To Relation with given email

Add a tag to a relation with the given email address. If the tag is already associated to the relation, no action is taken.

```
https://api.e-act.nl/api/1.0/relation/addtag/{tagId}
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| tagId | Number | id of the tag to add |
| email | String | address of the relation |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| status | String | ok |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Add Tag To Relation

Add a tag to a relation. If the tag is already associated to the relation, no action is taken.

```
https://api.e-act.nl/api/1.0/relation/{relId}/addtag/{tagId}
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| relId | Number | id of the relation |
| tagId | Number | id of the tag to add |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| result | Boolean | code |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Remove Tag From Relation

Remove a tag from a relation. If the tag was not associated to the relation, no action is taken.

```
https://api.e-act.nl/api/1.0/relation/{relId}/removetag/{tagId}
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| relId | Number | id of the relation |
| tagId | Number | id of the tag to remove |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| result | Boolean | code |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Set a Free field For a Relation

Assign a free field to a relation. If the field is already associated to the relation, the value is updated.

```
https://api.e-act.nl/api/1.0/relation/{relId}/setfield
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| relId | Number | id of the relation |
| fieldCode | String | code of the free field to add or update |
| fieldValue | String | the new value the field should be set to |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| result | Boolean | code |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

### Show tags for relation

Returns a list of tags that are associated with the given relation.

```
https://api.e-act.nl/api/1.0/relation/{id}/tags
```

#### Parameters

| Field | Type | Description |
| --- | --- | --- |
| id | Number | the id of the relation |
| admin | Number | administration id of caller (used as authentication) |
| key | String | administration API access key of caller (used as authentication) |

#### Success Response (200)

| Field | Type | Description |
| --- | --- | --- |
| Array | String | List of of tagnames |

#### Error Response (4xx)

| Name | Description |
| --- | --- |
| error | An error message. |

---

Document generated on 2023-04-12T04:32:50.249Z