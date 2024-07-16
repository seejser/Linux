# docker mongodb sh
## CLI 
### 通过命令更新数据

`
1. docker exec -ti norgren-mongo bash

2. mongo

3. show dbs
4.  use imi_dealer
5.  show collections
6.  db.dealers.find({ _id: "664ede4dc7f90d481c32d60a" })
7.  db.dealers.find({ china_name:"上海伊里德自动化设备有限公司" }).pretty()
8.  db.dealers.updateOne(
   { china_name: "上海伊里德自动化设备有限公司" }, // 查询条件
   { $set: { headquarters_address: "上海市浦东新区金桥开发区新金桥路1088号" } } // 更新操作
)

`
