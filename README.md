# Onehub Node JS Sending SMS Library
```Node JS
import fetch from 'node-fetch';

fetch('https://api.onehub.co.ke/v1/sms/send', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'x-api-user': 'API_USERNAME_HERE',
        'x-api-key': 'API_KEY_HERE'
    },
    body: JSON.stringify({
        'phoneNumbers': '+2547XXXXXXXX,+2547XXXXXXXX',
        'message': 'Hello Api!',
        'senderId': 'Onehub'
    })
});
```
# Username and API Key
You can get your username and API Key [here](https://dashboard.onehub.co.ke/account/0/user/signup).
# Request Body Parameters
`phoneNumbers` - `[Type: String]` `[Required]` - Phone numbers of the recipients in international format with the plus (+) sign. Multiple numbers should be comma-separated.

`Message` - `[Type: String]` `[Required]` - The message you want to send. Each message is counted as 160 characters long. Messages longer than 160 characters will be billed accordingly.

`Sender ID` - `[Type: String]` `[Required]` - A sender ID serves as a branding for outgoing messages, typically representing your company name. Your users will receive messages with your specified sender ID. You can apply for your sender ID on our [website](https://onehub.co.ke/).
# Response Body Parameters
## Response in case of successful sending of a message:
```json
{
    "0":{
        "country":"kenya",
        "cost":"KES 2.00",
        "success":[
            "+2547XXXYXXXX",
            "+2547XXXXXXXX"
        ]
    },
    "status":200,
    "message":"Message sent"
}
```
## Response in case a message fails:
```json
{
   "0":{
      "country":"kenya",
      "cost":"KES 1.00",
      "success":[
         "+2547XXXYXXXX"
      ],
      "failed":[
         "+2547XXXXXXXX"
      ]
   },
   "status":200,
   "message":"Message sent"
}
```
## Response in case of wrong credentials:
```json
{
    "status":401,
    "message":"Unauthorized"
}
```
# Onehub Node JS Add Contacts Library
```Node js
var request = require('request');

// authentication
var x_username       = ""
var x_apikey         = ""

// data
var params = {
    'name' : 'John Migo', // contact name
    'phone' : '+254711xxxxxx', // international format
    'tags' : 'developer,nairobi', // optional comma separated tags
    'groups': 'Nairobi Coding, Group 2' // optional groups to add contact
}

// endpoint
var addContactURL     = "https://api.onehub.co.ke/v1/contacts/add";

var headers = {
    'Content-Type' :  'application/json',
    'Content-Length' : params.length,
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: addContactURL,
    method: 'POST',
    headers: headers,
    form: params
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    console.log(body)
})
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Response Body Parameters
## Response in case of successful adding of a contact:
```json
{
    "status": 200,
    "message": "Contact added"
}
```
# Onehub Node JS Edit Contacts Library
```Node js
var request = require('request');

// authentication
var x_username        = ""
var x_apikey          = ""

// data
var params = {
    'name' : 'John New', // new contact name
    'phone' : '+254711xxxxxx', // new phonenumber - international format
    'tags' : 'Edited Tag 1, Edited Tag', // new tags - comma separated tags
    'groups': 'New Group1' // optional groups to link contact
}

// id of contact to edit: this can be gotten from the fetch contacts api
var contactId         = "1";

// endpoint
var editContactURL    = "https://api.onehub.co.ke/v1/contacts/edit/" + contactId;


var headers = {
    'Content-Type' :  'application/json',
    'Content-Length' : params.length,
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: editContactURL,
    method: 'POST',
    headers: headers,
    form: params
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    console.log(body)
})
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Response Body Parameters
## Response in case of successful adding of a contact:
```json
{
    "status": 200,
    "message": "Contact has been updated"
}
```
# Onehub Node JS Fetch Contacts Library
```Node js
var request             = require('request');

// authentication
var x_username          = ""
var x_apikey            = ""

// endpoint
var fetchContactURL     = "https://api.onehub.co.ke/v1/contacts/fetch";

var headers = {
    'Content-Type' :  'application/json',
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: fetchContactURL,
    method: 'GET',
    headers: headers
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    console.log(body)
})
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Response Body Parameters
## Response in case of successful fetching of a contact:
```json
{
    "status": 200,
    "contacts": [
        {
            "id": 2,
            "name": "Jane Mwaura",
            "phoneNumber": "+254712345678",
            "tags": "kenya,nairobi",
            "groups": [],
            "createdOn": "2019-12-02T00:00:00.000Z",
            "lastEditedOn": null
        }
    ]
}
```
# Onehub Node JS Delete Contacts Library
```Node js
var request = require('request');

// authentication
var x_username          = ""
var x_apikey            = ""

// id of contact to delete
var params = {
    "contactIds":[1,2,3,4]
}

// endpoint
var deleteContactURL    = "https://api.onehub.co.ke/v1/contacts/delete";

var headers = {
    'Content-Type' :  'application/json',
    'Accept' : 'application/json',
    'Content-Length' : params.length,
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: deleteContactURL,
    method: 'POST',
    headers: headers,
    form:params
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    console.log(body)
})
```
## ```!``` Please note that this will also remove the contact from all linked groups.
```json
{
    "contactIds": [1,2,3,4]
}
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` 

`phone` -	`[Type: String]` `[Required]` - Must be in international format.

`tags` - `[Type: String]`	`[Optional]` - A unique field to help group contacts e.g football,team,family.

`groups` - `[Type: String]`	`[Optional]` - This is a group name that the contacts will be added to. It must be an existing group.
# Onehub Node JS Create Group Library
```Node js
var request = require('request');

