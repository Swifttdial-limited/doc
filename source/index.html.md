---
title: SwifttDial API DOcs

# language_tabs: # must be one of https://git.io/vQNgJ
#   - shell
#   - ruby
#   - python
#   - javascript

toc_footers:
  - <a href='https://sms.swifttdial.com'>Login</a>
  # >

includes:
  - dlrstatuses
  - errors

search: true

code_clipboard: true
server: https://sms.api.swifttdial.com:2778
meta:
  - name: description
    content: SwifttDial Bulk sms API Docs
---

# Usage Overview

SwifttDial SMS API Docs

Customer Support:
tech@swifttdial.com
URL: https://swifttdial.com/contact-us/

Here are some information that should help you understand the basic usage of our Restful API.

Including info about authenticating users, making requests, responses, potential errors, query parameters and more.

# Headers

Certain API calls require you to send data in a particular format as part of the API call.

| Header        | value sample      | when to apply                                                     |
| ------------- | ----------------- | ----------------------------------------------------------------- |
| Content-Type  | application /json | must be sent whn passing Data                                     |
| Authorization | x-api-key         | MUST be sent whenever the endpoint requires (Authenticated User). |

# Authentication

This endpoint is used to get an authorization token from the server. The token will be used to authenticate requests to protected endpoints

<aside>* Acquire API KEY FROM DASHBOARD **
</aside> 
```shell
https://bulkdev.swifttdial.com:2778/api/outbox/create
header 'Content-Type: application/json' \
header 'X-API-Key: your-api-key you generate from the dashboard' \
```

| Parameter     | Description                    |     |
| ------------- | ------------------------------ | --- |
| AUTHORIZATION | x-api-key                      |
| HEADERS       | Content-Type: application/json |
| data          | profile_code :12356            |

# Send Bulk

### POST

Send SMS

```shell
Request body
{
  "profile_code": "12345",
	"messages": [
		{
			"recipient": "25472xxxxxxx",
			"message": " HI this is a Test",
			"message_type":1,
			"req_type": 1,
			"external_id": "tStriug0Usdecwc4xu12sczeepo99ge45xh0556xordguiyh"
		}
	],
	"dlr_callback_url": "http://example.com"
}

```

`POST` `https://bulkdev.swifttdial.com:2778/api/outbox/create \ `

```shell

curl --request POST \
  --url https://bulkdev.swifttdial.com:2778/api/outbox/create \
  --header 'Content-Type: application/json' \
  --header 'X-API-Key: meowmeowmeow' \
  --data '{
    "profile_code": "12345",
	"messages": [
		{
			"recipient": "254712xxxxxx",
			"message": " HI this is a test",
			"message_type":1,
			"req_type": 1,
			"external_id": "your unique external_id"
		}
	],
	"dlr_callback_url": "http://example.com"
}
```

Send a single message to one or multiple recipients. You can send up to 200 recipients in a single request. This endpoint can send both on demand and bulk messages.

| Parameter           | Description                               |
| ------------------- | ----------------------------------------- |
| AUTHORIZATIONS:     | X-api-key                                 |
| REQUEST BODY SCHEMA | application/json                          |
| REQUEST BODY:       |
| profile_code        | linked to sms product configuration       |
| Messages            | Arry of objects(Messages)[ 1 .. 20] items |
| dlr_callback_url    | dlr Callback Url                          |

<!-- ###Requests -->

##Responses
` 200 ok`

```shell
200 ok {
"external_id": "tStriug0Usdecwc4xu12sczeepo99ge45xh0556xordguiyh",
"recipient": "254780011971",
"sms_count": 1
}
```

| Parameter    | Description        |
| ------------ | ------------------ |
| external_id: | Message Id.        |
| message_ref  | Message Reference. |
| recipient:   | Mobile Number.     |
| sms_count    | Sms Count.         |

```shell
401 Unauthorized
{
"code": "description",
}
```

`401 Unauthorized`

| Parameter      | Description |
| -------------- | ----------- |
| code (string): | Description |

```shell
403 Forbidden
{

"code": "details",
}
```

`403 Forbidden`

| Parameter      | Description |
| -------------- | ----------- |
| code (string): | Description |

```shell
422 unprocesable Entity
{
  "detail": "Invalid Profile Code"
}
```

`422 unprocesable Entity`

