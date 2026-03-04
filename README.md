# SciFi — Source Verification

Verified source code for the SciFi voting contract deployed to Ethereum mainnet on August 8, 2015 - just 9 days after the Frontier launch.

| | |
|---|---|
| **Contract** | [`0xd94badbec21695b7a36abcb979efad0108319d18`](https://etherscan.io/address/0xd94badbec21695b7a36abcb979efad0108319d18) |
| **Block** | [51,291](https://etherscan.io/block/51291) |
| **Creation TX** | [`0xd064cb23...`](https://etherscan.io/tx/0xd064cb23bc28e3a233d40deadfc7580d71cd7eef707cd1dbf7eedf03b020b85d) |
| **Compiler** | Solidity v0.1.4, optimizer enabled |
| **Original post** | [r/ethereum (Aug 8, 2015)](https://www.reddit.com/r/ethereum/comments/3g7lx6/are_you_tired_of_best_scifi_movies_of_all_time/) |

## Verify

```bash
./verify.sh
```

Requires `node` and `curl`. Downloads the solc binary automatically on first run.

```
✅ EXACT MATCH
   Runtime bytecode: 219 bytes
   Compiler: solc v0.1.4+commit.5f6c3cdf (optimizer enabled)
   Contract: 0xd94badbec21695b7a36abcb979efad0108319d18
```

## Source

[`SciFi.sol`](SciFi.sol) compiles to a byte-perfect match of the on-chain runtime bytecode (219 bytes).

The source was posted by the author on r/ethereum at Frontier launch, with one difference from the deployed version: the Reddit post shows `bytes32[1000000]` (1 million) while the deployed contract uses `bytes32[1000000000]` (1 billion). The post was edited after deployment, likely simplifying the number for readability.

## How It Works

One of the earliest interactive dApps on Ethereum. Users bid ETH to rank their favorite sci-fi movies:

- **`vote(bytes32 name)`** - send ETH to bid on a movie. New movies are added automatically; repeat bids accumulate.
- **`bids(bytes32)`** - check the total bid for a movie
- **`movies(uint256)`** / **`movie_num()`** - list all movies that have received bids

All ETH is permanently burned - the contract has no withdrawal function, ensuring the creator can't vote for free.

The author's original ranking: eXistenZ at #1 (0.0045 ETH), Blade Runner at #2, Melancholia at #3.

## Notes

- **Runtime bytecode**: exact match with solc v0.1.4 (optimizer enabled)
- **Creation bytecode**: 1-byte difference - native C++ solc adds a STOP (0x00) padding byte after the constructor RETURN, shifting the CODECOPY offset from 0x10 to 0x11. Runtime code is identical.
- Etherscan's verification form only supports solc v0.4.11+. This contract predates that by over a year.