// authentication
var x_username       = ""
var x_apikey         = ""

// data
var params = {
    "name": "",
    "tags": "",
}

// endpoint
var addGroupURL     = "https://api.onehub.co.ke/v1/contacts/groups/add";

var headers = {
    'Content-Type' :  'application/json',
    'Content-Length' : params.length,
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: addGroupURL,
    method: 'POST',
    headers: headers,
    form: params
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    console.log(body)
})
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Onehub Node JS Edit Group Library
```Node js
var request = require('request');

// authentication
var x_username       = ""
var x_apikey         = ""

// data
var params = {
    "name": "",
}

var groupId = ""

// endpoint
var editGroupURL     = "https:/api.onehub.co.ke/v1/contacts/groups/edit/" + groupId

var headers = {
    'Content-Type' :  'application/json',
    'Content-Length' : params.length,
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: editGroupURL,
    method: 'POST',
    headers: headers,
    form: params
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    else{
        console.log(error)
    }
})
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful editing of a group:
```json
{
    "status": 200,
    "message": "Group has been updated"
}
```
# Onehub Node JS Fetch Group Library
```Node js
var request             = require('request');

// authentication
var x_username          = ""
var x_apikey            = ""

// endpoint
var fetchGroupsURL     = "https://api.onehub.co.ke/v1/contacts/groups/fetch";

var headers = {
    'Content-Type' :  'application/json',
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: fetchGroupsURL,
    method: 'GET',
    headers: headers
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    else{
        console.log(error)
    }
})
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful fetching of a group:
```json
{
    "status": 200,
    "groups": [
        {
            "groupId": 12,
            "groupName": "Kenzu Safaris",
            "createdOn": "2019-05-17T00:00:00.000Z",
            "contacts": []
        }
    ]
}
```
# Onehub Node JS Link Contacts To Group Library
```Node js
var request = require('request');

// authentication
var x_username       = ""
var x_apikey         = ""

// data
var params = {
    "contactIds": [1,2,3,4],
}

var groupId = ""

// endpoint
var addContactsToGroupURL     = "https://api.onehub.co.ke/v1/contacts/add/" + groupId

var headers = {
    'Content-Type' :  'application/json',
    'Content-Length' : params.length,
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: addContactsToGroupURL,
    method: 'POST',
    headers: headers,
    form: params
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    else{
        console.log(error)
    }
})
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful linking contacts to a group:
```json
{
    "status": 200,
    "message": "The contacts linked to group"
}
```
# Onehub Node JS Fetch Group Contacts Library
```Node js
var request             = require('request');

// authentication
var x_username          = ""
var x_apikey            = ""

var groupId = ""

// endpoint
var fetchGroupContactsURL = "https://api.onehub.co.ke/v1/contacts//groups/fetch/"+groupId

