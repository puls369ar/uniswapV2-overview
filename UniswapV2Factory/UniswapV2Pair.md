# UniswapV2Pair [Contract](https://github.com/Uniswap/v2-core/blob/master/contracts/UniswapV2Pair.sol)

The contract that describes token pair inside the liquidity pool of UniswapV2



# Modifiers
* `lock` - All main functions apply this modifier. If `unlocked` variable is 0 they will be reverted

# Variables&Constants
uint public constant MINIMUM_LIQUIDITY = 10**3;
bytes4 private constant SELECTOR = bytes4(keccak256(bytes('transfer(address,uint256)')));

* `address public factory` - Address of the factory to get a fee collector's address from it's instance
* `address public token0` - Address of pair's first token
* `address public token1` - Address of pair's second token
* `uint112 private reserve0` - Amount of `token0` in the pool
* `uint112 private reserve1` - Amount of `token1` in the pool
* `uint32 private blockTimestampLast` - Latest timestamp when reserves were updated by un `_update()` function
Cumulative prices don't represent the current price directly but a running total of the price * time
* `uint public price0CumulativeLast` - The cumulative price is the integral (or sum) of the price of `token0` relative to token1 over time. 
* `uint public price1CumulativeLast` - The cumulative price is the integral (or sum) of the price of `token1` relative to token1 over time
* `uint public kLast` - reserve0 * reserve1, as of immediately after the most recent liquidity event




# Functions

Key functions
* `initialize(address _token0, address _token1)` — Initializes the pair with two tokens (token0 and token1). Called only once during pair creation 
  by the factory contract
* `mint(address to)` — Mints liquidity provider (LP) tokens to the specified address when liquidity is added to the pool
* `burn(address to)` — Burns LP tokens and returns corresponding token0 and token1 amounts to the user, updating the reserves
* `swap(uint amount0Out, uint amount1Out, address to, bytes calldata data)` — Executes a token swap, sending tokens to the recipient and optionally 
  supports flash swaps
* `sync()` — Synchronizes the reserves with the actual token balances the contract holds
* `skim(address to)` — Sends any excess tokens in the contract (not part of reserves) to the specified address

Helper core functions
* `_update(uint balance0, uint balance1, uint112 _reserve0, uint112 _reserve1)` — Updates reserves and cumulative price information used for TWAPs
* `_mintFee(uint112 _reserve0, uint112 _reserve1)` — Collects protocol fees (if applicable), minting LP tokens as fees
* `_mint(address to, uint amount)` — Internal function that mints LP tokens and sends them to the specified address
* `_burn(address from, uint amount)` — Internal function that burns LP tokens from the specified address

View/Pure Functions
* `getReserves()` — Returns the current reserves of token0 and token1, along with the last block timestamp when reserves were updated.
* `price0CumulativeLast()` — Returns the last cumulative price of token0, used for TWAP calculations.
* `price1CumulativeLast()` — Returns the last cumulative price of token1, used for TWAP calculations.

# Second Party Contracts, Libraries, Interfaces
* `IUniswapV2Pair` – Main interface to inherit from
* `IERC20`, `IUniswapV2Factory`  – To create instances
* `UniswapV2ERC20` - This contract implements the ERC20 token standard for Uniswap LP tokens
* `Math` - Provides safe mathematical operations to avoid overflow and underflow issues in calculations
* `UQ112x112` - Handles fixed-point arithmetic for precise calculations involving prices and liquidity in Uniswap

# Interface Diagram
UniswapV2Pair->(IUniswapV2Pair,UniswapV2ERC20->IUniswapV2ERC20)
