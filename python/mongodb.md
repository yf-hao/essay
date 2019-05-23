## 1. 插入数据
```python
from pymongo import  MongoClient

client = MongoClient()
# 连接数据库，如果没有就创建
database = client['demo']

collection = database['spider']

# 插入一条数据
data ={'id':123,'name':'hao','age':20}
collection.insert(data)

# 批量插入
data = [
    {'id':124,'name':'hao1','age':20},
    {'id':125,'name':'hao2','age':30}
]
collection.insert(data)

```
## 2.查询数据

