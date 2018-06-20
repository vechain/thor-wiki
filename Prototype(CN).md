## 合约代码
 
```
pragma solidity ^0.4.18;

contract ExampleContract{
    
}
```

##  方法
|方法|描述| 参数|
|---|---|----|
|$master|返回合约master地址（默认合约部署人为合约拥有者）|-|
|$set_master|设置合约master new （仅限合约拥有者可执行此操作）|newMaster：新合约拥有者地址|
|$balance|返回指定区块的VET & VTHO 余额 |blockNumber: 区块编号（区块编号区间仅限在最新块前65535个块至最新块）|
|$energy|返回指定区块的VTHO |blockNumber: 区块编号（区块编号区间仅限在最新块前65535个块至最新块）|
|$transfer_energy| 消息发送者转移VTHO至消息接收者  |amount:欲转移VTHO至消息接收者的数值(VTHO/Wei)|
|$moveEnergyTo|消息发送者调用VTHO转移功能和从合同部署人或合同将指定的VTHO转向消息接收方|to:消息接收者地址<br>amount: 欲转移VTHO至消息接收者的数值(VTHO/Wei)|
|has_code|返回消息发送者是否为合约 |-|
|$storageFor|账号模型中的存储|[参考](https://solidity.readthedocs.io/en/v0.4.24/miscellaneous.html#layout-of-state-variables-in-storage)|
|$user_plan|返回用户计划中的额度以及余额恢复速率|-|
|$set_user_plan|设置合约所有用户的合约计划额度以及恢复速率 |credit：欲设置的可用额度数值(Wei)；recoveryRate：每秒的恢复速率(Wei)|
|$is_user|查看地址是否为合约的用户 |user： 指定地址|
|$user_credit|返回指定用戶可用剩余额度|user： 用户地址|
|$add_user|添加地址成为合约用户，一旦添加后，默认设置用户可用额度及恢复速率（仅限合约拥有者及合约本身可调用此方法）|user：用户地址|
|$remove_user|将一名合约用户从合约用户中移除。（仅限合约拥有者及合约本身可调用此方法）|user：用户地址|
|$sponsor|合约赞助 |yesOrNo(bool)：<br>true: 成为合约赞助者合集中的赞助者 ； <br>false:从合约赞助者合集中移除|
|$is_sponsor|查询指定地址是否为赞助者 |sponsor：欲查询用户地址|
|$select_sponsor|从赞助者合集中选择一名成为合约赞助者|sponsor：合集中赞助者地址|
|$current_sponsor|返回当前赞助者|-|

### prototype 合约地址 
0x000000000000000000000050726f746f74797065
### prototype abi 

```
[{"constant":true,"inputs":[{"name":"target","type":"address"}],"name":"$hasCode","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"}],"name":"$currentSponsor","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"user","type":"address"}],"name":"$removeUser","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"user","type":"address"}],"name":"$isUser","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"credit","type":"uint256"},{"name":"recoveryRate","type":"uint256"}],"name":"$setUserPlan","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"sponsor","type":"address"}],"name":"$isSponsor","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"user","type":"address"}],"name":"$userCredit","outputs":[{"name":"remainedCredit","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"key","type":"bytes32"}],"name":"$storage","outputs":[{"name":"value","type":"bytes32"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"user","type":"address"}],"name":"$addUser","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"}],"name":"$userPlan","outputs":[{"name":"credit","type":"uint256"},{"name":"recoveryRate","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"sponsor","type":"address"}],"name":"$selectSponsor","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"yesOrNo","type":"bool"}],"name":"$sponsor","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"key","type":"bytes32"},{"name":"blockNumber","type":"uint32"}],"name":"$storage","outputs":[{"name":"value","type":"bytes32"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"blockNumber","type":"uint32"}],"name":"$balance","outputs":[{"name":"amount","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"}],"name":"$master","outputs":[{"name":"master","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"blockNumber","type":"uint32"}],"name":"$energy","outputs":[{"name":"amount","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"newMaster","type":"address"}],"name":"$setMaster","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"}]
```



### demo code 

```
web3.eth.accounts.wallet.add("0xdce1443bd2ef0c2631adc1c67e5c93f13dc 23a41c18b536effbbdcbcdb96fb65"); //0x7567d83b7b8d80addcb281a71d54fc7b3364ffed 
var master=await cprototypeafter.methods.$master("0x7567d83b7b8d80addcb281a71d54fc7b 3364ffed").call() 
var master=await cprototypeafter.methods.$setMaster("0x7567d83b7b8d80addcb281a71d54f c7b3364ffed","").send({ 
from:"0x7567d83b7b8d80addcb281a71d54fc7b3364ffed" }) 
var cmaster=await cprototypeafter.methods.$master("0x7567d83b7b8d80addcb281a71d54fc7b 3364ffed").call() 
```
    




