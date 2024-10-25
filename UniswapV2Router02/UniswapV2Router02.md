# UniswapV2Router02 [Contract](https://github.com/Uniswap/v2-periphery/blob/master/contracts/UniswapV2Router02.sol)

The contract that describes token pair inside the liquidity pool of UniswapV2



# Modifiers
`ensure` - checks if the value of `deadline` is bigger then `block.timestamp`

# Variables&Constants
* `address public immutable override factory` - Address of the `UniswapV2Factory` instance to communicate with
* `address public immutable override WETH` - Address of the used chain's wrapped native token  

# Functions
* `constructor(address _factory, address _WETH)` - It takes two parameters for arguments `_WETH` and `_factory`. We may deploy our Uniswap contract to other EVM compatible chains. In that case the address of it's native wrapped token will be different

Key functions
* `addLiquidity(
      address tokenA,
      address tokenB,
      uint amountADesired,
      uint amountBDesired,
      uint amountAMin,
      uint amountBMin
    )` - by using core helper `_addLiquidity()` function it gets valid amounts and transfers (using `SafeTransfer.transferFrom()`) tokens to the `UniswapV2Pair` instance (got by `UniswapV2Library.pairFor()` function having token addresses and `factory` s an input) and after LP token is minted from that instance to the given address
* `addLiquidityETHaddress token,
        uint amountTokenDesired,
        uint amountTokenMin,
        uint amountETHMin,
        address to,
        uint deadline
)` - Has the same purpose as `addLiquidity` but for ETH/Token pairs


Removal functions have their variations where they implement *withPermit* and *FeeOnTransfer* functionalities. The latest is a mandatory to manage fee-demanding tokens while those are being transferred back to the holder (when creating we pay it separately, not from the tokens provided for the liquidity)

* `removeLiquidity(
        tokenA,
        address tokenB,
        uint liquidity,
        uint amountAMin,
        uint amountBMin,
        address to,
        uint deadline`) - `UniswapV2Pair()` instance is restored by `UniswapV2Library.pairFor()` function from token and `factory` addresses. After which the LP token is returned from the holder and the tokens inside are returned back to the holder (specified address). Functions below implement the same behaviour, but for ETH/Token pairs and functionalities mentioned above
* `removeLiquidityETH`
* `removeLiquidityETHSupportingFeeOnTransferTokens`
* `removeLiquidityWithPermit`
* `removeLiquidityETHWithPermit`
* `removeLiquidityETHWithPermitSupportingFeeOnTransferTokens`

Swap functions also provide different variations for the tokens that need *Fee on Transfer*

We provide exact amount for “investing” token and get calculated amount of “returning” Token
* `swapExactTokensForTokens`
* `swapExactTokensForTokensSupportingFeeOnTransferTokens`

We provide exact amount for “investing” ETH token and get calculated amount of “returning” Token
* `swapExactETHForTokens`
* `swapExactETHForTokensSupportingFeeOnTransferTokens`

We provide exact amount for “returning” token and get calculated amount of “investing” Token
* `swapTokensForExactTokens`

We provide exact amount for “returning” ETH token and get calculated amount of “investing” Token
* `swapTokensForExactETH`

We provide exact amount for “investing” token and get calculated amount of “returning” ETH Token
* `swapExactTokensForETH`
* `swapExactTokensForETHSupportingFeeOnTransferTokens`

We provide exact amount for “returning” token and get calculated amount of “investing” ETH Token
* `swapETHForExactTokens`

All of them function almost the same. Let's view the one
`function swapExactTokensForTokens(
        uint amountIn,
        uint amountOutMin,
        address[] calldata path,
        address to,
        uint deadline
)` - First it calls `UniswapV2Library.getAmountsOut()` function by providing `factory` and inputed amount and token's addresses wrapped in an array. As a result it get's the amount that will be returned to him duirng the swap together with inputed token amount in one array. Then the transfer is performed by `SafeTransfer.transferFrom()` function where **caller** sends tokens to the liquidity pair. Inside core `_swap()` function that is the next line code, instance of appropriate `UniswapV2Pair` contract is created and amounts of another token are transferred back to the specified address via `UniswapV2Pair::swap()` function 



Helper core functions
* `function _addLiquidity(
        address tokenA,
        address tokenB,
        uint amountADesired,
        uint amountBDesired,
        uint amountAMin,
        uint amountBMin
)` - 

* `function _swap(uint[] memory amounts, address[] memory path, address _to)` - instance of appropriate `UniswapV2Pair` contract is created and amounts of another token that are in the pool are transferred back to the specified address via `UniswapV2Pair::swap()` function


# Second Party Contracts, Libraries, Interfaces
* `IUniswapV2Router02` – Main interface to inherit from
* `IERC20`, `IUniswapV2Factory`, `IWETH`  – To create instances
* `TransferHelper` - This library provides set of functions to execute token transfers safe
* `UniswapV2Library` - Library with functions to work with `UniswapV2Pair` instances, in our case restoring the one from `factory` and token 
  addresses for example
* `SafeMath` -  provides arithmetic functions with built-in safety checks to prevent common issues like integer overflow and underflow. It expands 
  functionality of type `uint` in our contract


# Interface Diagram
UniswapV2Router->IUniswapV2Router02->IUniswapV2Router01


