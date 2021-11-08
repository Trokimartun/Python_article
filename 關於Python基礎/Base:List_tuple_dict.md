## list(串列)

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
print(man_tuple[0]) 
print(man_tuple[-2])
```

* list 和 tuple 互相轉換 
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

## Dict(字典)：key-map的形式

list和Tuple都是使用數字取得元素值的方式，如果想要用其他key值來取值就可以使用Dict
語法：{key1:value1 [,key2:value2,…]}



[參考資料](https://ithelp.ithome.com.tw/articles/10200547)
