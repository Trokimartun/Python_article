` os `  與 ` os.path ` 為處理作業系統相關及目錄路徑的模組 (module) ，` os ` 有以下的常用常數
常數|說明
:---|:---
os.name | 系統平台名稱，目前註冊三種 'posix' 、 'nt' 及 'java' 。
os.sep | 系統平台路徑的分隔符號，例如 POSIX 為 '/' 而 Windows 為 '\\' 。
os.linesep | 系統平台的斷行符號，例如 POSIX 為 '\n' 而 Windows 為 '\r\n 。

`os` 有以下的常用函數 (function)

函數|說明
:---|:---
os.system(command)	| 執行 command ， command 為系統指令的字串。
os.getcwd()	| 取得目前所在路徑。
os.rename(src, dst, *, src_dir_fd=None, dst_dir_fd=None)	| 將 src 改名為 dst 。
os.listdir(path='.') | 	回傳 path 中所有內容的串列，預設為當前路徑。
os.mkdir(path, mode=0o777, *, dir_fd=None)	| 建立 path 路徑，如果已存在就會發起例外。
os.remove(path, *, dir_fd=None) |	移除 path ，如果 path 是目錄就會發起例外。
os.rmdir(path, *, dir_fd=None)	| 刪除 path 目錄。

以下程式示範利用 `os.name` 判斷作業系統種類，然後用相對應的系統指令清除終端機畫面
```py
import os

if os.name == "posix":
    os.system("clear")
elif os.name == "nt":
    os.system("cls")
else:
    print("未能識別的作業系統。")
```

於命令列執行以上程式
***
$ python3 odemo01.py
***
按下 `Enter` 鍵，就會清除終端機的畫面
***
$
***

`os.path` 有以下的常用函數

函數 |	說明
:---|:---
os.path.isfile(path)	| 判斷 path 檔案是否存在。
os.path.isdir(path)	| 判斷 path 路徑是否存在。
os.path.split(path)	| 分割路徑為 (head, tail) ，其中 head 為目錄， tail 為檔案名稱。
os.path.splitext(path)	| 分割路徑為 (root, ext) ，其中 root 為目錄包括檔名， ext 為副檔名。
os.path.join(dirpath, filename) |	將 dirpath 與 filename 結合，無需自行判斷要用 '\\' 或 '/' 。
os.path.dirname(path) |	回傳 path 的目錄路徑。
os.path.basename(path) |	回傳 path 的檔案名稱。
os.path.getsize(path)	| 回傳 path 以位元組計算的大小。

以下程式先判斷目錄是否存在，如果不存在就建立新目錄，然後把文字檔案拷貝到新目錄，最後用 UNIX-Like 的系統指令 cat 印出檔案內容
```py
import os
import os.path
import shutil

if not os.path.isdir("demo"):
    os.mkdir("demo")
    
new_path = "demo/new.txt"
shutil.copy("quotes.txt", new_path) 
os.system("cat " + new_path)
```

於命令列執行以上程式
***
$ python3 odemo02.py
Hello world!
There is no spoon.
Manners maketh the man.
You need time to know, to forgive and to love.
And then be a simple man.
$
***
