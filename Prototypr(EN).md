# Prototype(EN)

## Contract Code
 [prototype.sol](https://github.com/vechain/thor/blob/master/builtin/gen/prototype.sol)

## Contract Address
 `0x000000000000000000000050726f746f74797065`

>The above mentioned prototype contract address are same on both the test net and main net.

##  Function

|Function|Description|Parameter|
|---|---|----|
|master|By default, the contract deployer is the contract holder. The contract holder's address will be returned as a result of calling contract functions.|self: The method caller's address.|
|setMaster|Set the new contract holder (Only the current contract holder has privilege to do this operation.)|self: The method caller' address<br>newMaster: New contract's holder's address.|
|balance|Return the specified block's VET and VTHO balance.|self: The method caller' address.<br>blockNumber: Block number (The range of block number varies from 65535 ahead of latest block number to latest block number.)|
|energy|Return the specified block's VTHO balance.|self: The method caller's address.<br>blockNumber: Block number (The range of block number varies from 65535 ahead of latest block number to latest block number.)|
|hasCode|check the account type of the contract caller (contract account/normal account).|self: The method caller' address.|
|storageFor|The account model's content stored in storage.|self: The method caller' address.<br>key: [Reference](https://solidity.readthedocs.io/en/latest/miscellaneous.html#layout-of-state-variables-in-storage)|
|userPlan|Return the user planned balance and the recovery rate of plan.|self: The method caller' address.|
|setUserPlan|Set balance and recovery rate for all contract users.|self: The method caller' address.<br>credit: The available balance set to be used(Wei).<br>recoveryRate: The balance recovery rate based on per second(Wei).|
|isUser|Check whether the account is a contract user.|self: The method caller' address.<br>user: The specified user's address.|
|userCredit|Return the specified user's available balance.|self: The method caller' address.<br>user: The specified user's address.|
|addUser|Add the address to be contract user. Once successfully added, the default available balance and balance recovery rate will be set automatically. (Only the contract user and contract itself have privilege to call this function.)|self: The method caller' address.<br>user: The specified user's address.|
|removeUser|Remove one contract user out of user list. (Only the contract user and contract itself have privilege to call this function.)|self: The method caller' address<br>user: The specified user's address.|
|sponsor|Contract sponsor.|self: The method caller' address.<br>yesOrNo(bool): <br>true: Become the contract sponsor candidates.<br>false: Delete from contract sponsor candidates list.|
|isSponsor|Check whether the specified user is contract sponsor or not.|self: The method caller' address.<br>sponsor：The specified address that is going to be checked.|
|selectSponsor|Select one candidate to be a contract sponsor from sponsor candidates list.|self: The method caller' address.<br>sponsor: The specified sponsor candidate's address in the contract sponsor candidates list.|
|currentSponsor|Return the current contract sponsor.|self: The method caller' address.|