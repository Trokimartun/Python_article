# 多模組使用logging
    logging模組保證在同一個python直譯器內，多次呼叫logging.getLogger(‘log_name’)都會返回同一個logger例項
    
    即使是在多個模組的情況下。所以典型的多模組場景下使用logging的方式是在main模組中配置logging
    
    這個配置會作用於多個的子模組，然後在其他模組中直接通過getLogger獲取Logger物件即可。
    
    配置檔案：
    
```py
[loggers] 
keys=root,main 
[handlers] 
keys=consoleHandler,fileHandler 
[formatters] 
keys=fmt 
[logger_root] 
level=DEBUG 
handlers=consoleHandler 
[logger_main] 
level=DEBUG 
qualname=main 
handlers=fileHandler 
[handler_consoleHandler] 
class=StreamHandler 
level=DEBUG 
formatter=fmt 
args=(sys.stdout,) 
[handler_fileHandler] 
class=logging.handlers.RotatingFileHandler 
level=DEBUG 
formatter=fmt 
args=('tst.log','a',20000,5,) 
[formatter_fmt] 
format=%(asctime)s - %(name)s - %(levelname)s - %(message)s 
datefmt= 
```

## 主模組main.py：

```py
import logging 
import logging.config 
logging.config.fileConfig('logging.conf') 
root_logger = logging.getLogger('root') 
root_logger.debug('test root logger...') 
logger = logging.getLogger('main') 
logger.info('test main logger') 
logger.info('start import module \'mod\'...') 
import mod 
logger.debug('let\'s test mod.testLogger()') 
mod.testLogger() 
root_logger.info('finish test...') 
```

## 子模組mod.py：

```py
import logging 
import submod 
logger = logging.getLogger('main.mod') 
logger.info('logger of mod say something...') 
def testLogger(): 
logger.debug('this is mod.testLogger...') 
submod.tst() 
```
## 子子模組submod.py：

```py
import logging 
logger = logging.getLogger('main.mod.submod') 
logger.info('logger of submod say something...') 
def tst(): 
logger.info('this is submod.tst()...') 
```

然後執行python main.py，控制檯輸出：

    2012-03-09 18:22:22,793 - root - DEBUG - test root logger... 
    2012-03-09 18:22:22,793 - main - INFO - test main logger 
    2012-03-09 18:22:22,809 - main - INFO - start import module 'mod'... 
    2012-03-09 18:22:22,809 - main.mod.submod - INFO - logger of submod say something... 
    2012-03-09 18:22:22,809 - main.mod - INFO - logger say something... 
    2012-03-09 18:22:22,809 - main - DEBUG - let's test mod.testLogger() 
    2012-03-09 18:22:22,825 - main.mod - DEBUG - this is mod.testLogger... 
    2012-03-09 18:22:22,825 - main.mod.submod - INFO - this is submod.tst()... 
    2012-03-09 18:22:22,841 - root - INFO - finish test... 

可以看出，和預想的一樣，然後在看一下tst.log，logger配置中的輸出的目的地：
    
    2012-03-09 18:22:22,793 - main - INFO - test main logger 
    2012-03-09 18:22:22,809 - main - INFO - start import module 'mod'... 
    2012-03-09 18:22:22,809 - main.mod.submod - INFO - logger of submod say something... 
    2012-03-09 18:22:22,809 - main.mod - INFO - logger say something... 
    2012-03-09 18:22:22,809 - main - DEBUG - let's test mod.testLogger() 
    2012-03-09 18:22:22,825 - main.mod - DEBUG - this is mod.testLogger... 
    2012-03-09 18:22:22,825 - main.mod.submod - INFO - this is submod.tst()... 
