# XPChain Core 릴리즈 가이드 (GitHub Actions)

이 저장소(`arnoldcho/xpchain-community-core`)는 태그 기준으로 자동 빌드/릴리즈하도록 설정되어 있습니다.

## 1) 지원 대상
- Linux (Ubuntu x86_64): `xpchaind`, `xpchain-cli`, `xpchain-tx`, `xpchain-qt`
- Windows 64bit: `xpchaind.exe`, `xpchain-cli.exe`, `xpchain-tx.exe`, `xpchain-qt.exe`
- Windows 32bit: `xpchaind.exe`, `xpchain-cli.exe`, `xpchain-tx.exe`, `xpchain-qt.exe`
- macOS: `xpchaind`, `xpchain-cli`, `xpchain-tx`, `xpchain-qt`

주의: iOS는 XPChain Core(데스크톱/노드 소프트웨어) 공식 빌드 타깃이 아닙니다.

## 2) 릴리즈 실행 방법

### 방법 A. 태그 푸시 (권장)
```bash
git tag v0.17.0-4
git push origin v0.17.0-4
```

### 방법 B. 수동 실행
- GitHub 저장소 > Actions > `Build and Release XPChain Core`
- `Run workflow` 클릭
- `tag` 입력 (예: `v0.17.0-4`)

## 3) 결과물 확인
- GitHub Releases에 자동 생성
- 첨부 파일 예시:
  - `xpchain-v0.17.0-4-linux-x86_64.tar.gz`
  - `xpchain-v0.17.0-4-win64.zip`
  - `xpchain-v0.17.0-4-win32.zip`
  - `xpchain-v0.17.0-4-macos.tar.gz`

## 4) 운영 권장사항
- 태그를 찍기 전에 `master` 기준으로 테스트 빌드 1회 권장
- 릴리즈 노트에 변경점(합의/지갑/네트워크)을 꼭 명시
- 파일 해시(`sha256sum`)를 릴리즈 노트에 함께 게시
