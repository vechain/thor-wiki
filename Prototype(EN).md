# Prototype(EN)

## Contract Code
 [prototype.sol](https://github.com/vechain/thor/blob/master/builtin/gen/prototype.sol)

## Contract Address
 `0x000000000000000000000050726f746f74797065`

>The above mentioned prototype contract address is same on both the testnet and mainnet.


##  Function

|Function|Description|Parameter|
|---|---|----|
|master|By default, the contract deployer is the contract master;Return  contract master's address|self: The address to be operated.|
|setMaster|Set the new contract master (Only the current contract master and contract itself have privilege to call this function).|self: The address to be operated<br>newMaster: The new contract master's address.|
|balance|Return the specified block's VET balance.|self: The address to be operated.<br>blockNumber: Block number (BlockNumber ∈ [latest block - 65535, latest block]).|
|energy|Return the specified block's VTHO balance.|self: The address to be operated.<br>blockNumber: Block number (BlockNumber ∈ [latest block - 65535, latest block]).|
|hasCode|Check the message sender's account type(contract account/normal account).|self: The address to be operated.|
|storageFor|The account model's content stored in storage.|self: The address to be operated.<br>key: [Reference](https://solidity.readthedocs.io/en/latest/miscellaneous.html#layout-of-state-variables-in-storage)|
|creditPlan|Return the credits plan and credit's recovery rate.|self: The address to be operated.|
|setCreditPlan|Set the credits and recovery rate for all users of the contract (Only the current contract master and contract itself have privilege to call this function).|self: The address to be operated.<br>credit: The planned credit(Wei) set by either contract or contract holder.<br>recoveryRate: The credit recovery rate based on per second(Wei).<br> When arriving the peak, the credit is not going to grow.|
|isUser|Check whether the specified account is a user of the contract.|self: The address to be operated.<br>user: The specified user's address.|
|userCredit|Return the specified user's remaining credit.|self: The address to be operated.<br>user: The specified user's address.|
|addUser|Add the address to become contract's user. Once successfully added, the default credits and credit recovery rate will be set as default value by setCreditPlan function (Only the current contract master and contract itself have privilege to call this function).|self: The address to be operated.<br>user: The specified user's address.|
|removeUser|Remove specified address from contract's user list (Only the current contract master and contract itself have privilege to call this function).|self: The address to be operated.<br>user: The specified user's address.|
|Sponsor|Become a sponsors in the sponsor list .|self: The address to be operated.|
|unSponsor|Remove 'self' in the sponsor list .|self: The address to be operated.|
|isSponsor|Check whether the specified address is listed on contract's sponsor list or not.|self: The address to be operated.<br>sponsor：The specified address that is going to be checked.|
|selectSponsor|Select one sponsor to become contract's sponsor from contract sponsor list (Only the current contract master and contract itself have privilege to call this function).|self: The address to be operated.<br>sponsor: The specified sponsor's address in the sponsor list.|
|currentSponsor|Return current sponsor.|self: The address to be operated.|