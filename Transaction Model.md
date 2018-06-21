# Transaction Model
The VeChainThor Blockchain adopts a new transaction model to solve some of the fundamental
problems that hinder a broader use of blockchain at the moment. Specifically, a VeChainThor
Blockchain transaction includes the following fields:

- `chainTag` : `uint8`, **last byte** of the genesis block ID.
- `blockRef`  : `uint64` Default is **best block**, The BlockRef(an eight-byte array) includes two parts: the first four bytes contains the block height (number) and the rest four bytes a part of the referred block’s ID.if its future block should put blockNumber+"00000000".
- `expiration` : `uint32` Default is **0** . Number of blocks that can be used to specify when the transaction expires[1].Specifically, Expiration+BlockRef[:4] defines the height of the latest block that the transaction can be packed into.
- `clauses` : `array` an array of “clause” objects each of which contains fields “To”, “Value” and
“Data” to enable single “from” coupling with multiple “to”
- `from`  : `string` ,20bytes, The address for the sending account.
- `to` (optional) : `string`,20bytes, The destination address of the message, left undefined for a contract-creation transaction. 
- `value`(optional) :`string(hex)`,  The value transferred for the transaction in **Wei**, also the endowment if it’s a contract-creation transaction. 
- `gasPriceCoef` :`uint8` , Default is **0**, gasPriceCoef required range of  **∈[0,255]** . [2]
- `gas`  :`uint64`, The amount of gas to use for the transaction.
- `dependsOn`: `string`, ID of the transaction on which the current transaction depends
- `nonce`  ：`uint64`   transaction nonce customizable by user .
- `reserved`  : `array` **Must be empty array**.
- `Signature` : signature of the hash of the transaction body 𝛺, that is, 𝑠𝑖𝑔𝑛𝑎𝑡𝑢𝑟𝑒 =
𝑠𝑖𝑔𝑛(ℎ𝑎𝑠ℎ(𝛺), 𝑝𝑟𝑖𝑣𝑎𝑡𝑒_𝑘𝑒𝑦).

[1]If you want the transaction expire after **120** minutes , then you can set  expiration as **`720`**(block).

[2]if you set gasPriceCoef as **`128`** then the price of transaction is nearly *1.5x* of base price but higher priority than without set the gaspriceCoef.




## Transaction ID vs Account Nonce
In the Ethereum account model, the account nonce is used as a counter to make sure each transaction can only be used once. Although it provides a solution to replay attacks, in practice such a mechanism has proven to be troublesome, especially for enterprise users. For instance, if a user sends out multiple transactions at the same time (which is very likely for an enterprise user when, for example, registering products or updating records) and one transaction fails, all those with a larger nonce would be rejected by Ethereum nodes. 

We scrap the account-nonce mechanism and introduce the concept of the transaction ID. In the VeChainThor Blockchain, every transaction is given a unique ID, 𝑇𝑥𝐼𝐷, which can be calculated as:

```
𝑇𝑥𝐼𝐷 = ℎ𝑎𝑠ℎ(ℎ𝑎𝑠ℎ(𝛺), 𝑠𝑖𝑔𝑛𝑒𝑟_𝑎𝑑𝑑𝑟𝑒𝑠𝑠)
```

>1. where 𝛺 is the set that contains all the transaction fields listed above except the field “Signature”
>2. ```Signer_address = ECRecover(ℎ𝑎𝑠ℎ(𝛺),Signature)```
>3. where 𝛺 is using BLAKE2b cryptographic hash function  

In the VeChainThor Blockchain, when validating a given transaction, instead of checking the current account nonce, the system computes its 𝑇𝑥𝐼𝐷 and checks whether it has been used before.

## Transaction Dependency

Every VeChainThor transaction includes novel fields DependsOn, BlockRef and Expiration related to transaction dependency. 

- DependsOn stores the ID of the transaction on which the current one depends. In other words, the current transaction cannot be validated without the success of the transaction referred by DependsOn. Here by “success”, we mean that the referred transaction has not only been included in the blockchain but been executed successfully (without any error returned by the system).

- BlockRef stores the reference to a particular block whose next block is the earliest block the current transaction can be packed. The reference (an eight-byte array) includes two parts: the first four bytes contains the block height (number) and the second four bytes a part of the referred block’s ID. In practice, the second part of BlockRef does not have to be assigned value if the block is not available (e.g. a block in the future).

- Expiration stores the number of blocks that can be used to specify when the transaction expires. Specifically, Expiration plus BlockRef[:4] (this refers to the integer value of the first four bytes of BlockRef) defines the height of the latest block that the transaction can be packed into.
>
``` 
Block Number ∈[blockRef.number , BlockRef.number + expiration] 
```


## Multi-task Transaction
Another novel built-in feature is that the VeChainThor Blockchain allows a single transaction to carry out multiplegit tasks. To do that, we define the “Clause” structure that represents a certain on blockchain task. Each Clause contains three fields:

- To – recipient’s address
- Value – amount transferred to the recipient
- Data – either the EVM code for account initialization or some input data

We then define field “Clauses” as a set of Clause objects in the transaction model to make it possible for a transaction to conduct multiple tasks. The “Clause” model may remind you of the classic BitCoin “UTXO” model since both models allow a transaction to have multiple output. However, with “Clauses” users can do a lot more than a set of output balance information can.

The multi-task mechanism has two main characteristics:

- Since the tasks are contained in a single transaction, their executions can be considered as an atomic operation, meaning that, they either all succeed, or all fail. 
- During the transactions execution, the included tasks are processed one by one in the order defined by the fields Clauses

