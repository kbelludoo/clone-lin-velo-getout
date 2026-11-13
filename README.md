# clone-lin-velo-getout

Experimental **LIN** clone of Velodrome Finance V2 (Solidly-style)
`Pool.getAmountOut` — volatile `x*y` and stable `x³y+y³x` Newton `_get_y`.
Same kernel is used by Aerodrome on Base.

**Proofs live in [kbelludoo/lin-open](https://github.com/kbelludoo/lin-open)** — this repo is the LIN copy only.

- **Upstream (hash-pinned, not vendored):** [velodrome-finance/contracts](https://github.com/velodrome-finance/contracts) `b3065d8b6702b14b094f9f6046b752cc9f78c43b`
  - `contracts/Pool.sol` sha256 `32d040ff419fa9b1f9113f7e10d587b332a2ab9c6b6099851025cc16a4e986bb` blob `91412c378bba4d8076271cee52e1397b1520b709`
  - License GPL-3.0-or-later. This repository does **not** vendor the Solidity source.
- **LIN kernel:** [`src/lin_velo_getout.lin`](src/lin_velo_getout.lin) (sha256 `599cd420395b044db259639ee08c92c2b4480634a8333a821bf73d573a569689`, identical to lin-open)
- **C11 oracle copy:** [`test/oracles/velo_getout_c11.c`](test/oracles/velo_getout_c11.c)
- **Proofs (lin-open only):** `examples/velo_getout/` and `make velo-getout-proof`
- **Class:** EXPERIMENTAL uint64-scale, `SCALE = 1e9`. Not Optimism/Base uint256. Not 1e18 decimals. Not a production pool replacement.

Named goldens (equal `1e9` reserves): volatile +10% fee 0 → **90909090**; fee 5 → **90867766**; fee 30 (Uniswap-0.3% match) → **90661089**; stable +10% fee 0 → **99950051**; fee 1 → **99940071**; `dx=0` fail-closed **0**. Naive i64 `4e9*4e9` wraps to **-2446744073709551616**; 128-bit muldiv fail-closes to **0**.

## Reproduce proofs (in lin-open)

```bash
make velo-getout-proof
# or: python3 test/prove_velo_getout_external.py
```

## Not claimed

Uint256 / ONE=1e18 / token-decimals mainnet parity.
LIN replacing Velodrome, Aerodrome, Uniswap, or the EVM. TVL or dollar savings. zk soundness.
Solidly cubic `k` alone (see clone-lin-solidly-k). This clone is the quote kernel.
