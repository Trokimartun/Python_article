# logging用法解析

初始化 
```py
logger = logging.getLogger(“endlesscode”)，getLogger() 
```
方法後面最好加上所要日誌記錄的模組名字
    
後面的日誌格式中的  `%(name)s`  對應的是這裡的模組名字

設定級別 
```py
logger.setLevel(logging.DEBUG)
```

Logging 中有 NOTSET < DEBUG < INFO < WARNING < ERROR < CRITICAL這幾種級別，日誌會記錄設定級別以上的日誌

`Handler`
常用的是 `StreamHandler ` 和 `FileHandler` 

windows下你可以簡單理解為一個是console和檔案日誌，一個列印在CMD視窗上，一個記錄在一個檔案上

`formatter`
定義了最終 log 資訊的順序,結構和內容，我喜歡用這樣的格式 ‘[%(asctime)s] [%(levelname)s]
```py
%(message)s’, ‘%Y-%m-%d %H:%M:%S’，
%(name)s #Logger的名字
%(levelname)s #文字形式的日誌級別
%(message)s #使用者輸出的訊息
%(asctime)s #字串形式的當前時間。預設格式是 “2003-07-08 16:49:45,896”。逗號後面的是毫秒
%(levelno)s #數字形式的日誌級別
%(pathname)s #呼叫日誌輸出函式的模組的完整路徑名，可能沒有
%(filename)s #呼叫日誌輸出函式的模組的檔名
%(module)s  #呼叫日誌輸出函式的模組名
%(funcName)s #呼叫日誌輸出函式的函式名
%(lineno)d #呼叫日誌輸出函式的語句所在的程式碼行
%(created)f #當前時間，用UNIX標準的表示時間的浮 點數表示
%(relativeCreated)d #輸出日誌資訊時的，自Logger建立以 來的毫秒數
%(thread)d #執行緒ID。可能沒有
%(threadName)s #執行緒名。可能沒有
%(process)d #程序ID。可能沒有
```
* 記錄 使用object.debug(message)來記錄日誌
* 下面來寫一個例項，在CMD視窗上只打出error以上級別的日誌，但是在日誌中打出debug以上的資訊

```py
import logging
logger = logging.getLogger("simple_example")
logger.setLevel(logging.DEBUG)
# 建立一個filehandler來把日誌記錄在檔案裡，級別為debug以上
fh = logging.FileHandler("spam.log")
fh.setLevel(logging.DEBUG)
# 建立一個streamhandler來把日誌打在CMD視窗上，級別為error以上
ch = logging.StreamHandler()
ch.setLevel(logging.ERROR)
# 設定日誌格式
formatter = logging.Formatter("%(asctime)s - %(name)s - %(levelname)s - %(message)s")
ch.setFormatter(formatter)
fh.setFormatter(formatter)
#將相應的handler新增在logger物件中
logger.addHandler(ch)
logger.addHandler(fh)
# 開始打日誌
logger.debug("debug message")
logger.info("info message")
logger.warn("warn message")
logger.error("error message")
logger.critical("critical message")
```

執行一下將會看到CMD視窗只記錄兩條，spam.log中記錄了五條日誌

* 當一個專案比較大的時候，不同的檔案中都要用到Log,可以考慮將其封裝為一個類來使用
```py
#! /usr/bin/env python
#coding=gbk
import logging,os
class Logger:
def __init__(self, path,clevel = logging.DEBUG,Flevel = logging.DEBUG):
self.logger = logging.getLogger(path)
self.logger.setLevel(logging.DEBUG)
fmt = logging.Formatter('[%(asctime)s] [%(levelname)s] %(message)s', '%Y-%m-%d %H:%M:%S')
#設定CMD日誌
sh = logging.StreamHandler()
sh.setFormatter(fmt)
sh.setLevel(clevel)
#設定檔案日誌
fh = logging.FileHandler(path)
fh.setFormatter(fmt)
fh.setLevel(Flevel)
self.logger.addHandler(sh)
self.logger.addHandler(fh)
def debug(self,message):
self.logger.debug(message)
def info(self,message):
self.logger.info(message)
def war(self,message):
self.logger.warn(message)
def error(self,message):
self.logger.error(message)
def cri(self,message):
self.logger.critical(message)
if __name__ =='__main__':
logyyx = Logger('yyx.log',logging.ERROR,logging.DEBUG)
logyyx.debug('一個debug資訊')
logyyx.info('一個info資訊')
logyyx.war('一個warning資訊')
logyyx.error('一個error資訊')
logyyx.cri('一個致命critical資訊')
```

這樣每次使用的時候只要例項化一個物件就可以了

