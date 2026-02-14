---
title: "Android Studio Panda : JetBrains AI Assistant Codex 로그인 오류 해결법"
date: 2026-02-13 17:20:00 +0900
categories:
  - Android
tags:
  - Android-Studio
  - JetBrains-AI-Assistant
  - Codex
comments: true
---

## Overview

현재 Android Studio **Panda 1 \| 2025.3.1** 환경에서 JetBrains AI Assistant를 설치한 뒤, OpenAI 로그인(`Sign in to Codex with ChatGPT`)을 시도하면 진행되지 않고 IDE 오류가 발생하는 버그가 있습니다.

실제 발생한 오류는 `OpenAI 인증 URL 리소스`가 누락되어 발생하는 문제로 보여집니다.

```text
java.util.MissingResourceException: Registry key llm.chat.agent.codex.openai.apache.license.tos.url is not defined
    at com.intellij.openapi.util.registry.Registry.getBundleValue$intellij_platform_util(Registry.kt:372)
    at com.intellij.openapi.util.registry.RegistryValue.resolveRequiredValue(RegistryValue.kt:209)
    at com.intellij.openapi.util.registry.RegistryValue.asString(RegistryValue.kt:46)
    at com.intellij.openapi.util.registry.Registry$Companion.stringValue(Registry.kt:145)
    at com.intellij.ml.llm.core.ui.activation.CodexAuthSwingDslUi.lambda$2$5(CodexAuthSwingDslUi.kt:100)
    at com.intellij.ml.llm.core.ui.activation.CodexAuthSwingDslUi.<init>(CodexAuthSwingDslUi.kt:71)
```

결론부터 말하면, Marketplace에서 **`MCP Server`** 플러그인을 설치하면 바로 해결됩니다.

---

## 문제 상황

1. JetBrains AI Assistant 설치 후 AI Chat 화면 진입
2. `Sign in to Codex with ChatGPT` 버튼으로 OpenAI 로그인 시도
3. 버튼 클릭이 동작하지 않거나 인증 관련 IDE 오류 발생

### 초기 화면 및 로그인 화면

<div style="display: flex; gap: 12px; flex-wrap: wrap; align-items: flex-start;">
  <figure style="flex: 1 1 320px; margin: 0;">
    <div style="aspect-ratio: 454 / 563; overflow: hidden;">
      <img src="/assets/img/posts/2026-02-13-android-studio-panda-codex/01-ai-assistant-initial.png" alt="JetBrains AI Assistant 초기 화면" style="width: 100%; height: 100%; object-fit: cover; object-position: top; display: block;">
    </div>
  </figure>
  <figure style="flex: 1 1 320px; margin: 0;">
    <img src="/assets/img/posts/2026-02-13-android-studio-panda-codex/02-sign-in-to-codex.png" alt="Sign in to Codex with ChatGPT 버튼" style="width: 100%; display: block;">
  </figure>
</div>

---

## 해결 방법

`Settings > Plugins > Marketplace`에서 **MCP Server** 플러그인을 설치한 뒤 IDE를 재시작하면 됩니다.
### MCP Server 플러그인

![Marketplace MCP Server 플러그인](/assets/img/posts/2026-02-13-android-studio-panda-codex/03-marketplace-mcp-server.png)
### 로그인 후 화면

<div>
  <img src="/assets/img/posts/2026-02-13-android-studio-panda-codex/04-codex-login-success.png" alt="로그인 후 화면" loading="lazy">
</div>


여담이지만,, Codex CLI, App, Plugin 형태로 모두 사용해봤지만 앱이 가장 편했던 것 같습니다!

---
