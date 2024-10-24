# UniswapV2Pair
Five main functions that implement AMM logic in UniswapV2Pair Smart Contract
* mint(address to) Mints new liquidity tokens based on token balances and reserves, updating reserves and locking minimum liquidity if it's the first deposit.
* burn(address to) Burns liquidity tokens, transfers the corresponding token0 and token1 amounts to the user, and updates reserves.
* swap(uint amount0Out, uint amount1Out, address to) Transfers tokens for a swap, checks inputs and outputs, and updates reserves after the swap.
* skim(address to) Transfers any excess token balances from the pair contract to the specified address.
* sync() Forces reserves to match the current token balances in the contract.
