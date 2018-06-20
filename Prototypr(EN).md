#Prototype example (new)

## Contract code 
```
pragma solidity ^0.4.18;

contract ExampleContract{
    
}
```



##  Methods
|Methods|Description| parameter|
|---|---|----|
|$master|return master's address(default contract deployer is contract master)|-|
|$set_master|set  new contract master(only contract master can call the method)|newMaster：new contract master's address|
|$balance|return VET & VTHO balance at specific block |blockNumber: number of block  (The difference between latest block number and query block number **can not** exceed more than 65535)|
|$energy|return VTHO balance at specific block |blockNumber: number of block  (The difference between latest block number and query block number **can not** exceed more than 65535)|
|$transfer_energy| message sender transfer amount of VTHO to recipient  |amount:amount transferred to the recipient(VTHO/Wei)|
|$moveEnergyTo|message sender call the function and transfer amount of VTHO from contract master or contract's address to recipient|to:recipient's address<br>amount: amount transferred to the recipient(VTHO/Wei)|
|has_code|determine the message sender either a contract or not |-|
|$storageFor|Storage|[Reference](https://solidity.readthedocs.io/en/v0.4.24/miscellaneous.html#layout-of-state-variables-in-storage)|
|$user_plan|return credits and recovery rate|-|
|$set_user_plan|set a default credits and recovery rate for all contract users |credit：default credits(Wei)；recoveryRate：recoveryRate per second(Wei)|
|$is_user|check the user address either contract's user or not |user： user's address|
|$user_credit|return user's credit balance|user： user's address|
|$add_user|add a user become contract's user, once the user has been added , the user will has default credits.(only contract master and contract it self are allow to call the function)|user：user's address|
|$remove_user|remove a user become contract's user, once the user has been removed , the user will has default credits.(only contract master and contract it self are allow to call the function)|user:user's address|
|$sponsor|sponsor the contract |yesOrNo(bool)：<br>true: willing to become contract's sponsor ； <br>false:unwilling to become contract's sponsor|
|$is_sponsor|determine the address either the sponsor or not |sponsor：specific address|
|$select_sponsor|select an address from sponsor set to become contract sponsor|sponsor：an address from sponsor set|
|$current_sponsor|return current sponsor|-|

### Prototype address 
0x000000000000000000000050726f746f74797065 

### Prototype abi 
```
[{"constant":true,"inputs":[{"name":"target","type":"address"}],"name":"$hasCode","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"}],"name":"$currentSponsor","outputs":[{"name":"","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"user","type":"address"}],"name":"$removeUser","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"user","type":"address"}],"name":"$isUser","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"credit","type":"uint256"},{"name":"recoveryRate","type":"uint256"}],"name":"$setUserPlan","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"sponsor","type":"address"}],"name":"$isSponsor","outputs":[{"name":"","type":"bool"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"user","type":"address"}],"name":"$userCredit","outputs":[{"name":"remainedCredit","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"key","type":"bytes32"}],"name":"$storage","outputs":[{"name":"value","type":"bytes32"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"user","type":"address"}],"name":"$addUser","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"}],"name":"$userPlan","outputs":[{"name":"credit","type":"uint256"},{"name":"recoveryRate","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"sponsor","type":"address"}],"name":"$selectSponsor","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"yesOrNo","type":"bool"}],"name":"$sponsor","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"key","type":"bytes32"},{"name":"blockNumber","type":"uint32"}],"name":"$storage","outputs":[{"name":"value","type":"bytes32"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"blockNumber","type":"uint32"}],"name":"$balance","outputs":[{"name":"amount","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"}],"name":"$master","outputs":[{"name":"master","type":"address"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":true,"inputs":[{"name":"target","type":"address"},{"name":"blockNumber","type":"uint32"}],"name":"$energy","outputs":[{"name":"amount","type":"uint256"}],"payable":false,"stateMutability":"view","type":"function"},{"constant":false,"inputs":[{"name":"target","type":"address"},{"name":"newMaster","type":"address"}],"name":"$setMaster","outputs":[],"payable":false,"stateMutability":"nonpayable","type":"function"}]
```



### Demo code 
```
web3.eth.accounts.wallet.add("0xdce1443bd2ef0c2631adc1c67e5c93f13dc 23a41c18b536effbbdcbcdb96fb65"); //0x7567d83b7b8d80addcb281a71d54fc7b3364ffed 
var master=await cprototypeafter.methods.$master("0x7567d83b7b8d80addcb281a71d54fc7b 3364ffed").call() 
var master=await cprototypeafter.methods.$setMaster("0x7567d83b7b8d80addcb281a71d54f c7b3364ffed","").send({ 
from:"0x7567d83b7b8d80addcb281a71d54fc7b3364ffed" }) 
var cmaster=await cprototypeafter.methods.$master("0x7567d83b7b8d80addcb281a71d54fc7b 3364ffed").call() 
```
    




