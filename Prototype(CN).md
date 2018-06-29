# Prototype(CN)

## 合约代码
  
 [prototype.sol](https://github.com/vechain/thor/blob/master/builtin/gen/prototype.sol)
 
## 合约地址 
 
 `0x000000000000000000000050726f746f74797065`
>Prototype合约地址，在主网及测试网皆为以上地址

##  方法

|方法|描述| 参数|
|---|---|----|
|master|默认合约部署者为合约控制者，调用此方法将会返回合约控制者地址|self: 要操作对象的地址|
|setMaster|设置新的合约控制者（仅限当前合约控制者可执行此操作）|self: 要操作对象的地址<br>newMaster: 新合约控制者地址|
|balance|返回指定区块VET余额 |self: 要操作对象的地址<br>blockNumber: 区块编号(Block Number ∈[最新区块-65535 , 最新区块]|
|energy|返回指定区块的VTHO余额 |self: 要操作对象的地址<br>blockNumber: 区块编号(Block Number ∈[最新区块-65535 , 最新区块]|
|hasCode|返回消息发送者是否为合约 |self: 要操作对象的地址|
|storageFor|账号模型中的存储|self: 要操作对象的地址<br>key: [参考](https://solidity.readthedocs.io/en/latest/miscellaneous.html#layout-of-state-variables-in-storage)|
|creditPlan|返回用户计划中的额度以及额度恢复速率|self: 要操作对象的地址|
|setCreditPlan|设置合约所有用户的用户计划额度以及额度恢额度速率 （仅限合约控制者及合约本身可调用此方法)|self: 要操作对象的地址<br>credit: 欲设置的可用额度数值(Wei)<br>recoveryRate: 每秒额度恢复速率(Wei)|
|isUser|查看地址是否为合约的用户 |self: 要操作对象的地址<br>user: 指定地址|
|userCredit|返回指定用戶可用额度|self: 要操作对象的地址<br>user: 用户地址|
|addUser|添加地址成为合约用户，一旦添加后，根据setCreditPlan方法赋予新添加用户可用额度及额度恢复速率（仅限合约控制者及合约本身可调用此方法）|self: 要操作对象的地址<br>user: 用户地址|
|removeUser|将一名合约用户从合约用户中移除。（仅限合约控制者及合约本身可调用此方法）|self: 要操作对象的地址<br>user: 用户地址|
|sponsor|成为合约赞助名单中的候选人 |self: 要操作对象的地址|
|unsponsor|取消对合约的赞助，从赞助名单中移除 |self: 要操作对象的地址|
|isSponsor|查询指定地址是否为赞助者 |self: 要操作对象的地址<br>sponsor：欲查询用户地址|
|selectSponsor|从赞助者合集中选择一名成为合约赞助者（仅限合约控制者及合约本身可调用此方法)|self: 要操作对象的地址<br>sponsor: 合集中赞助者地址|
|currentSponsor|返回当前赞助者|self: 要操作对象的地址|