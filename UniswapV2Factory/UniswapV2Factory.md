# UniswapV2Factory

* constructor - Initializes the contract by setting the feeToSetter and defining the defaultMintFee and defaultSwapFee

* allPairsLength - Returns the total number of liquidity pairs created by the factory (the length of the allPairs array)

* createPair() - Creates a new liquidity pair and deploys appropriate `UniswapV2Pair` contract instance, between two ERC-20 tokens. It ensures the tokens are not identical, not zero-addressed, and checks that the pair doesn’t already exist. Each pair is stored in a separate address and has
separate fees value that are set to default ones. Can be changed by `feeToSetter`authority in setter functions. After creation, it assigns the default mint and swap fees to the pair and emits the PairCreated event

Setter functions for the fees and fee authority, only current `feeToSetter` authority is able to execute functions
* setFeeTo
* setFeeToSetter
* setMintFee
* setSwapFee
* setDefaultMintFee
* setDefaultSwapFee

# All used Interfaces, their relations and descriptions
* UniswapV2Factory<-IUniswapV2Factory
* UniswapV2Pair<-IUniswapV2Pair, {UniswapV2ERC20<-IUniswapV2ERC20}
* `IUniswapV2Callee` for the case when external smart contract that implements `IUniswapV2Callee::uniswapV2Call()` function calls to  * `UniswapV2Pair::swap()` function
* `IERC20` to check the balances from the token contract


