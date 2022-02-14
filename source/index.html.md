---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  # - <a href='#'>Sign Up for a Developer Key</a>
  # - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true
server: https://bulkdev.swifttdial.com:2778
meta:
  - name: description
    content: Documentation for the Kittn API
---

# swifttdial SMS API Docs

Customer Support:
tech@swifttdial.com
URL: https://swifttdial.com/contact-us/

## Usage Overview

Here are some information that should help you understand the basic usage of our Restful API.

Including info about authenticating users, making requests, responses, potential errors, query parameters and more.

## Headers

Certain API calls require you to send data in a particular format as part of the API call.

| Header        | value sample      | when to apply                                                     |
| ------------- | ----------------- | ----------------------------------------------------------------- |
| content-Type  | application /json | must be sent whn passing Data                                     |
| authorization | x-api-key         | MUST be sent whenever the endpoint requires (Authenticated User). |

## Responses

Unless otherwise specified, all of API endpoints will return the information that you request in the JSON data format.

```
json

```

`code`

`
Standard Response Format

Delivery Reports
Below is a description of each delivery report

| Status                 | Description                                                                                                                                                                                                                                                                          |     |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --- |
| DeliveredToTerminal    | Delivered to device                                                                                                                                                                                                                                                                  |
| AbsentSubscriber       | Subscriber has not been able to connect to the network for the last 24 hrs. In some cases (airtel) customers have to lock their phone to 3G only to be able to receive messages. This is an issue specific to them                                                                   |
|                        |
| Delivery Impossible    | Number has been ported to another telco or has temporarily been deactivated by SP. Or the number has been inactive for a long period of time. In some cases the telco has blocked delivery due to violation of policy. ie. Sending marketing message beyond 6PM and earlier than 7am |
| SenderName Blacklisted | The customer has explicitly blocked messages from the sender id. or opted out of receiving promotional messages                                                                                                                                                                      |
| Invalid Source Address | The sender ID does not exist on the telco                                                                                                                                                                                                                                            |

# Authentication

This endpoint is used to get an authorization token from the server. The token will be used to authenticate requests to protected endpoints

# Send Bulk Sms|

Send Bulk Promotional or/and Transaction messages|

#### Send a single message to one or multiple recipients ** Acquire API KEY FROM DASHBOARD **

| Parameter     | Description                    |     |
| ------------- | ------------------------------ | --- |
| AUTHORIZATION | x-api-key                      |
| HEADERS       | Content-Type: application/json |
| data          | profile_code :123              |

> https://bulkdev.swifttdial.com:2778

# Send Bulk

### POST

Send SMS

`POST` `https://bulkdev.swifttdial.com:2778/api/outbox/create \ `

Send a single message to one or multiple recipients. You can send up to 200 recipients in a single request. This endpoint can send both on demand and bulk messages.

| Parameter           | Description                               |
| ------------------- | ----------------------------------------- |
| AUTHORIZATIONS:     | X-api-key                                 |
| REQUEST BODY SCHEMA | application/json                          |
| REQUEST BODY:       |
| profile_code        | linked to sms product configuration       |
| Messages            | Arry of objects(Messages)[ 1 .. 20] items |
| dlr_callback_url    | dlr Callback Url                          |

###Requests

<details>
  <summary><b><u>Responses ` 200 ok</u></b></summary>

###Responses ` 200 ok`

| Parameter    | Description        |
| ------------ | ------------------ |
| external_id: | Message Id.        |
| message_ref  | Message Reference. |
| recipient:   | Mobile Number.     |
| sms_count    | Sms Count.         |

</details>

<details>

<summary>Intro:</summary>

#### Sub intro

[
{
"external_id": "tStriug0Usdecwc4xu12sczeepo99ge45xh0556xordguiyh",
"recipient": "254780011971",
"sms_count": 1
}
]

</details>

`422 unprocesable Entity`

| Parameter      | Description  |
| -------------- | ------------ |
| code (string): | error code   |
| description    | Description. |
| detail:        | Detail.      |

`500 Internal Server Error`

| Parameter      | Description  |
| -------------- | ------------ |
| code (string): | error code   |
| description    | Description. |
| detail:        | Detail.      |

```shell
curl --request POST \
  --url https://bulkdev.swifttdial.com:2778/api/outbox/create \
  --header 'Content-Type: application/json' \
  --header 'X-API-Key: meowmeowmeow' \
  --data '{"profile_code": "12345",
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

# Message Status

`https://bulkdev.swifttdial.com:2778/api/outbox/delivery-status/message_ref/ \`

Check the delivery status of a single/Bulk messages

| Parameter       | Description |
| --------------- | ----------- |
| AUTHORIZATIONS: | X-api-key   |

```
curl --request GET \
 --url https://bulkdev.swifttdial.com:2778/api/outbox/delivery-status/message_ref/ \
 --header 'X-API-Key: your-api-key'
```

# Subscription Messages

### `https://bulkdev.swifttdial.com:2778/api/outbox`

| Parameter        | Description                                                                                  |
| ---------------- | -------------------------------------------------------------------------------------------- |
| to               | An arraray of phone numbers                                                                  |
| message          | he message to be sent a single massage is 160 characters                                     |
| from:            | The short code that will be used to send the message                                         |
| profile_code     | linked to sms product configuration                                                          |
| message_id       | A unique reference number that will be sent back to you on the provided delivery endpoint    |
| dlr_callback_url | The Url that we will send you a delivery report once the message is terminated to the device |

###Requests

| Parameter           | Description      |
| ------------------- | ---------------- |
| AUTHORIZATIONS:     | X-api-key        |
| REQUEST BODY SCHEMA | application/json |

header 'X-API-Key: your-x-api' \
 header 'Content-Type: application/json' \

```json

body
{
    "to": ["25472xxxxxxx"],
    "message": "Your Message",
    "messageId": "a-eunique-id",
    "from": "23599",
    "service": "23599_News_5/sms"
    "callback": "http://example.com/callback"

}
```

```shell
curl --request POST \
  --url https://bulkdev.swifttdial.com:2778/api/outbox \
  --header 'Content-Type: application/json' \
  --header 'X-API-Key: your-x-api' \
  --data '{
    "to": ["25472xxxxxxx"],
    "message": "Your Message",
    "messageId": "a-eunique-id",
    "from": "23599",
    "service": "23599_News_5/sms",
    "callback": "http://example.com/callback"

}'
```

# My Title

    ## My Subtitle

    ```csharp
        Code snippet
    ```

    ```java
        Code snippet
    ```

    ```php
    <?php
        Code snippet
    ?>
    ```

    ```ruby
    #Code snippet
    ```
