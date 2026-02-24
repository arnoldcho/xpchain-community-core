# Vultr Node Setup Log

## 2026-02-24 - Initial Instance Provisioning

### Purpose
- XPChain wallet/node installation test on Ubuntu desktop environment

### Provider / Plan
- Provider: Vultr
- Plan: Shared CPU `$10/mo`
- Size: `vc2-1c-2gb`
- vCPU: `1`
- Memory: `2 GB`
- Storage: `55 GB`

### Region / Image
- Region: `Singapore, SG`
- Marketplace App: `Ubuntu Desktop (XFCE)`
- OS: `Ubuntu 24.04`
- Marketplace variable `desktopuser`: `arnold`

### Server Identity
- Hostname: `XPChain-Node-05`
- Label: `XPChain-Node-05`

### Connectivity
- Instance connectivity: `Instance(s) with Public IP`
- Public IPv4: `Enabled`
- Public IPv6: `Not selected`

### Additional Features
- VPC Network: `Disabled`
- Automatic Backups: `Disabled`
- DDoS Protection: `Disabled`
- Limited User Login: `Not enabled in this screen`
- Cloud-Init User Data: `Disabled`

### Pending
- [ ] Deploy instance
- [ ] SSH access verification
- [ ] XPChain binaries install
- [ ] xpchaind first run and sync check
- [ ] Firewall / systemd setup
- [ ] Installation guide update for website

## Linux Install Procedure (v0.17.0-4)

### Release source
- Tag: `v0.17.0-4`
- Download URL:
  - `https://github.com/arnoldcho/xpchain-community-core/releases/download/v0.17.0-4/xpchain-v0.17.0-4-linux-x86_64.tar.gz`

### Installation commands
```bash
mkdir -p ~/xpchain && cd ~/xpchain
wget -O xpchain-v0.17.0-4-linux-x86_64.tar.gz \
https://github.com/arnoldcho/xpchain-community-core/releases/download/v0.17.0-4/xpchain-v0.17.0-4-linux-x86_64.tar.gz
tar -xzf xpchain-v0.17.0-4-linux-x86_64.tar.gz
chmod +x xpchaind xpchain-cli xpchain-tx xpchain-qt
```

### Archive structure note
- `xpchain-v0.17.0-4-linux-x86_64.tar.gz` extracts binaries directly into current directory.
- No subdirectory is created after extraction.

### Initial node config
```bash
mkdir -p ~/.xpchain
cat > ~/.xpchain/xpchain.conf << 'EOF'
server=1
listen=1
port=8798
bind=0.0.0.0
discover=1
dnsseed=1
maxconnections=64
fallbackfee=0.11
EOF
```

### Fee fallback option
- If fee estimation is unstable right after startup/sync, set a fallback fee.
- Recommended: put it in `xpchain.conf` so both daemon and wallet use it consistently.
- Temporary CLI/GUI launch examples:
```bash
./xpchaind -fallbackfee=0.11
./xpchain-qt -fallbackfee=0.11
```

### Start and verify
```bash
./xpchaind -daemon
./xpchain-cli getblockchaininfo
./xpchain-cli getnetworkinfo
./xpchain-cli getconnectioncount
```

### Qt launch (desktop environment)
```bash
./xpchain-qt
```

### Firewall
```bash
sudo ufw allow 8798/tcp
sudo ufw status
```

### Notes
- This section is a baseline procedure and will be updated if runtime/install issues are found.

## Troubleshooting

### `./xpchaind: error while loading shared libraries: libboost_filesystem.so.1.74.0`

Cause:
- Current Linux release artifact was built on Ubuntu 22.04 toolchain and linked against Boost `1.74`.
- Ubuntu 24.04 default Boost runtime is newer, so `libboost_filesystem.so.1.74.0` may not exist.

Current guidance:
1. Preferred for immediate test:
   - Use Ubuntu `22.04` server image for runtime compatibility with current artifact.
2. Preferred long-term release fix:
   - Rebuild Linux artifact targeting Ubuntu `24.04` (or package with portable/static strategy).
3. Quick diagnostics command:
```bash
ldd ./xpchaind | grep -E 'not found|boost'
```

## Validation Result (2026-02-24)

### Runtime status
- `xpchaind` startup: `OK`
- `xpchain-cli getblockchaininfo`: `OK`
- `xpchain-cli getnetworkinfo`: `OK`
- `xpchain-cli getconnectioncount`: `7` (at capture time)

### Sync snapshot
- `chain`: `main`
- `blocks`: `3368` (sync in progress)
- `headers`: `424000`
- `initialblockdownload`: `true`

### Notes
- Linux standalone (4-file) runtime test passed on current test server.
- Node is syncing and network connections are established.

## Basic CLI Commands

```bash
# 노드 기본 상태
./xpchain-cli getblockchaininfo
./xpchain-cli getnetworkinfo
./xpchain-cli getconnectioncount

# 지갑 상태
./xpchain-cli getwalletinfo
./xpchain-cli getbalances

# 블록/트랜잭션 조회
./xpchain-cli getbestblockhash
./xpchain-cli getblockcount
./xpchain-cli getblockhash <height>
./xpchain-cli getblock <blockhash>
./xpchain-cli getrawtransaction <txid> 1

# 주소/입출금
./xpchain-cli getnewaddress
./xpchain-cli getreceivedbyaddress <address>
./xpchain-cli sendtoaddress <address> <amount>
```

## Incident Response Commands

```bash
# 프로세스 확인
ps -ef | grep xpchaind | grep -v grep
pgrep -a xpchaind

# 서비스 사용 시 상태/로그
sudo systemctl status xpchaind --no-pager
journalctl -u xpchaind -n 100 --no-pager
journalctl -u xpchaind -f

# 데몬 직접 실행 시 로그
tail -n 100 ~/.xpchain/debug.log
tail -f ~/.xpchain/debug.log

# 피어/네트워크 진단
./xpchain-cli getpeerinfo | grep -E '"addr"|"inbound"'
./xpchain-cli getconnectioncount
ss -lntp | grep 8798
sudo ufw status verbose

# 블록 동기화 진단
./xpchain-cli getblockchaininfo
./xpchain-cli getchaintips

# 정지/시작
./xpchain-cli stop
./xpchaind -daemon
```
