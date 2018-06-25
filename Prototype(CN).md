# Prototype(CN)

## 合约代码
  
[prototype.sol](https://github.com/vechain/thor/blob/master/builtin/gen/prototype.sol)
 
## 合约地址 
 
 `0x000000000000000000000050726f746f74797065`
>Prototype合约地址，在主网及测试网皆为以上地址

## VET 和 VTHO
VeChainThor采取双代币机制，也就是VET（主代币）、VTHO（次代币）。主代币能生成（以一定的恢复速率自动产生）次代币至最大值“credit”(此值由账户自己或者账户的操控者设置，到达最大峰值之后不再产生VTHO)，次代币VTHO被作为”energy”来购买手续费的gas根据 gas price。

##  方法

|方法|描述| 参数|
|---|---|----|
|master|合约账户的部署者为合约最初的控制者，也可后续由合约的控制者再设置新的控制者；普通用户的控制者最初需要普通用户本身设置，后续可由普通账户的控制者再设置新的控制者。调用此方法将会返回账户控制者地址|self: 要被操作对象的地址|
|setMaster|设置新的控制者（仅限账户控制者及账户本身可调用此方法）|self: 要被操作对象的地址<br>newMaster: 新账户控制者地址|
|balance|返回指定区块VET余额 |self: 要被操作对象的地址<br>blockNumber: 区块编号（区块编号区间仅限在最新块前65535个块至最新块）|
|energy|返回指定区块的VTHO Credit |self: 要被操作对象的地址<br>blockNumber: 区块编号（区块编号区间仅限在最新块前65535个块至最新块）|
|hasCode|返回消息发送者是否为合约 |self: 要被操作对象的地址|
|storageFor|账号模型中的存储|self: 要被操作对象的地址<br>key: [参考](https://solidity.readthedocs.io/en/latest/miscellaneous.html#layout-of-state-variables-in-storage)|
|creditPlan|返回credit额度以及credit恢复速率|self: 要被操作对象的地址|
|setCreditPlan|设置指定地址账户的credit计划额度以及恢额度速率 |self: 要被操作对象的地址<br>credit: 欲设置的energy可用额度数值(Wei)<br>recoveryRate: 每秒额度恢复credit的速率(Wei)|
|isUser|查看地址是否为合约的用户 |self: 要被操作对象的地址<br>user: 指定地址|
|userCredit|返回指定用戶可用剩余credit额度|self: 要被操作对象的地址<br>user: 用户地址|
|addUser|添加地址成为合约用户，一旦添加后，默认设置用户可用额度及额度恢复速率（仅限账户控制者及账户本身可调用此方法）|self: 要被操作对象的地址<br>user: 用户地址|
|removeUser|将一名合约用户从合约用户中移除。（仅限账户控制者及账户本身可调用此方法）|self: 要被操作对象的地址<br>user: 用户地址|
|sponsor|合约赞助 |self: 要被操作对象的地址<br>yesOrNo(bool): <br>true: 成为合约赞助者合集中的赞助者 <br>false: 从合约赞助者合集中移除|
|isSponsor|查询指定地址是否为赞助者 |self: 要被操作对象的地址<br>sponsor：欲验证的用户地址|
|selectSponsor|从赞助者合集中选择一名成为账户赞助者。（仅限账户控制者及账户本身可调用此方法）|self: 要被操作对象的地址<br>sponsor: 合集中赞助者地址|
|currentSponsor|返回当前赞助者|self: 要被操作对象的地址|
