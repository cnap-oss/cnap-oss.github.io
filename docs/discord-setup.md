# Discord 봇 설정 가이드

CNAP Agent를 Discord에서 사용하기 위한 Discord 봇 설정 방법을 안내합니다.

## Discord Bot Token 발급

### 1. Discord Developer Portal 접속

[Discord Developer Portal](https://discord.com/developers/applications)에 접속합니다.

### 2. 새 애플리케이션 생성

1. **'New Application'** 버튼을 클릭합니다.
2. 애플리케이션 이름을 입력합니다 (예: "CNAP Agent").
3. Discord 개발자 약관에 동의하고 **'Create'**를 클릭합니다.

![New Application](/images/discord-new-app.png)

### 3. Bot 생성

1. 왼쪽 사이드바에서 **'Bot'** 메뉴를 클릭합니다.
2. **'Add Bot'** 버튼을 클릭합니다.
3. 확인 대화상자에서 **'Yes, do it!'**을 클릭합니다.

![Add Bot](/images/discord-add-bot.png)

### 4. Bot Token 복사

1. Bot 설정 페이지에서 **'Reset Token'** 버튼을 클릭합니다.
2. 확인 대화상자에서 **'Yes, do it!'**을 클릭합니다.
3. 표시된 토큰을 **복사**합니다.

::: danger 중요
Bot Token은 비밀번호와 같습니다. 절대로 공개 저장소나 다른 사람과 공유하지 마세요. 토큰이 노출되면 즉시 'Reset Token'을 클릭하여 새로운 토큰을 발급받으세요.
:::

::: warning 주의
토큰은 생성 시 한 번만 표시됩니다. 복사한 토큰을 안전한 곳에 보관하세요. 토큰을 잃어버린 경우 'Reset Token'을 클릭하여 새로 발급받아야 합니다.
:::

### 5. Privileged Gateway Intents 활성화

Bot이 Discord 서버에서 메시지를 읽고 처리하려면 다음 권한을 활성화해야 합니다:

1. Bot 설정 페이지에서 **'Privileged Gateway Intents'** 섹션으로 스크롤합니다.
2. 다음 항목을 활성화합니다:
   - ✅ **MESSAGE CONTENT INTENT** - 메시지 내용을 읽을 수 있습니다.
   - ✅ **SERVER MEMBERS INTENT** - 서버 멤버 정보를 읽을 수 있습니다.
3. **'Save Changes'** 버튼을 클릭합니다.

![Privileged Gateway Intents](/images/discord-intents.png)

::: tip 팁
`MESSAGE CONTENT INTENT`는 봇이 메시지 내용을 읽기 위해 필수적입니다. 이 권한이 없으면 봇이 메시지에 응답할 수 없습니다.
:::

## Bot 초대 URL 생성

### 1. OAuth2 설정

1. 왼쪽 사이드바에서 **'OAuth2'** > **'URL Generator'**를 클릭합니다.
2. **'SCOPES'** 섹션에서 다음을 선택합니다:
   - ✅ **bot** - 봇으로 추가됩니다.
   - ✅ **applications.commands** - 슬래시 커맨드를 사용할 수 있습니다.

### 2. Bot 권한 설정

**'BOT PERMISSIONS'** 섹션에서 다음 권한을 선택합니다:

#### General Permissions

- ✅ **Read Messages/View Channels** - 채널을 보고 메시지를 읽을 수 있습니다.

#### Text Permissions

- ✅ **Send Messages** - 메시지를 보낼 수 있습니다.
- ✅ **Send Messages in Threads** - 스레드에 메시지를 보낼 수 있습니다.
- ✅ **Embed Links** - 링크를 임베드할 수 있습니다.
- ✅ **Attach Files** - 파일을 첨부할 수 있습니다.
- ✅ **Read Message History** - 메시지 기록을 읽을 수 있습니다.
- ✅ **Add Reactions** - 반응을 추가할 수 있습니다.

::: tip 권장 권한
위 권한은 CNAP Agent가 정상적으로 작동하기 위한 최소 권한입니다. 필요에 따라 추가 권한을 부여할 수 있습니다.
:::

### 3. 초대 URL 복사

1. 페이지 하단의 **'GENERATED URL'**에서 생성된 URL을 복사합니다.
2. 이 URL은 봇을 서버에 초대할 때 사용됩니다.

![Generated URL](/images/discord-generated-url.png)

## Discord 서버에 봇 추가

### 1. 초대 URL 사용

1. 위에서 복사한 초대 URL을 브라우저 주소창에 붙여넣습니다.
2. 봇을 추가할 서버를 선택합니다.
3. 권한을 확인하고 **'Authorize'**를 클릭합니다.
4. CAPTCHA 인증을 완료합니다.

::: warning 주의
봇을 서버에 추가하려면 해당 서버의 **'Manage Server'** 권한이 필요합니다.
:::

### 2. 봇 확인

1. Discord 서버의 멤버 목록에서 봇이 추가되었는지 확인합니다.
2. 봇은 오프라인 상태로 표시됩니다. CNAP을 실행하면 온라인 상태로 변경됩니다.

## CNAP 설정 파일에 Token 추가

### 자동 설정 (설치 스크립트 사용)

[퀵스타트 가이드](./quickstart.md)의 설치 스크립트를 사용하면 설치 과정에서 Discord Bot Token을 입력하라는 프롬프트가 표시됩니다.

```bash
Discord Bot Token을 입력하세요: <여기에 복사한 토큰 붙여넣기>
```

### 수동 설정

설정 파일(`$HOME/.cnap/config.yml`)을 직접 편집할 수도 있습니다:

```yaml
# Discord Bot Configuration
discord:
  token: "YOUR_DISCORD_BOT_TOKEN_HERE"
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

# Discord Bot Configuration
discord:
  token: "..."
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

### Token 오류

설정 파일의 토큰이 올바른지 확인하세요. 필요한 경우 [Discord Developer Portal](https://discord.com/developers/applications)에서 'Reset Token'을 클릭하여 새 토큰을 발급받으세요.

### 봇이 메시지에 응답하지 않는 경우

`MESSAGE CONTENT INTENT`가 활성화되어 있는지 확인하세요.

## 다음 단계

[퀵스타트 가이드](./quickstart.md)로 돌아가 설치를 계속하세요.
