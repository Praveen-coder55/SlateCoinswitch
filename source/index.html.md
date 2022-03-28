---
title: COINSWITCH API

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - ruby
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

# Introduction 

Financial Information eXchange (FIX) protocol is an electronic communications protocol initiated in 1992 for international real-time exchange of information related to the securities transactions and markets. You can use it to receive real-time market data from us and it's an alternative to WebSocket protocol.

You can use it for real-time order management and receiving execution reports from us, and it's an alternative to WebSocket protocol.

# Implemented Standards:

<ul>

<li><a href="https://www.fixtrading.org/standards/fix-4-4/">FIX.4.4</a></li>

</ul>

# Messages

All FIX messages are equipped with Standard Header and Trailer, below we will describe what is required in them in accordance with FIX 4.4, the standard that we use.

<h2>Standard Header</h2>

<table>
  <tr>						
    <th>Tag</th>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>8</td>
    <td>BeginString</td>
    <td>FIX.4.4</td>
  </tr>
  <tr>
    <td>9</td>
    <td>BodyLength</td>
    <td>Message length, in bytes, forward to the CheckSum <10> field</td>
  </tr>
  <tr>
    <td>35</td>
    <td>MsgType</td>
    <td>Defines message type</td>
  </tr>
  <tr>
    <td>49</td>
    <td>SenderCompID</td>
    <td>Assigned value used to identify message sender</td>
  </tr>
  <tr>
    <td>56</td>
    <td>TargetCompID</td>
    <td>Assigned value used to identify message receiver</td>
  </tr>
  <tr>
    <td>34</td>
    <td>MsgSeqNum</td>
    <td>Integer message sequence number. Reset on Logon, Logout and Disconnect.</td>
  </tr>
  <tr>
    <td>52</td>
    <td>SendingTime</td>
    <td>Time of message transmission always expressed in UTC (Universal Time Coordinated, also known as "GMT")</td>
  </tr>
</table>

<h2>Standard Trailer</h2>

<table>
  <tr>						
    <th>Tag</th>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>10</td>
    <td>CheckSum</td>
    <td>Three byte, simple checksum. Always the last field in a message, i.e. serves, with the trailing , as the end-of-message delimiter. Always defined as three characters</td>
  </tr>  
</table>

<h2>Logon</h2>

First message sent by the client to Coinswitch FIX Gateway after connection to initiate a FIX session. After successful authorization, server will respond with same message type and start delivering market data messages to you.

<table>
  <tr>						
    <th>Tag</th>
    <th>Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>49</td>
    <td>SenderCompID</td>
    <td>Your API key</td>
  </tr>  
  <tr>
    <td>56</td>
    <td>TargetCompID</td>
    <td>FIXSERVICE</td>
  </tr>
  <tr>
    <td>108</td>
    <td>HeartBtInt</td>
    <td>1 (seconds)</td>
  </tr>
  <tr>
    <td>98</td>
    <td>EncryptMethod</td>
    <td>0</td>
  </tr>
</table>

<h2>Logout</h2>

Message sent by any side to close established session. If received, should be sent back unchanged to confirm session termination.

<h2>Heartbeat</h2>

Message sent by any side after defined amount of seconds in communication silence.

# OEML API

Financial Information eXchange (FIX) protocol is an electronic communications protocol initiated in 1992 for international real-time exchange of information related to securities transactions and markets.

You can use it for real-time order management and receiving execution reports from us, and it's an alternative to WebSocket protocol.

<h2>Implemented Standards:</h2>

<ul>

<li><a href="https://www.fixtrading.org/standards/fix-4-4/">FIX.4.4</a></li>
<li><a href="https://www.fixtrading.org/standards/fix-5-0-sp-2/">FIX.5.0</a></li>
<li><a href="https://www.fixtrading.org/standards/session-level-specs/">FIX.1.1</a></li>

</ul>

<h2>Endpoint</h2>

Our sesssion configuration parameters:

