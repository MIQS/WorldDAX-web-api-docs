Base endpoint: https://xxx.com/consolidated

# REST Public Endpoints

* [Consolidated Feed Sources](#dataSources)
* [Ticker](#ticker)
* [Order Book](#orderBook)
* [Trades](#trades)
* [Charts](#charts)

<a name="dataSources" id="dataSources"> </a>

---
## Data Sources

    GET /dataSources

    Get data sources of consolidated feed

### Request Parameters

Name                  | Type(value)      | Mandatory   | Description
----------------------| -----------------|-------------|-----------------------------
instrumentId          | String           | O           |

### Success Response Body Fields

Name               | Type(value)      | Mandatory   | Description
-------------------| -----------------|-------------|--------------------------------
instrumentId       | String           | M           | e.g. BTCUSD
dataSources        | Array of dataSource  | M           | e.g. [COINBASE_PRO, BITSTAMP, BITFINEX]

---
## Ticker

    GET /ticker

### Request Parameters

Name               | Type(value)      | Mandatory   | Description
-------------------| -----------------|-------------|-----------------------
instrumentId       | String           | M           | e.g. “ETHBTC”
dataSource         | Enum             | M         | e.g. "CONSOLIDATED"

### Success Response Body Fields

Name             | Type(value)      | Mandatory   | Description
-----------------| -----------------|-------------|-----------------------
instrumentId     | String           | M           | e.g. “ETHBTC”
dataSource       | Enum           | M           |
lastModifiedTime | Long             | M           | 
lastPrice        | DoubleString     | M           | 
bestBid          | DoubleString     | M           | 
bestAsk          | DoubleString     | M           | 
24hHigh          | DoubleString     | M           | 
24hLow           | DoubleString     | M           | 
24hVolume        | DoubleString     | M           | 
24hChange        | DoubleString     | M           | 

---
<a name="orderBook" id="orderBook"> </a>

## Order Book

    GET /orderbook
    
    Weight: 5

### Request Parameters

Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           | 
bookLevel       | Integer          | M           | 1 - top bid and ask; 2 – order book;
dataSource         | Enum             | M         | e.g. "CONSOLIDATED"

### Success Response Body Fields

Name               | Type(value)                                   | Mandatory   | Description
-------------------| ----------------------------------------------|-------------|-----------------------
instrumentId       | String                                        | M           |
dataSource         | Enum             | M         | e.g. "CONSOLIDATED"
lastModifiedTime   | Long                                          | M           |
bookLevel       | Integer                                       | M           | 1/2/3
sequence        | Long                                          | M           | 
bids            | Array of [price, size, numOfOrders/orderId]   | M           | Level 1 – This is one sized array;Level 2 – The aggregated size for each price level is returned with numOfOrders count for the price;Level 3 – The order level information is returned
asks            | Array of [price, size, numOfOrders/orderId]   | M           | Level 1 – This is one sized array;Level 2 – The aggregated size for each price level is returned with numOfOrders count for the price;Level 3 – The order level information is returned

---
<a name="trades" id="trades"> </a>

## Trades

    GET /trades
    
Returns most recent trades in an array.

### Request Parameters

Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           |
dataSource         | Enum             | M         | e.g. "CONSOLIDATED"

### Success Response Body Array Json Fields

Name            | Type(value)      | Mandatory   | Description
----------------| -----------------|-------------|-----------------------
instrumentId    | String           | M           |
dataSource         | Enum             | M         | e.g. "CONSOLIDATED"
createdTime     | Long             | M           |
tradeId   | String           | M           | 
price     | DoubleString     | M           | 
size      | DoubleString     | M           | 
side      | Enum             | M           |


<a name="charts" id="charts"> </a>

---
## Charts

    GET /charts

It returns an array of data point stats.

### Request Parameters

Name          | Type(value)     | Mandatory   | Description
--------------| ----------------|-------------|-----------------------
instrumentId  | String          | M           |
dataSource         | Enum             | M         | e.g. "CONSOLIDATED"
startTime        | Long            | M         | Seconds since Unix Epoch
endTime       | Long            | M           | Seconds since Unix Epoch
granularity   | Integer         | M           | In seconds; 60/300/900/3600/21600/86400;The combination of startTime, endTime and granularity determines how many data points obtained. The maximum supported number of data points is xxx

### Success Response Body Fields

Name             | Type(value)     | Mandatory   | Description
-----------------| ----------------|-------------|-----------------------
lastModifiedTime | Long            | M           |
dataSource         | Enum             | M         | e.g. "CONSOLIDATED"
startTime        | Long            | M           |
endTime          | Long            | M           | 
openPrice        | String          | M           | 
closePrice       | String          | M           | 
low              | String          | M           | 
high             | String          | M           | 
volume           | String          | M           | 

