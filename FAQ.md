## FAQ

### VeChainThor explorer 
So far, the VeChainThor explorer is only available in Mac OS the usage and installation packages will be available shortly. Version for Windows OS currently is under development, which will be available later. Coming new version of VeChainThor client will have following features: explorer, transaction builder, and account management together with manual documentations. 

### Consensus
VeChainThor adopts the PoA (Proof-of-Authority) consensus protocol, instead of neither PoW (Proof-of-Work) nor PoS (Proof-of-Stake). Members in the whitelist requiring KYC (know-your-customer) identity verification are in charge of and responsible for the operation of the blockchain network. Concerning the safety issue, we leverage DPRP protocol to mess up the order of packer who pack the block, making sure the sequence of order of packers varies each time when packing the block. 


### Block Generation Speed
The default interval of block generation is 10 seconds, but the concrete timestamp interval depends on the specific situation.

### Orphan Generation/suggestion 
It is possible to generate orphan block and it is suggested to verify the fork situation every `12` block interval. 

### Dual token precision 
The precision of both `VET` and `VTHO` is 10^18 Wei. VTHO is generated from staking the VET and it is consumed for payments and smart contract execution on the VeChainThor blockchain


### Are the failed transactions going to be recorded on the chain? Is the transaction gas going to be deducted?

When you send tokens, interact with a contract, send `VET`/`VTHO`, or do anything else on the blockchain, you must pay for computation. That payment is calculated in Gas and gas is paid in VTHO. Regardless of whether your transaction succeeds or fails. Even if it fails, the proposer(authority node) must validate and execute your transaction (compute) and therefore you must pay for that computation just like you would pay for a successful transaction.

### How does the token swap from ERC20 VeChain token to VET work?
•The ticker symbol for the VeChainThor Mainnet token will changed to `VET`.

•Token swap ratio is 1:100. One ERC20 VeChain token will be split to 100 VETs on the VeChainThor Mainnet.

•In order to make it more user friendly to differentiate the VeChainThor address and Ethereum address, the display of the VeChainThor address will be customized in the UI by replace the first characters `0X` with `VX`. 

### Thorify
Thorify is a  web3 adaptor for VeChain Thor RESTful HTTP API. for more details please visit https://github.com/vechain/thorify.
