# Aztecscan AZTEC payout audits

Public audit artifacts for Aztecscan provider off-chain delegator reward payouts.

## Operator

- Operator: Aztecscan / Aztlan Labs
- Aztec staking provider id: `4`
- Distribution wallet / Safe: `0x90e7b822a5Ac10edC381aBc03d94b866e4B985A1`
- Reward token: AZTEC `0xA27EC0006e59f245217Ff08CD52A7E8b169E62D2`
- Ethereum mainnet StakingRegistry: `0x042dF8f42790d6943F41C25C2132400fd727f452`
- Aztec mainnet rollup: `0xAe2001f7e21d5EcABf6234E9FDd1E76F50F74962`

## Policy

- Commission: `2500` bps = 25%
- Cadence: weekly
- First off-chain payout starts at Aztec epoch `3943`
- Settlement windows are inclusive and non-overlapping. The next run should start at the previous run's `toEpoch + 1`.

## Runs

| Window | Run id | Delegator payout | Operator commission | Artifacts |
|---|---:|---:|---:|---|
| epochs `3943-4104` | `mqozqmiy-ed7589` | `34,912.5 AZTEC` | `11,637.5 AZTEC` | [`audit`](./runs/epoch-3943-4104-mqozqmiy-ed7589.json), [`safe`](./runs/epoch-3943-4104-mqozqmiy-ed7589.safe.json) |

## Verification

The audit JSON records the settlement window, reward parameters, attributed checkpoints, per-delegator transfer amounts, and encoded transaction calldata.

To reproduce a run, use the same payout runner version and the public config in this repo, plus your own archival Ethereum mainnet RPC URL.

For this first run:

```bash
git clone https://github.com/aztec-scan/aztec-staking-payout.git
cd aztec-staking-payout
git checkout b2bc318
cp ../aztec-payout-audit/config.public.yaml ./config.yaml
# edit config.yaml and add your own archival rpcUrl
npm install
npm run settle -- --config ./config.yaml --from-epoch 3943 --to-epoch 4104 --dry-run
```

The generated payout amounts should match the audit file for the same epoch window.