var headers = {
    'Content-Type' :  'application/json',
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: fetchGroupContactsURL,
    method: 'GET',
    headers: headers
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    else{
        console.log(error)
    }
})
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful fetching group contacts:
```json
{
    "groupId": 2536,
    "groupName": "Chama Ya Mama",
    "contacts": [
        {
            "id": 65,
            "name": "John Doe",
            "phoneNumber": "+2547xxx4578",
            "tags": "chairman"
        },
        {
            "id": 63,
            "name": "Pendo JM",
            "phoneNumber": "+2547xxy4597",
            "tags": "member"
        }
    ]
}
```
# Onehub Node JS Remove Group Contacts Library
```Node js
var request = require('request');

// authentication
var x_username       = ""
var x_apikey         = ""

// data
var params = {
    "contactIds": [1,2,3,4],
}

var groupId = ""

// endpoint
var deleteGroupContactsURL     = "https://api.onehub.co.ke/v1/contacts/delete"+groupId

var headers = {
    'Content-Type' :  'application/json',
    'Content-Length' : params.length,
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: deleteGroupContactsURL,
    method: 'POST',
    headers: headers,
    form: params
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    else{
        console.log(error)
    }
})
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful removing group contacts:
```json
{
    "status": 200,
    "message": "Contacts removed form group"
}
```
# Onehub Node JS Delete Groups Library
```Node js
var request             = require('request');

// authentication
var x_username          = ""
var x_apikey            = ""

var params = {
    "groupIds":[1,2,3,4]
}

// endpoint
var deleteGroupURL = "https://api.onehub.co.ke/v1/contacts/groups/delete"

var headers = {
    'Content-Type' :  'application/json',
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: deleteGroupURL,
    method: 'POST',
    headers: headers,
    form:params
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    else{
        console.log(error)
    }
})
```
# Request Body Parameters
`name` - `[Type: String]` `[Required]` - The group name.

`tags` - `[Type: String]`	`[Optional]` - These are tags in the contacts you want to link. The group will be formed and the contacts automatically linked to the group.
# Response Body Parameters
## Response in case of successful deleting groups:
```json
{
    "status": 200,
    "message": "4 groups have been deleted"
}
```
# Onehub Node JS Sender Ids Library
```Node js
var request             = require('request');

// authentication
var x_username          = ""
var x_apikey            = ""

// endpoint
var fetchSenderidsURL = "https://api.onehub.co.ke/v1/sms/senderIds/fetch"

var headers = {
    'Content-Type' :  'application/json',
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: fetchSenderidsURL,
    method: 'GET',
    headers: headers
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    else{
        console.log(error)
    }
})
```
# Response Body Parameters
## Response in case of successful fetching of Sender Ids:
```json
{
    "status": 200,
    "senderids": [
        {
            "sender_id": "BraceAfrica",
            "country": "Kenya",
            "status": "active"
        },
        {
            "sender_id": "JubaPay",
            "country": "Kenya",
            "status": "active"
        },
        {
            "sender_id": "Foleni",
            "country": "Uganda",
            "status": "active"
        }
    ]
}
```
# Onehub Node JS Fetch Account Balance Library
```Node js
var request             = require('request');

// authentication
var x_username          = ""
var x_apikey            = ""

// endpoint
var fetchBalanceURL = "https://api.onehub.co.ke/v1/billing/balance"

var headers = {
    'Content-Type' :  'application/json',
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: fetchBalanceURL,
    method: 'GET',
    headers: headers
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    else{
        console.log(error)
    }
})
```
# Response Body Parameters
## Response in case of successful fetching account balance:
```json
{
    "status": 200,
    "data": {
        "amount": 6080.11,
        "currency": "KES"
    }
}
```
# Onehub Node JS Fetch Account Statement Library
```Node js
var request             = require('request');

// authentication
var x_username          = ""
var x_apikey            = ""

// endpoint
var fetchStatementURL = "https://api.onehub.co.ke/v1/billing/topups"

var headers = {
    'Content-Type' :  'application/json',
    'Accept' : 'application/json',
    'x-api-user' : x_username,
    'x-api-key' : x_apikey
}

var options = {
    url: fetchStatementURL,
    method: 'GET',
    headers: headers
}

// the request and response
request(options, function (error, response, body) {
    if (!error && response.statusCode == 200) {
        // Print out the response body
        console.log(body)
    }
    else{
        console.log(error)
    }
})
```
# Response Body Parameters
## Response in case of successful fetching account statement:
```json
{
    "status": 200,
    "data": [
        {
            "id": 4155,
            "amount": "KES 500",
            "description": "Mpesa Code ML689276",
            "type": "MPESA",
            "date_created": "2019-12-22T14:38:44.000Z",
            "currency": "KES"
        }
        {
            "id": 4338,
            "amount": "KES 1100",
            "description": "Mpesa Code MJUYEO67M",
            "type": "MPESA",
            "date_created": "2019-12-22T14:38:44.000Z",
            "currency": "KES"
        }
        {
            "id": 4598,
            "amount": "KES 8000",
            "description": "Admin Top Up",
            "type": "Admin",
            "date_created": "2019-12-22T14:38:44.000Z",
            "currency": "KES"
        }
    ]
}
```


