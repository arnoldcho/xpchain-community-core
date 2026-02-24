# XPChain Core v0.17.0-4 Release Validation

## Scope
- Release tag: `v0.17.0-4`
- Repository: `arnoldcho/xpchain-community-core`
- Validation type: runtime smoke + wallet functional test

## macOS Validation (PASS)

### Environment
- Platform: macOS (Apple Silicon)
- App: `XPChain-Qt.app`
- Build: `0.17.0`

### Checks
1. App launch
- Result: `PASS`
- Notes: App launches and console/debug window is accessible.

2. Sync state
- Result: `PASS`
- Notes: Node sync completed and wallet entered normal operating state.

3. Wallet info RPC
- Command: `getwalletinfo`
- Result: `PASS`
- Notes: wallet fields returned normally (`walletversion`, `balance`, keypool, hdseed).

4. Receive transaction flow
- Command: `listtransactions`
- Result: `PASS`
- Notes: `category: "receive"` entry confirmed with confirmations increasing.

5. Send transaction flow
- Command: `listtransactions`
- Result: `PASS`
- Notes: `category: "send"` entry confirmed with fee applied and confirmation progress.

### Conclusion
- macOS runtime and wallet send/receive behavior validated for `v0.17.0-4`.
- Current status: **usable for practical wallet operation** under tested environment.

## Follow-up
- Keep using `rc` tags for pre-release validation and only finalize stable version tags after runtime checks on all target OS.
