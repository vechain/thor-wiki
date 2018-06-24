# Prototype(EN)

## Contract Code
 [prototype.sol](https://github.com/vechain/thor/blob/master/builtin/gen/prototype.sol)

## Contract Address
 `0x000000000000000000000050726f746f74797065`

>The above mentioned prototype contract address are same on both the testnet and mainnet.

##  Function

|Function|Description|Parameter|
|---|---|----|
|master|By default, the contract deployer is the contract initial master. The contract master's address will be returned as a result of calling this function.|self: The address to operate.|
|setMaster|Set the new contract master (Only the current contract master has privilege to do this operation.)|self: The address to operate.<br>newMaster: New contract master's address.|
|balance|Return the specified block's VTHO balance.|self: The address to operate.<br>blockNumber: Block number (The range of block number varies from 65535 ahead of latest block number to latest block number.)|
|energy|Return the specified block's VTHO balance.|self: The address to operate.<br>blockNumber: Block number (The range of block number varies from 65535 ahead of latest block number to latest block number.)|
|hasCode|check the account type of the contract caller (contract account/normal account).|self: The address to operate.|
|storageFor|The account model's content stored in storage.|self: The address to operate.<br>key: [Reference](https://solidity.readthedocs.io/en/latest/miscellaneous.html#layout-of-state-variables-in-storage)|
|userPlan|Return the user plan, the maximum credit, and recovery rate will be included in the user plan.|self: The address to operate.|
|setUserPlan|Set credit and recovery rate for all contract users.|self: The address to operate.<br>credit: The maximum balance that can be used(Wei).<br>recoveryRate: The credit recovery rate based on per second(Wei).|
|isUser|Check whether the account is a contract user.|self: The address to operate.<br>user: The specified user's address.|
|userCredit|Return the specified user's available credit.|self: The address to operate.<br>user: The specified user's address.|
|addUser|Add the address to be contract user. Once successfully added, the default available balance and balance recovery rate will be set automatically. (Only the contract master and contract itself have privilege to call this function.)|self: The address to operate.<br>user: The specified user's address.|
|removeUser|Remove one contract user out of user list. (Only the contract master and contract itself have privilege to call this function.)|self: The address to operate.<br>user: The specified user's address.|
|sponsor|Be a sponsor or not.|self: The address to operate.<br>yesOrNo(bool): <br>true: Become the contract sponsor candidates.<br>false: Delete from contract sponsor candidates list.|
|isSponsor|Check whether the specified user is a contract sponsor or not.|self: The address to operate.<br>sponsor：The specified address that is going to be checked.|
|selectSponsor|Select one candidate to be a contract sponsor from sponsor candidates list.|self: The address to operate.<br>sponsor: The specified sponsor candidate's address in the contract sponsor candidates list.|
|currentSponsor|Return the current contract sponsor.|self: The address to operate.|