<table>
  <tr>						
    <th>Parameter</th>
    <th>Value</th>
  </tr>
  <tr>
    <td>SocketConnectHost</td>
    <td>k8s-default-fixservi-d1b15c3482-9d59ea28701faacb.elb.ap-south-1.amazonaws.com</td>
  </tr>  
  <tr>
    <td>SocketConnectPort</td>
    <td>80</td>
  </tr>
  <tr>
    <td>HeartBtInt</td>
    <td>30 (seconds)</td>
  </tr>
  <tr>
    <td>SenderCompID</td>
    <td>Your API key</td>
  </tr>  
  <tr>
    <td>TargetCompID</td>
    <td>FIXSERVICE</td>
  </tr>
  <tr>
    <td>ResetOnLogon</td>
    <td>Y</td>
  </tr>
  <tr>
    <td>FileLogPath</td>
    <td>tmp</td>
  </tr>
  <tr>
    <td>DefaultApplVerID</td>
    <td>7</td>
  </tr>
</table>

<h2>Messages</h2>

This section will provide necessary documentation for the FIX protocol messages.

<h2>New Order Single</h2>

<table>
  <tr>						
    <th>FIX Field Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>ClOrdID</td>
    <td>The unique identifier of the order assigned by the client</td>
  </tr>
  <tr>
    <td>OrdType</td>
    <td>OEML supports only the LIMIT order type. Market orders don't have price protection, and because of that, they are not supported.</td>
  </tr>
  <tr>
    <td>Side</td>
    <td>Side of order.</td>
  </tr>
   <tr>
    <td>Symbol</td>
    <td>Exchange symbol</td>
  </tr>
  <tr>
    <td>Price</td>
    <td>Order price.</td>
  </tr>
  <tr>
    <td>OrderQty</td>
    <td>Order quantity</td>
  </tr>
  <tr>
    <td>TimeInForce</td>
    <td>Time in force is a special instruction used when placing a trade to indicate how long an order will remain active before it expires</td>
  </tr>
</table>

<h2>Order Cancel Request</h2>

<table>
  <tr>						
    <th>FIX Field Name</th>
    <th>Description</th>
  </tr>
  <tr>
    <td>ClOrdID</td>
    <td>The unique identifier of the order assigned by the client</td>
  </tr>
  <tr>
    <td>OrdType</td>
    <td>OEML supports only the LIMIT order type. Market orders don't have price protection, and because of that, they are not supported.</td>
  </tr>
  <tr>
    <td>Side</td>
    <td>Side of order.</td>
  </tr>
   <tr>
    <td>Symbol</td>
    <td>Exchange symbol</td>
  </tr>
  <tr>
    <td>Price</td>
    <td>Order price.</td>
  </tr>
  <tr>
    <td>OrderQty</td>
    <td>Order quantity</td>
  </tr>
  <tr>
    <td>TimeInForce</td>
    <td>Time in force is a special instruction used when placing a trade to indicate how long an order will remain active before it expires</td>
  </tr>
   <tr>
    <td>TimeInForce</td>
    <td>Time in force is a special instruction used when placing a trade to indicate how long an order will remain active before it expires</td>
  </tr>
</table>


<!-- # Authentication

> To authorize, use this code:

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
```

```shell
# With shell, you can just pass the correct header with each request
curl "api_endpoint_here" \
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
```

> Make sure to replace `meowmeowmeow` with your API key.

Kittn uses API keys to allow access to the API. You can register a new Kittn API key at our [developer portal](http://example.com/developers).

Kittn expects for the API key to be included in all API requests to the server in a header that looks like the following:

`Authorization: meowmeowmeow`

<aside class="notice">
You must replace <code>meowmeowmeow</code> with your personal API key.
</aside>

# Kittens

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
curl "http://example.com/api/kittens" \
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
curl "http://example.com/api/kittens/2" \
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
curl "http://example.com/api/kittens/2" \
  -X DELETE \
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
 -->
