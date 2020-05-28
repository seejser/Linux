## Mac install monogodb

1.install
```
brew install mongodb
```

2.setup

```
cd /

mkdir data

cd data

mkdir db

monogod
```

3.use

```
mongod


```
4.阿里云

```
//查询
db.topics.findOne (
    {content: "HDF治疗的优势及临床获益"},
)

//查询并修改
db.topics.update  (
    {content: "HDF治疗的优势及临床获益"},
    { $set: { writer:"5eb575d990c813083985fc4a",
            uid:"5eb575d990c813083985fc4a"
            } },
)
```