| Parameter      | Description |
| -------------- | ----------- |
| code (string): | Description |

```shell
500 Internal Server Error
{
  "detail": "500 server-error",
}
```

`500 Internal Server Error`

| Parameter      | Description |
| -------------- | ----------- |
| code (string): | description |

## GET DLR

GET MESSAGE DELIVERY

`GET https://bulkdev.swifttdial.com:2778/api/outbox/delivery-status/message_ref/ \`

Check the delivery status of a single/Bulk messages

```shell
curl --request GET \
 --url https://bulkdev.swifttdial.com:2778/api/outbox/delivery-status/message_ref/ \
 --header 'X-API-Key: your-api-key'
```

| Parameter       | Description                                              |
| --------------- | -------------------------------------------------------- |
| AUTHORIZATIONS: | X-api-key                                                |
| message_ref     | This is the externalId generated when sending api outbox |

`Response 422 Unprocessable Entity`

```shell
 Body{
"detail": "Error Message"
}

```

<!--
## POST DLR Request

Web hook post

### `POST https://bulkdev.swifttdial.com:2778/api/outbox`

`Headers Body`

`Content-Type: application/json`

```shell
request Body
{
    "uid": "45$045ea8b3abf540aa89cac71985b3a278",
    "actor_type": "system",
    "event_type": "sms_delivery_status",
    "created_at": "1594868435",
    "data": {
        "external_id": "abf540aa89cac71985b3a278",
        "message_ref": "76387871a0bd4f44afcbf3af8fb53054",
        "status": "delivered",
        "status_reason": "delivered_to_terminal",
        "status_description": "Message Delivered to terminal"
    }
}
```

```shell
code sample

curl --request POST \
  --url https://bulkdev.swifttdial.com:2779/api/outbox/create \
     --header "Content-Type: application/json" \
     --data-binary '{
  "uid": "45$045ea8b3abf540aa89cac71985b3a278",
  "actor_type": "system",
  "event_type": "sms_delivery_status",
  "created_at": "1594868435",
  "data": {
    "external_id": "abf540aa89cac71985b3a278",
    "message_ref": "76387871a0bd4f44afcbf3af8fb53054",
    "status": "delivered",
    "status_reason": "delivered_to_terminal",
    "status_description": "Message Delivered to client Mobile"
  }
}' \

``` -->

# Subscription Messages

` POST https://bulkdev.swifttdial.com:2778/api/outbox/premium`

| Parameter        | Description                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------------- |
| to               | An arraray of phone numbers                                                                  |
| message          | he message to be sent a single massage is 160 characters                                     |
| from:            | The short code that will be used to send the message                                         |
| profile_code     | linked to sms product configuration                                                          |
| message_id       | A unique reference number that will be sent back to you on the provided delivery endpoint    |
| dlr_callback_url | The Url that we will send you a delivery report once the message is terminated to the device |

## MT/MO Messages

Send a single message to one or multiple recipients
###Requests

| Parameter           | Description      |
| ------------------- | ---------------- |
| AUTHORIZATIONS:     | X-api-key        |
| REQUEST BODY SCHEMA | application/json |

`POST` `https://bulkdev.swifttdial.com:2778/api/outbox/premium`

`header 'X-API-Key: your-x-api' \`

`header 'Content-Type: application/json' \`

```json
Request Body:
{
   "profile_code": "22021501",
   "messages": [
       {
           "mobile_number": "254791876624",
           "message": " HI this is a Test",
           "message_type":1,
           "req_type": 1,
           "external_id": "tStriug0Usdecwc4xu12sczeepo99ge45xh0556xordguiyh"
       }
   ],
   "dlr_callback_url": "https://posthere.io/77e1-4095-9dba"
}'
```

```shell
sample code

curl --location --request POST 'https://bulkdev.swifttdial.com:2778/api/outbox/premium' \
--header 'x-api-key: your x-api-key' \
--header 'Content-Type: application/json' \
--data-raw '{
   "profile_code": "123456",
   "messages": [
       {
           "mobile_number": "2547xxxxxxxx",
           "message": " HI this is a Test",
           "message_type":1,
           "req_type": 1,
           "external_id": "tStriug0Usdecwc4xu12sczeepo99ge45xh0556xordguiyh"
       }
   ],
   "dlr_callback_url": "https://posthere.io/77e1-4095-9dba"
}'
```
