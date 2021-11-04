# logging模組簡介

Python的logging模組提供了通用的日誌系統，可以方便第三方模組或者是應用使用。

這個模組提供不同的日誌級別，並可以採用不同的方式記錄日誌

比如檔案，HTTP GET/POST，SMTP，Socket等，甚至可以自己實現具體的日誌記錄方式。

logging模組與log4j的機制是一樣的，只是具體的實現細節不同。

* 模組提供logger，handler，filter，formatter。

## logger
logger：提供日誌介面，供應用程式碼使用。

logger最長用的操作有兩類：配置和傳送日誌訊息。

可以通過
```py
logging.getLogger(name)
```
獲取logger物件，如果不指定 `name` 則返回 `root` 物件，多次使用相同的 `name` 呼叫 `getLogger` 方法返回同一個 `logger` 物件。

## handler

* handler：將日誌記錄`（log record）`傳送到合適的目的地`（destination）`

比如檔案:socket等。一個logger物件可以通過addHandler方法新增0到多個handler

每個`handler`又可以定義不同日誌級別，以實現日誌分級過濾顯示。

## filter 

* filter：提供一種優雅的方式決定一個日誌記錄是否傳送到`handler`。

## formatter

* formatter：指定日誌記錄輸出的具體格式。`formatter`的構造方法需要兩個引數：訊息的格式字串和日期字串，這兩個引數都是可選的。
