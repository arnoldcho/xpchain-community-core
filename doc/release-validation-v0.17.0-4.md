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

## Linux Validation (PASS)

### Environment
- Platform: Ubuntu 24.04 (Vultr, XFCE)
- Binary package: `xpchain-v0.17.0-4-linux-x86_64.tar.gz`
- Runtime files: `xpchaind`, `xpchain-cli`, `xpchain-tx`, `xpchain-qt`

### Checks
1. Node start and chain progress
- Command: `./xpchain-cli getblockchaininfo`
- Result: `PASS`
- Notes: node started normally, chain sync progressed from low height and continued.

2. P2P connectivity
- Command: `./xpchain-cli getnetworkinfo`, `./xpchain-cli getconnectioncount`
- Result: `PASS`
- Notes: active peers observed (`connections` in normal range, e.g. 7~9).

3. Wallet status RPC
- Command: `./xpchain-cli getwalletinfo`
- Result: `PASS`
- Notes: wallet metadata and keypool fields returned normally.

4. Receive transaction flow
- Command: `listtransactions` (Qt debug console)
- Result: `PASS`
- Notes: `category: "receive"` transaction confirmed, confirmations increased over time.

5. Send transaction flow
- Command: `listtransactions` (Qt debug console)
- Result: `PASS`
- Notes: `category: "send"` transaction confirmed with fee and block inclusion.

6. Restart resilience
- Action: `xpchaind` / `xpchain-qt` stop-start cycle
- Result: `PASS`
- Notes: wallet and node resumed normally after restart.

### Conclusion
- Linux runtime and wallet receive/send/restart behavior validated for `v0.17.0-4`.
- Current status: **usable for practical wallet operation** under tested Ubuntu 24.04 environment.

## Windows Validation (PASS)

### Environment
- Platform: Windows 64-bit
- Runtime binary: `xpchain-qt.exe`
- Build: `0.17.0`

### Checks
1. App launch
- Result: `PASS`
- Notes: `xpchain-qt.exe` launched normally on Windows 64-bit environment.

2. Node start and chain progress
- Command: `./xpchain-cli getblockchaininfo`
- Result: `PASS`
- Notes: node started normally, chain sync progressed from low height and continued.

3. P2P connectivity
- Command: `./xpchain-cli getnetworkinfo`, `./xpchain-cli getconnectioncount`
- Result: `PASS`
- Notes: active peers observed (`connections` in normal range, e.g. 7~9).

4. Wallet status RPC
- Command: `./xpchain-cli getwalletinfo`
- Result: `PASS`
- Notes: wallet metadata and keypool fields returned normally.

5. Receive transaction flow
- Command: `listtransactions` (Qt debug console)
- Result: `PASS`
- Notes: `category: "receive"` transaction confirmed, confirmations increased over time.

6. Send transaction flow
- Command: `listtransactions` (Qt debug console)
- Result: `PASS`
- Notes: `category: "send"` transaction confirmed with fee and block inclusion.

7. Restart resilience
- Action: close and relaunch wallet (`xpchain-qt.exe`)
- Result: `PASS`
- Notes: wallet restarted cleanly and returned to normal state after relaunch.

### Conclusion
- Windows 64-bit runtime and wallet receive/send/restart behavior validated for `v0.17.0-4`.
- Current status: **usable for practical wallet operation** under tested Windows 64-bit environment.

## Windows 32-bit Validation (PASS)

### Environment
- Platform: Windows 32-bit
- Runtime binary: `xpchain-qt.exe`
- Build: `0.17.0`

### Checks
1. App launch
- Result: `PASS`
- Notes: `xpchain-qt.exe` launched normally on Windows 32-bit environment.

2. Node start and chain progress
- Command: `./xpchain-cli getblockchaininfo`
- Result: `PASS`
- Notes: node started normally, chain sync progressed from low height and continued.

3. P2P connectivity
- Command: `./xpchain-cli getnetworkinfo`, `./xpchain-cli getconnectioncount`
- Result: `PASS`
- Notes: active peers observed (`connections` in normal range, e.g. 7~9).

4. Wallet status RPC
- Command: `./xpchain-cli getwalletinfo`
- Result: `PASS`
- Notes: wallet metadata and keypool fields returned normally.

5. Receive transaction flow
- Command: `listtransactions` (Qt debug console)
- Result: `PASS`
- Notes: `category: "receive"` transaction confirmed, confirmations increased over time.

6. Send transaction flow
- Command: `listtransactions` (Qt debug console)
- Result: `PASS`
- Notes: `category: "send"` transaction confirmed with fee and block inclusion.

7. Restart resilience
- Action: close and relaunch wallet (`xpchain-qt.exe`)
- Result: `PASS`
- Notes: wallet restarted cleanly and returned to normal state after relaunch.

### Conclusion
- Windows 32-bit runtime and wallet receive/send/restart behavior validated for `v0.17.0-4`.
- Current status: **usable for practical wallet operation** under tested Windows 32-bit environment.
