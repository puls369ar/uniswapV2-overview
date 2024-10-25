# UniswapV2Factory [Contract](https://github.com/Uniswap/v2-core/blob/master/contracts/UniswapV2Factory.sol)

# Mappings and Arrays
* `getPair` - Addresses of `UniswapV2Pair` instances mapped from these pair's token addresses
* `allPairs` - The actual `UniswapV2Pair` addresses

LIF3
  
* `mintFee` -
* `swapFee` -

/LIF3

# Variables
* `feeTo` - The address where fees will be sent
* `feeToSetter` - The account authorized to set `feeTo` address

LIF3
  
* `defaultMintFee`
* `defaultSwapFee`
  
/LIF3

# Fucntions

* `constructor()` - Initializes the contract by setting the feeToSetter. LIF3 Defines the `defaultMintFee` and `defaultSwapFee` /LIF3
* `allPairsLength()` - Returns the total number of liquidity pairs created by the factory (the length of the `allPairs` array)

* `createPair()` - Creates a new liquidity pair and deploys appropriate `UniswapV2Pair` contract instance between two ERC-20 tokens. It ensures the tokens are not identical, not zero-addressed, and checks for the pair to not already exist. Each pair is stored in a separate address and has separate fee values set to default. LIF3 Adds the appropriate fee values in `mintFee` and `swapFee` mappings (`defaultMintFee` and `defaultSwapFee` in our case) /LIF3. Emits the PairCreated event 

Setter functions for the `feeTo` and `feeToSetter` authority, only current `feeToSetter` authority is able to execute functions
* `setFeeTo()`
* `setFeeToSetter()`

LIF3
Below are the functions that let us modify `defaultSwapFee` and `defaultMintFee` values, also to change that values previously set in `mintFee` and `swapFee` mappings, when creating pair 
* `setMintFee()`
* `setSwapFee()`
* `setDefaultMintFee()`
* `setDefaultSwapFee()`
/LIF3

# Second Party Contracts
* `IUniswapV2Factory` -  To inherit the contract
* `UniswapV2Pair` - To get the bytecode for low-level instance creation
* `IUniswapV2Pair` - To create an instance
* `IUniswapV2Callee` - for the case when an external smart contract that implements `IUniswapV2Callee::uniswapV2Call()` function calls to  * `UniswapV2Pair::swap()` function

# Interface Diagram
* UniswapV2Factory<-IUniswapV2Factory
* UniswapV2Pair<-IUniswapV2Pair, {UniswapV2ERC20<-IUniswapV2ERC20}



