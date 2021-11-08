
```py
man_tuple = ("陽光", "空氣", "水", "食物")
nman_list = ["sun","air","water","food"]
tuple_to_list = list(man_tuple)
list_to_tuple = tuple(man_list)
print(list(tuple_to_list))
print(list(list_to_tuple))
```

# 輸出結果
['陽光', '空氣', '水', '食物']
['sun', 'air', 'water', 'food']
