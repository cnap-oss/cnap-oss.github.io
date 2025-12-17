# 퀵스타트 가이드

CNAP Agent를 빠르게 시작하는 방법을 안내합니다.

## 시스템 요구사항

- **운영체제**: macOS 또는 Linux
- **아키텍처**: amd64 (x86_64) 또는 arm64 (aarch64)
- **필수 소프트웨어**: Docker
- **네트워크**: 인터넷 연결 (GitHub 릴리스 다운로드 및 API 사용을 위해)
- **Discord Bot Token**: [Discord 봇 설정 가이드](./discord-setup.md) 참조
- **OpenCode Zen API Key**: [OpenCode Zen API Key 발급 가이드](./opencode-api-key.md) 참조

## 설치

### 자동 설치 (권장)

다음 명령어를 실행하여 CNAP을 자동으로 설치할 수 있습니다:

```bash
curl -fsSL https://cnap-oss.github.io/install.sh | bash
```

### 설치 과정

설치 스크립트를 실행하면 다음과 같은 정보를 입력하라는 메시지가 표시됩니다:

#### 1. Discord Bot Token

Discord 봇을 설정하고 토큰을 발급받아야 합니다. 자세한 방법은 [Discord 봇 설정 가이드](./discord-setup.md)를 참조하세요.

#### 2. OpenCode Zen API Key

OpenCode Zen API Key를 발급받아야 합니다. 자세한 방법은 [OpenCode Zen API Key 발급 가이드](./opencode-api-key.md)를 참조하세요.

#### 3. Shell 프로파일 업데이트

설치 스크립트가 자동으로 Shell 프로파일 업데이트를 제안합니다. `y`를 입력하여 자동으로 PATH를 설정하거나, `N`을 입력하여 수동으로 설정할 수 있습니다.

**수동 설정 방법:**

::: code-group

```bash [Bash]
echo 'export PATH="$HOME/.cnap/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

```bash [Zsh]
echo 'export PATH="$HOME/.cnap/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

```fish [Fish]
set -Ux fish_user_paths $HOME/.cnap/bin $fish_user_paths
```

:::

## Docker 설치

CNAP은 작업 실행을 위해 Docker가 필요합니다. Docker가 설치되어 있지 않은 경우, 설치 스크립트가 자동 설치를 제안합니다.

### macOS

::: code-group

```bash [Homebrew]
brew install --cask docker
```

```bash [수동 설치]
# Docker Desktop 다운로드
# https://www.docker.com/products/docker-desktop
```

:::

Docker Desktop 앱을 실행하여 Docker 서비스를 시작하세요.

### Linux

```bash
# Docker 공식 설치 스크립트
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh

# 현재 사용자를 docker 그룹에 추가
sudo usermod -aG docker $USER
newgrp docker
```

::: warning 주의
변경 사항을 적용하려면 로그아웃 후 다시 로그인하거나 `newgrp docker` 명령어를 실행해야 합니다.
:::

## 설치 확인

설치가 완료되면 다음 명령어로 설치를 확인할 수 있습니다:

```bash
# 버전 확인
cnap --version

# 도움말 확인
cnap --help
```

## 설치 위치

CNAP은 다음 위치에 설치됩니다:

- **바이너리**: `$HOME/.cnap/bin/cnap`
- **설정 파일**: `$HOME/.cnap/config.yml`
- **데이터베이스**: `$HOME/.cnap/` (SQLite)

## 기본 사용법

### 에이전트 생성

```bash
cnap agent create
```

대화형 프롬프트가 나타나며 에이전트 정보를 입력할 수 있습니다.

### 작업 생성

```bash
cnap task create
```

에이전트를 선택하고 작업을 생성합니다.

### 작업 실행

```bash
cnap task send
```

생성된 작업을 선택하고 실행합니다.

### 기타 명령어

```bash
# 에이전트 목록 조회
cnap agent list

# 작업 목록 조회
cnap task list

# 작업 상세 조회
cnap task get <task-id>
```

## 문제 해결

### 명령어를 찾을 수 없는 경우

```bash
# 새 터미널을 열거나 Shell 프로파일 다시 로드
source ~/.bashrc  # Bash
source ~/.zshrc   # Zsh
```

### Docker 실행 문제

```bash
# macOS: Docker Desktop 실행
open -a Docker

# Linux: Docker 서비스 시작
sudo systemctl start docker
```
