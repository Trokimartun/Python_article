### Python 函式 function example
簡單來說算是一個可以重複使用的功能，把你想寫的功能寫在def內，可以重複使用，可以將賦予的功能給予其他值

```py
def test1(a, b):
    return a, b

def test2(a, b):
    return a + b

test1(3, 4)  # (3, 4) 
test1('test', 'mark')  # ('test', 'mark')
test1([1, 2, 3], [0, 0, 0])  # ([1, 2, 3], [0, 0, 0])

test2(3, 4)  # 7
test2('test', 'mark')  # 'testmark'
test2([1, 2, 3], [0, 0, 0])  # [1, 2, 3, 0, 0, 0]

test3 = test2

test3(3, 4)  # 7
```

功能內如果有給予預設參數值的話，就算不給參數值也會將預設值印出來
```py
def test1(a=5):
    return a

test1()  # 5
test1(a=100)  # 100
test1(a='how are you?')  # how are you?
test1(['1', '2', '3'])  # ['1', '2', '3']
```

### Python *args 與 **kwargs example

  如果你希望函式(function)可以接受任意參數值的話，可以使用args以及kwargs  

  args也就是多個沒有定義的參數組成的元組，kwargs也就是將有指定的參數組合字典  
  另外也可以針對args取得或是kwargs做取得
```py
def test_more(*args, **kwargs):
    get_args = args
    get_kwargs = kwargs
    return get_args, get_kwargs

print(test_more(1, 2, key='word', key2='wwwww'))  # ((1, 2), {'key': 'word', 'key2': 'wwwww'})

print(test_more(1, 2, 3, 4, apple=45, mark=100, allen=300))  # ((1, 2, 3, 4), {'apple': 45, 'mark': 100, 'allen': 300})
 
print(test_more(1, 2, 3, 4, None))  # ((1, 2, 3, 4, None), {})

print(test_more(apple='eat', mark=100, allen=300, test=[1, 2, 5]))  # ((), {'apple': 'eat', 'mark': 100, 'allen': 300, 'test': [1, 2, 5]})


get_args, get_kwargs = test_more(1, 2, 3, 4, None, apple='eat', mark=100, allen=500, test=[1, 2, 3, 5])
print(get_args)  # (1, 2, 3, 4, None)

print(get_kwargs)  # {'apple': 'eat', 'mark': 100, 'allen': 500, 'test': [1, 2, 3, 5]}

print(type(get_args))  # <class 'tuple'>
print(type(get_kwargs))  # <class 'dict'>
```

[參考來源](https://learn.markteaching.com/%E3%80%90python-%E6%95%99%E5%AD%B8%E3%80%91args-%E4%BB%A5%E5%8F%8A-kwargs-%E5%9F%BA%E6%9C%AC%E7%94%A8%E6%B3%95-example/)
