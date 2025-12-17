# OpenCode Zen API Key 발급 가이드

CNAP Agent에서 AI 기능을 사용하기 위한 OpenCode Zen API Key 발급 방법을 안내합니다.

## API Key 발급

### 1. OpenCode Zen 웹사이트 접속

[OpenCode Zen](https://opencode.ai/auth)에 접속합니다.

### 2. 계정 생성 또는 로그인

#### 신규 사용자

1. **'Sign Up'** 또는 **'회원가입'** 버튼을 클릭합니다.
2. 필요한 정보를 입력합니다:
   - 이메일 주소
   - 비밀번호
   - 이름 (선택사항)
3. 이메일 인증을 완료합니다.
4. 계정 생성이 완료됩니다.

#### 기존 사용자

1. **'Sign In'** 또는 **'로그인'** 버튼을 클릭합니다.
2. 이메일과 비밀번호를 입력합니다.
3. 로그인을 완료합니다.

### 3. 대시보드 접속

로그인 후 자동으로 대시보드로 이동하거나, 상단 메뉴에서 **'Dashboard'**를 클릭합니다.

### 4. API Keys 메뉴로 이동

1. 왼쪽 사이드바 또는 상단 메뉴에서 **'API Keys'** 메뉴를 찾아 클릭합니다.
2. API Keys 관리 페이지가 표시됩니다.

### 5. 새 API Key 생성

1. **'Create New API Key'** 또는 **'+ New API Key'** 버튼을 클릭합니다.
2. API Key 설정 대화상자가 나타납니다.

### 6. API Key 설정

API Key 생성 시 다음 정보를 입력합니다:

- **Name**: API Key의 이름 (예: "CNAP Agent", "Production Key")
  - 용도를 쉽게 식별할 수 있는 이름을 사용하세요.
- **Description** (선택사항): API Key에 대한 설명
- **Permissions** (선택사항): API Key의 권한 설정
  - 기본 설정을 사용하는 것을 권장합니다.

::: tip 팁
여러 프로젝트나 환경(개발, 프로덕션)에서 사용하는 경우, 각각 별도의 API Key를 생성하여 관리하는 것이 좋습니다.
:::

### 7. API Key 복사

1. **'Create'** 또는 **'Generate'** 버튼을 클릭합니다.
2. 생성된 API Key가 표시됩니다.
3. **'Copy'** 버튼을 클릭하여 API Key를 복사합니다.

::: danger 중요
API Key는 생성 시 한 번만 표시됩니다. 반드시 안전한 곳에 보관하세요. API Key를 잃어버린 경우, 새로운 API Key를 생성하고 기존 Key를 폐기(Revoke)해야 합니다.
:::

::: warning 보안 주의사항

- API Key는 비밀번호와 같이 민감한 정보입니다.
- 절대로 공개 저장소에 API Key를 커밋하지 마세요.
- API Key가 노출된 경우 즉시 폐기하고 새로 발급받으세요.
- 환경 변수나 안전한 설정 파일에 저장하세요.
  :::

## CNAP 설정 파일에 API Key 추가

### 자동 설정 (설치 스크립트 사용)

[퀵스타트 가이드](./quickstart.md)의 설치 스크립트를 사용하면 설치 과정에서 OpenCode Zen API Key를 입력하라는 프롬프트가 표시됩니다.

```bash
OpenCode Zen API Key를 입력하세요: <여기에 복사한 API Key 붙여넣기>
```

### 수동 설정

설정 파일(`$HOME/.cnap/config.yml`)을 직접 편집할 수도 있습니다:

```yaml
# API Keys Configuration
api_keys:
  opencode: "YOUR_OPENCODE_API_KEY_HERE"
  anthropic: "" # 선택사항
  openai: "" # 선택사항
```

::: code-group

```bash [편집]
# 설정 파일 열기
nano $HOME/.cnap/config.yml

# 또는
vim $HOME/.cnap/config.yml
```

```yaml [예시]
# CNAP Configuration File

# API Keys Configuration
api_keys:
  opencode: "sk-opencode-1234567890abcdefghijklmnopqrstuvwxyz"
  anthropic: ""
  openai: ""
# 나머지 설정...
```

:::

::: danger 보안
설정 파일에는 민감한 정보가 포함되어 있습니다. 파일 권한이 적절하게 설정되어 있는지 확인하세요:

```bash
chmod 600 $HOME/.cnap/config.yml
```

:::

## 문제 해결

### API Key 인증 오류

API Key가 올바르게 복사되었는지, 설정 파일에 공백이나 특수문자가 없는지 확인하세요. 필요한 경우 새 API Key를 생성하세요.

## 다음 단계

[퀵스타트 가이드](./quickstart.md)로 돌아가 설치를 계속하세요.
