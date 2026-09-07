# ubuntu-24.04

[![latest](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fraw.githubusercontent.com%2Fnobreak-labs%2Fubuntu-24.04%2Fmain%2Findex.json&query=%24.latest&label=latest&color=blue)](https://github.com/nobreak-labs/ubuntu-24.04/releases/latest)
[![release date](https://img.shields.io/github/release-date/nobreak-labs/ubuntu-24.04)](https://github.com/nobreak-labs/ubuntu-24.04/releases/latest)
[![downloads](https://img.shields.io/github/downloads/nobreak-labs/ubuntu-24.04/total)](https://github.com/nobreak-labs/ubuntu-24.04/releases)
![arch](https://img.shields.io/badge/arch-amd64%20%7C%20arm64-blue)

Ubuntu 24.04 시리즈의 VMware Desktop VM 이미지를 배포하는 저장소입니다. 이미지는 `nobreak-labs/vm-image-builder`(비공개)에서 Packer로 빌드하며, amd64와 arm64를 함께 제공합니다.

## 버전 확인

| 파일 | 내용 |
|------|------|
| `index.json` | 전체 릴리스 목록과 `latest` |
| `manifest.json` | 최신 릴리스 상세 |
| `releases/<릴리스 버전>/manifest.json` | 과거 릴리스 상세 |

```shell
curl -s https://raw.githubusercontent.com/nobreak-labs/ubuntu-24.04/main/index.json
curl -s https://raw.githubusercontent.com/nobreak-labs/ubuntu-24.04/main/manifest.json
```

릴리스 버전은 `<OS 버전>-<YYYYMMDD>.<당일 순번>` 형식입니다. 예: `24.04.4-20260907.1`

## 내려받기

VM 아카이브(`.tar.gz`), 체크섬(`.tar.gz.sha256`), `manifest.json`이 각 [GitHub Release](https://github.com/nobreak-labs/ubuntu-24.04/releases)에 첨부됩니다. `manifest.json`의 `artifacts[].url`이 직접 다운로드 주소입니다.

```shell
curl -s https://raw.githubusercontent.com/nobreak-labs/ubuntu-24.04/main/manifest.json \
  | jq -r '.artifacts[] | select(.architecture == "arm64") | .url'
```

## 검증

내려받은 아카이브와 `.sha256`을 같은 디렉터리에 두고 실행합니다.

```shell
# macOS / Linux
shasum -a 256 -c <아카이브 이름>.tar.gz.sha256
```

```powershell
# Windows (PowerShell)
$f = "<아카이브 이름>.tar.gz"
(Get-FileHash $f -Algorithm SHA256).Hash.ToLower() -eq (Get-Content "$f.sha256").Split()[0]
```
