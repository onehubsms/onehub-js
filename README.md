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
var addContactURL     = "https://api.braceafrica.com/v1/contacts/add";

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
var editContactURL    = "https://api.braceafrica.com/v1/contacts/edit/" + contactId;


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
var fetchContactURL     = "https://api.braceafrica.com/v1/contacts/fetch";

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
var deleteContactURL    = "https://api.braceafrica.com/v1/contacts/delete";

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


