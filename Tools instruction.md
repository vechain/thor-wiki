**Since this documentation is associated with sensitive information, such as account, the approaches mentioned by this documentation is only for reference.**

## ToolKit
1. [Java Client SDK](https://github.com/vechain/thor-client-sdk4j)
 > Documentation Directory : `file:///（projectPath）/doc/index.html`
2. [Sync](https://github.com/vechain/thor-Sync)
 > [GitHub Documentation](https://github.com/vechain/thor-sync/wiki/Sync-manual)

## Private Key Management
### Approach 1: Ethereum Account Management
- VeChainThor private key and address format compatible with Ethereum.
- Ethereum mnemonic words cannot be used in VeChainThor platform since coin type of 2 blockchains is different and the private keys generated in 2 blockchains are different.

If adopting the Ethereum toolkit and account management approach, you can refer to: [Ethereum Account Management Introduction]
(https://ethereum.gitbooks.io/frontier-guide/content/managing_accounts.html)

### Approach 2: Sync

#### Account

| Sub-modules| Network | Description |
| --- | --- | --- |
| create  | MainNet / TestNet | Allow user to create an account or more, the address will be unique ID on blockChain |
| export key store| MainNet / TestNet  | Export the key store and save to custom path. its for recovery use  |
| export private key| MainNet / TestNet  | Export the private key and save to custom path. its for recovery use  |
| import Key Store | MainNet / TestNet | Input the key store to recover account. |
| mnemonic recovery | MainNet / TestNet | During account creation, it ask user to write down and keep it safe. the mnemonic words can recover account.|
| import private key | MainNet / TestNet | Input the private key to recover account. |

#### Account UI

The interface includes 2 parts, besides the navigation area.
1: Account Import/Create

* Wallet list
* Create
* Import（Key Store/Private Key）  
* Mnemonic word

2: Account information and detailed manipulation

* Account address, balance display 
* Delete account 
* Change exchange password
* Export key store 
* Export private key

----

### Approach 3: Java Client SDK

Please Refer To<br>
API：
[AccountClient](https://github.com/vechain/thor-client-sdk4j#accountclient)<br>
Console：
[Create Wallet](https://github.com/vechain/thor-client-sdk4j#create-wallet)

## Transaction Building And Signature
The definition of transaction models field can be referred to: https://github.com/vechain/thor/wiki/Transaction-Model

It is suggested to fetch 2 parameters from the blockchain in real time when establishing transactions in VeChainThor.
- `chainTag`, the last byte of genesis, used for differentiating tag of mainnet and testnet respectively.
- `blockRef`, the uint64 type variable, the first 8 bytes of block id, taken by the transaction model as a reference. Meanwhile, it is used together with expiration field as an estimation of validation of a transaction. If the current blocknumber > blockRef () + expiration, the transaction is discarded.

### Approach 1: Sync
### Transaction Builder

Besides the navigation part, the UI includes 2 areas, the upper and lower:
Area 1: Select the type of transaction to be built

* Single Transaction  
* Multi Transaction 
* Contract Deployment

Area 2: The transaction content to be built

* Because of the unique feature of VeChainThor, some parameters are set to be filled by user.

#### Single Transaction
The single transaction is like Ethereum, sent from one sender to another receiver.

| Fields | Description | Remarks |
| --- | --- | --- |
| from | The transaction sender address |-  |
| to  | The transaction receiver address |-  |
| value | Amount transferred to the receiver| Unit :VET |
| expiration | Number of blocks that can be used to specify when the transaction expires/invalid |Suggestion: 720 <br> Block Number ∈[blockRef.number , BlockRef.number + expiration] |
| maximum gas |Amount gas allowed to be used |- |

#### Multi-Transaction 
One transaction can include 0 or multiple clauses, users do not need to use contract to execute multiple tasks; At the meantime, the transaction atomicity is ensured (Atomicity means the operation is either all succeed, or all fail). For example, clauses make it possible to send messages to multiple receivers within one transaction whereas a conventional transaction is restricted to send message to only one receiver. 

| Fields | Description | Remarks |
| --- | --- | --- |
| from | Transaction sender address | - |
| expiration | Number of blocks that can be used to specify when the transaction expires/invalid | Suggestion: 720 <br> Block Number ∈[blockRef.number , BlockRef.number + expiration]  |
| to | Transaction receiver | - |
| value | Amount of VET | - |
| data | Content in hex format | - |

#### Contract Deployment
Deploy the contract into VeChainThor network.

|Fields | Description | Remarks |
| --- | --- | --- |
| contract deployer | Contract deployer | select from account list|
| contract data | The hex data of compiled contract | user needs to manually convert the contract to be hex format |
| expiration | Number of blocks that can be used to specify when the transaction expires/invalid | Suggestion: 720 <br> Block Number ∈[blockRef.number , BlockRef.number + expiration]  |  
| maximum gas | The amount of gas needs to be consumed|unit:Wei |

#### Advanced parameter Setting
**The fields below are all optional parameters**

|Fields | Description | Remarks |
| ------- | ------ | ------ |
| gasPriceCoef | Coefficient used to calculate the total gas price	 | `0` as default value，which ∈[0,255] |
| dependsOn  | ID of the transaction on which the current transaction depends | if dependsOn is NOT `null`, then only the transaction was successfully on chain will be executed.|
| blockRef | Reference to a specific block | `best block number` as default value |



## Send transaction

### Approach 1: Sync

Once a transaction has been built, with correct password of the sender inputted, a user can sign the transaction then.

---
### Approach 2: Java Client SDK
1. API :<br>
For details, refer to <br>
1.[Sign VET transaction](https://github.com/vechain/thor-client-sdk4j#sign-vet-transaction)<br>
2.[Sign VTHO transaction](https://github.com/vechain/thor-client-sdk4j#sign-vtho-transaction)

2. console:<br>
For details, please refer to [Sign VET transaction](https://github.com/vechain/thor-client-sdk4j#sign-vet-transactions)

## MPP Related
For details, refer to:<br>
1.[Prototype](https://github.com/vechain/thor/wiki/Prototype(EN))<br>
2.[Prototype Client](https://github.com/vechain/thor-client-sdk4j#prototypeclient)

### Credit Plan setup

```
Amount credit = Amount.VTHO();
credit.setDecimalAmount( "12.00" );//maximum credits(VTHO) for users
Amount recovery = Amount.VTHO();
recovery.setDecimalAmount( "0.00001" );//credits(VTHO) recovery rate per second  

TransferResult result = ProtoTypeContractClient.setCreditPlans(
        new Address[]{Address.fromHexString( "0xD3EF28DF6b553eD2fc47259E8134319cB1121A2A")},
        new Amount[]{credit},
        new Amount[]{recovery},
        ContractClient.GasLimit, (byte)0x0, 720, ECKeyPair.create( "0xeb78d6405ba1a28ccd938a72195e0802dfbe1de463bc6e5dd491b2c7562b5e3f" ) );
logger.info( "set credit plans:" + JSON.toJSONString( result ) );
```


Assume that the current transaction fee is 21 THO (always subject to the actual network parameter). When setting the credit Plan, you wish to limit the action to one user per day and gradually restore it. Then you can set credit plan's credit and recoveryRate as below:

```
1.credit ： credit.setDecimalAmount( "21.00" )
2.recoveryRate:  recovery.setDecimalAmount( "0.00024305555" ) // 0.00024305555 = 21 / 86400
```

## BlockChain Info Query
### Approach 1: Sync
Insights is able to visualize the VeChainThor data and display it in real time. User can query the blockchain information by the following contents.

#### Latest block/Block query/Block ID
By default, when accessing insights, insights automatically loads the latest block and query the info of it in real time. The specified block info can be queried by inputting block ID/number. 
>If Branch label exists, that represents the block is not in the mainnet.

|Fields | Description |
| --- | --- |
| block number | Number(height) of the block |
| block ID |Identifier of the block |
| size | Byte size of the block that is RLP encoded |
| parent ID | Block ID of parent block |
| timestamp  | Timestamp |
| total Score | Cumulative block score since genesis block |
| number of Transaction | Number of transaction in the block |
| gas limit  | The amount of gas used by the block |
| signer  | Who signed the block |
| beneficiary  | An address of account to receive block reward |
| txRoot | Root hash of transactions in the block |
| stateRoot | Root hash of account state |
| receiptsRoot |  Root hash of transaction receipts |

#### Transaction Query
Because the Insights queries the info on chain, all the transactions have receipt. 
>If Branch label exists, that represents the block is not in the main chain.

**Tx Info**

| Fields | Description |
| --- | --- |
| txID  | Identifier of the transaction |
| timeStamp  | Timestamp |
| from  | Transaction sender |
| block Number | Number of the block |
| block Id  | Identifier of the block |
| block Ref | Reference to a specific block |
| depends On | ID of the transaction which the transaction depends |
| nonce | Transaction nonce |
| gas | Maximum amount of gas the sender is willing to pay for the transaction |
| expiration | Number of blocks that transaction expires |
| gas used by transaction | The total amount of Gas used in the actual transaction|
| gas price Coefficient | Coefficient used to calculate the total gas price, which ∈[0 , 255]. |
| clauses | An array of "clause" objects each of which contains fields "To", "Value" and "Data" |
| to | Receiver 's address |
| value | Amount transferred to the receiver |
| data | Either the EVM code for account initialization or some input data (hex type)|
---

**Receipt**

|Fields | Description |
| --- | --- |
| gas Payer | An address who paid the transaction |
| paid (VTHO) | Amount of VTHO cost |
| tx Reward (VTHO) | Transaction reward for proposer |
| outputs | Event Logs |


#### Address Query
Query the corresponding according to the address.

 Fields | Description |
| --- | --- |
| address | Address of account|
| available VET | Available VET balance of address |
| available VTHO | Remaining VTHO |
| transactions | The detailed information of a sent transaction |


### Approach 2: Java Client SDK
For details, refer to<br>
1.[API](https://github.com/vechain/thor-client-sdk4j#query-transaction)
2.[java console](https://github.com/vechain/thor-client-sdk4j#4-java-console-approach)

## Confirm Transaction
#### 1. Get Block
Use java console command:

```
1.console:
java -jar thor-client-sdk4j-0.0.2.jar getBlock "http://localhost:8669"

2. API:
// get best block
Block block = BlockClient.getBlock(Revision.BEST);   
System.out.println(JSON.toJSONString(block));    

or

// get specified block
Revision revision = Revision.create(148847);
Block block = BlockClient.getBlock(revision);
System.out.println(JSON.toJSONString(block));

```
- best block

```
{
  "beneficiary": "0xafbd76f9cdd19015c2d322a35bbea0480f5d70e1",
  "gasLimit": 10448965,
  "gasUsed": 0,
  "id": "0x00026bfa7cbbd7c8cf643e45eadff1ddce1395cc47a5c08c521498f693381840",
  "isTrunk": true,
  "number": "158714",
  "parentID": "0x00026bf9c0828062b25d0b23df0c99f6571af389d273961b82c90906a0a96b1b",
  "receiptsRoot": "0x45b0cfc220ceec5b7c1c62c4d4193d38e4eba48e8815729ce75f9c0ab0e4c1c0",
  "signer": "0xafbd76f9cdd19015c2d322a35bbea0480f5d70e1",
  "size": 239,
  "stateRoot": "0xa8dd31b95e227b92e800d65c824d2fb124a36e924b398252ec995d3611a69d43",
  "timestamp": 1530016140,
  "totalScore": 1034108,
  "transactions": [],
  "txsRoot": "0x45b0cfc220ceec5b7c1c62c4d4193d38e4eba48e8815729ce75f9c0ab0e4c1c0"
}
```

- specified block

```
{
  "beneficiary": "0x0000000000000000000000000000000000000000",
  "gasLimit": 10000000,
  "gasUsed": 0,
  "id": "0x00000000ef3b214ad627b051f42add3b93b2f913f2594b94a64b2377b0f9159a",
  "isTrunk": true,
  "number": "0",
  "parentID": "0xffffffff00000000000000000000000000000000000000000000000000000000",
  "receiptsRoot": "0x45b0cfc220ceec5b7c1c62c4d4193d38e4eba48e8815729ce75f9c0ab0e4c1c0",
  "signer": "0x0000000000000000000000000000000000000000",
  "size": 170,
  "stateRoot": "0x120df3368f409525ed30fd98c999af8d66bfa553cae14005fc3b7f00bcc60de1",
  "timestamp": 1528387200,
  "totalScore": 0,
  "transactions": [],
  "txsRoot": "0x45b0cfc220ceec5b7c1c62c4d4193d38e4eba48e8815729ce75f9c0ab0e4c1c0"
}
```

>The transaction field is the txID of all the transactions inside of this block.

#### 2. Get the Transaction
Use java console command:


```
1.java console:
java -jar thor-client-sdk4j-0.0.2.jar getTransaction "0x255576013fd61fa52f69d5d89af8751731d5e9e17215b0dd6c33af51bfe28710"  "http://localhost:8669"

or
2.java api
Transaction transaction = TransactionClient.getTransaction("0x255576013fd61fa52f69d5d89af8751731d5e9e17215b0dd6c33af51bfe28710", false, null);
System.out.println("transaction"+JSON.toJSONString(transaction));
```
Return the transaction info:

```
{
id: '0x255576013fd61fa52f69d5d89af8751731d5e9e17215b0dd6c33af51bfe28710',
  chainTag: '0x9a',
  blockRef: '0x0002456e56ae5827',
  expiration: 720,
  clauses: 
    [
      {
      "to": "0xB2ef3293Bb6c886d9e57ba205c46450B6d48A0A1",
      "value": "1234560000000000000",
      "data": "0x"
      },
      {
      "to": "0x0000000000000000000000000000456E65726779",
      "value": "0",
      "data": "0xa9059cbb000000000000000000000000b2ef3293bb6c886d9e57ba205c46450b6d48a0a100000000000000000000000000000000000000000000000000000000000003ff"
       } 
    ],
  gasPriceCoef: 0,
  gas: 100000,
  origin: '0x267Dc1dF3e82E6BdAD45156C7c31Aad36DF2B5Fa',
  nonce: '0x164362fbdd0',
  dependsOn: null,
  size: 224,
  meta: 
   { blockID: '0x0002456fe81e6df0548a327faa3c1764eff7c3b7ce5cf1d1d27264818e78ea8c',
     blockNumber: 148847,
     blockTimestamp: 1529917460 },
  blockNumber: 23426 }
}
```

The transaction detailed content from the returned transaction information can be browsed.

#### 3. Get the transaction receipt.

```
1.java console:
java -jar thor-client-sdk4j-0.0.2.jar getTransactionReceipt "0x255576013fd61fa52f69d5d89af8751731d5e9e17215b0dd6c33af51bfe28710"  "http://localhost:8669"



2.java api
Receipt receipt = TransactionClient.getTransactionReceipt("0x255576013fd61fa52f69d5d89af8751731d5e9e17215b0dd6c33af51bfe28710", null);
System.out.println("receipt"+JSON.toJSONString(receipt));
```

Return transaction receipt info: a transaction includes 2 clauses, one of which is VET transfer while another of which is VTHO transfer.

```
{
  "gasUsed": 51462,
  "gasPayer": "0x267Dc1dF3e82E6BdAD45156C7c31Aad36DF2B5Fa",
  "paid": "0x2ca2dc057b7270000",
  "reward": "0xd640ece71d588000",
  "reverted": false,
  "meta": {
    "blockID": "0x0002456fe81e6df0548a327faa3c1764eff7c3b7ce5cf1d1d27264818e78ea8c",
    "blockNumber": 148847,
    "blockTimestamp": 1529917460,
    "txID": "0x255576013fd61fa52f69d5d89af8751731d5e9e17215b0dd6c33af51bfe28710",
    "txOrigin": "0x267Dc1dF3e82E6BdAD45156C7c31Aad36DF2B5Fa"
  },
 "outputs": [
        {
            "contractAddress": null,
            "events": [],
            "transfers": [
                {
                    "sender": "0x267dc1df3e82e6bdad45156c7c31aad36df2b5fa",
                    "recipient": "0xb2ef3293bb6c886d9e57ba205c46450b6d48a0a1",
                    "amount": "0x112209c76de80000"
                }
            ]
        },
        {
            "contractAddress": null,
            "events": [
                {
                    "address": "0x0000000000000000000000000000456E65726779",
                    "topics": [
                        "0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef",
                        "0x000000000000000000000000267dc1df3e82e6bdad45156c7c31aad36df2b5fa",
                        "0x000000000000000000000000b2ef3293bb6c886d9e57ba205c46450b6d48a0a1"
                    ],
                    "data": "0x00000000000000000000000000000000000000000000000000000000000003ff"
                }
            ],
             "transfers": []
    }
  ]
}
```

#### 4. Verify the validation of a transaction
- It is suggested that transaction confirmation block should over `12`.
- Transactions in the block are successfully executed. To validate the transaction, `reverted` field of transaction receipt can be referred to. If `reverted` field is false, the transaction is successfully executed and vice verse.

- Inside of the transaction receipt, Output will show this transaction's transfer info.
    ###### 1. VTHO:
    If its VTHO transfer，you can look into `events` in Output. Description is as follows:
    1. Contract needs to be confirmed `0x0000000000000000000000000000456e65726779`
    2. Topics:
    
       * Item 1: events call hashes, it is compulsory to **ensure**hash value is `0xddf252ad1be2c89b69c2b068fc378daa952ba7f163c4a11628f55a4df523b3ef`.
       * Item 2: The transaction sender.
       * Item 3: The transaction receipt.
      
    3. data: the transfer value, by default, the return value is hex, the unit of which is 10^18    (Wei). For example, the above data value is: 0x3ff = 1023 wei VTHO, i.e. 1023*10^-18    VTHO.
    
    ###### 2. VET:
     The `transfer` array in the Output includes transaction `sender`, `recipient`, `amount` (the amount of gas transferred).
    >  `amount` - By default, the return value is hex, the unit of which is 10^18 （Wei). For example, the transfers of above receipt is a hex: 0x112209c76de80000, which can be converted into 10 band as 1234560000000000000 wei. VET is of 18decimal type, thus it can be converted as 1.23456 VET.

#### 5. Transaction fee calculation

VeChainThor blockchain transaction consumes gas, gas is converted into VTHO based on gasPrice and account VTHO is deducted to calculate the transaction fee. 
The calculation equation is:
`VTHO = (1 + gasPriceCoef/255) * baseGasPrice`

Current mainnet set baseGasPrice to be: 1 VTHO = 1000gas (always subject to the actual network parameter). The VET transfer fee is 21000gas. If gasPriceCoef = 0, the used `VTHO = (1 + 0/255) * 21000/1000 = 21 VTHO`

- The priority of a transaction in transaction pool can be raised by adjusting gasPriceCoef. For example, if gasPriceCoef =128, `used VTHO = (1 + 128/255) * 21000/1000 = 31.5 VTHO`





