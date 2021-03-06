# ZyxSwap API

The ZyxSwap API is a set of endpoints used by market aggregators (e.g. coinmarketcap.com) to surface ZyxSwap liquidity
and volume information. All information is fetched from the underlying subgraphs.


# Documentation

All ZyxSwap pairs consist of two different tokens. ZYX is not a native currency in ZyxSwap, and is represented only by WZYX in the pairs.

The canonical WZYX address used by the ZyxSwap interface is `0xc9E1AEA009B0bAe9141F3dc7523fb42Fd48C8656`.

Results are cached for 5 minutes (or 300 seconds).

## [`/summary`](https://api.zyxswap.com/api/summary)

Returns data for the top ~1000 ZyxSwap pairs, sorted by reserves.

### Request

`GET https://api.zyxswap.com/api/summary`

### Response

```json5
{
  "updated_at": 1234567,              // UNIX timestamp
  "data": {
    "0x..._0x...": {                  // BEP20 token addresses, joined by an underscore
      "price": "...",                 // price denominated in token1/token0
      "base_volume": "...",           // last 24h volume denominated in token0
      "quote_volume": "...",          // last 24h volume denominated in token1
      "liquidity": "...",             // liquidity denominated in USD
      "liquidity_ZYX": "..."          // liquidity denominated in ZYX
    },
    // ...
  }
}
```

## [`/tokens`](https://api.zyxswap.com/api/tokens)

Returns the tokens in the top ~1000 pairs on ZyxSwap, sorted by reserves.

### Request

`GET https://api.zyxswap.com/api/tokens`

### Response

```json5
{
  "updated_at": 1234567,              // UNIX timestamp
  "data": {
    "0x...": {                        // the address of the BEP20 token
      "name": "...",                  // not necessarily included for BEP20 tokens
      "symbol": "...",                // not necessarily included for BEP20 tokens
      "price_ZYX": "...",             // price denominated in ZYX
    },
    // ...
  }
}
```

## [`/tokens/0x...`](https://api.zyxswap.com/api/tokens/0xc9E1AEA009B0bAe9141F3dc7523fb42Fd48C8656)

Returns the token information, based on address.

### Request

`GET https://api.zyxswap.com/api/tokens/0xc9E1AEA009B0bAe9141F3dc7523fb42Fd48C8656`

### Response

```json5
{
  "updated_at": 1234567,              // UNIX timestamp
  "data": {
    "name": "...",                    // not necessarily included for BEP20 tokens
    "symbol": "...",                  // not necessarily included for BEP20 tokens
    "price_ZYX": "...",               // price denominated in ZYX
  }
}
```

## [`/pairs`](https://api.zyxswap.com/api/pairs)

Returns data for the top ~1000 ZyxSwap pairs, sorted by reserves.

### Request

`GET https://api.zyxswap.com/api/pairs`

### Response

```json5
{
  "updated_at": 1234567,              // UNIX timestamp
  "data": {
    "0x..._0x...": {                  // the asset ids of ZYX and BEP20 tokens, joined by an underscore
      "pair_address": "0x...",        // pair address
      "base_name": "...",             // token0 name
      "base_symbol": "...",           // token0 symbol
      "base_address": "0x...",        // token0 address
      "quote_name": "...",            // token1 name
      "quote_symbol": "...",          // token1 symbol
      "quote_address": "0x...",       // token1 address
      "price": "...",                 // price denominated in token1/token0
      "base_volume": "...",           // volume denominated in token0
      "quote_volume": "...",          // volume denominated in token1
      "liquidity": "...",             // liquidity denominated in USD
      "liquidity_ZYX": "..."          // liquidity denominated in ZYX
    },
    // ...
  }
}
```
### Fees
Providing liquidity gives you a reward in the form of trading fees when people use your liquidity pool. 
Whenever someone trades on ZyxSwap, the trader pays a 0.30% fee.

Deposit/Withdraw fee : 0%.
