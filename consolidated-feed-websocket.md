Base endpoint: wss://xxx.com/consolidated

# Websocket Public Channels
* [Ticker](#ticker)
* [Order Book](#orderBook)
* [Trade](#trade)
* [Charts](#charts)

<a name="ticker" id="ticker"> </a>
---
## Ticker

Ticker data with 24h market statistics is pushed every 5 seconds

### Request Fields

Name           | Type(value)                     | Mandatory   | Description
---------------| --------------------------------|-------------|-----------------------
type           | subscribe/unsubscribe           | M           | Subscribe/Unsubscribe message type
channel        | ticker                          | M           |
dataSource     | Enum                            | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
userMessageId  | Integer                         | O           | Unique message id for this websocket session
instrumentIds  | Array of instrumentId Strings   | M           |


### Response Fields

Name           | Type(value)                     | Mandatory   | Description
---------------| --------------------------------|-------------|-----------------------
type           | subscribed/unsubscribed         | M           | Subscribed/Unsubscribed message type
channel        | ticker                          | M           |
dataSource     | Enum                            | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
timestamp      | Long                            | M           | Request accepted time
instrumentIds  | Array of instrumentId Strings   | M           |
userMessageId  | Integer                         | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields:

Name           | Type(value)    | Mandatory   | Description
---------------| ---------------|-------------|----------------
type           | ticker         | M           |
dataSource     | Enum           | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
timestamp      | Long           | M           | Ticker created time
instrumentId   | String         | M           | e.g. “BTCUSD”
lastPrice      | DoubleString   | M           |
bestBid        | DoubleString   | M           |
bestAsk        | DoubleString   | M           |
24hHigh        | DoubleString   | M           |
24hLow         | DoubleString   | M           |
24hVolume      | DoubleString   | M           |
24hChange      | DoubleString   | M           |

<a name="orderBook" id="orderBook"> </a>
---
## Order Book

### Request Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|----------------
type           | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel        | orderBook                      | M           |
dataSource     | Enum                           | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
depth          | Integer                        | O           | Default to 25
instrumentIds  | Array of instrumentId Strings  | M           |
userMessageId  | Integer                        | O           | Unique message id for this websocket session


### Response Fields

Name           | Type(value)                         | Mandatory   | Description
---------------| ------------------------------------|-------------|----------------
type           | subscribed/unsubscribed             | M           | Subscribe/Unsubscribe message type
channel        | orderBook                           | M           |
dataSource     | Enum                                | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
timestamp      | Long                                | M           | When subscription request was accepted
depth          | Integer                             | M           |
instrumentId   | instrumentId String                 | M           |
bids           | Array of [price, size, numOfOrders] | M           | Snapshot of bids with the aggregated size for each price level
asks           | Array of [price, size, numOfOrders] | M           | Snapshot of asks with the aggregated size for each price level
userMessageId  | Integer                             | (M)         | Mandatory if userMessageId is provided in the user request


### Channel Fields

Name           | Type(value)                        |  Mandatory  | Description
---------------| -----------------------------------| ------------|--------------------------------------
type           | orderBook                          | M           |
timestamp      | Long                               | M           | order book update time
instrumentId   | String                             | M           |
dataSource     | Enum                               | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
bids           | Array of [price, size, numOfOrders]| M           | Update of bids with the aggregated size for the updated price level
asks           | Array of [price, size, numOfOrders]| M           | Update of asks with the aggregated size for the updated price level


<a name="trade" id="trade"> </a>

---
## Trade

trade data is pushed whenever a trade occurs in the system.

### Request Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|-------------
type           | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel        | trade                          | M           |
dataSource     | Enum                           | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
instrumentIds  | Array of instrumentId Strings  | M           |
userMessageId  | Integer                        | O           | Unique message id for this websocket session

### Response Fields

Name           | Type(value)                    | Mandatory   | Description
---------------| -------------------------------|-------------|-------------
type           | subscribed/unsubscribe         | M           | Subscribe/Unsubscribe message type
channel        | trade                          | M           |
dataSource     | Enum                           | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
timestamp      | Long                           | M           | When the subscription request was accepted
instrumentIds  | Array of instrumentId Strings  | M           |
userMessageId  | Integer                        | (M)         | Mandatory if userMessageId is provided in the user request

### Channel Fields

Name             | Type(value)     | Mandatory   | Description
-----------------| ----------------|-------------|-------------
type             | trade           | M           |
timestamp        | Long            | M           | Trade time
instrumentId     | String          | M           |
dataSource       | Enum            | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
tradeId   | String          | M           |
price     | DoubleString    | M           |
size      | DoubleString    | M           |
side      | Enum            | M           | Buy/Sell

<a name="charts" id="charts"> </a>

---
## Charts

### Request Fields

Name            | Type(value)                    | Mandatory   | Description
----------------| -------------------------------|-------------|-------------
type            | subscribe/unsubscribe          | M           | Subscribe/Unsubscribe message type
channel         | charts                         | M           |
instrumentIds   | Array of instrumentId Strings  | M           |
dataSource      | Enum                           | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
granularity     | Integer                        | M           |
userMessageId   | Integer                        | O           | Unique message id for this websocket session


### Response Fields

Name            | Type(value)                                                       | Mandatory   | Description
----------------| ------------------------------------------------------------------|-------------|-------------
type            | subscribed/unsubscribed                                           | M           | Subscribe/Unsubscribe message type
channel         | charts                                                            | M           |
dataSource      | Enum                                                              | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
timestamp       | Long                                                              | M           | When the subscription request was accepted
instrumentId    | String                                                            | M           |
granularity     | Integer                                                           | M           |
userMessageId   | Integer                                                           | (M)         | Mandatory if userMessageId is provided in the user request
records         | Array of [startTime,open,close,low,high,volume] | M           |

The first charts message will contain the array of historical data
entries with the maximum size of 300.

### Channel Fields

Name          | Type(value)                                              | Mandatory   | Description
--------------| ---------------------------------------------------------|-------------|-------------
type          | charts                                                   | M           |
timestamp     | Long                                                     | M           | Chart update time
instrumentId  | String                                                   | M           |
dataSource    | Enum                                                     | O           | Subscribe/Unsubscribed "CONSOLIDATED" by default
granularity   | Integer                                                  | M           |
update        | [startTime,open,close,low,high,volume] | M           |


