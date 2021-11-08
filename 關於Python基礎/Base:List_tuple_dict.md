# list(串列)

  串列：由零或多個元素組成的，以「,」逗號分隔，並且放在[ ]裡面。  
  語法：[element1,element2.....]  

```py
man_list = ["sun","air","water","food"]
print(man_list[0]) 
print(man_list[-2])
```

  `輸出結果`  
  `sun`  
  `water`  

## Tuple(元組)：不能修改的List
優點：執行速度比list快，儲存在Tuple的資料比較安全
以下示範建立tuple，不同於list使用[]，tuple使用()
```py
man_tuple = ("陽光", "空氣", "水", "食物")
```

* list和tuple互相轉換 
```py
man_tuple = ("陽光", "空氣", "水", "食物")
man_list = ["sun","air","water","food"]
tuple_to_list = list(man_tuple)
list_to_tuple = tuple(man_list)
print(list(tuple_to_list))
print(list(list_to_tuple))
```

# 輸出結果
['陽光', '空氣', '水', '食物']
['sun', 'air', 'water', 'food']
