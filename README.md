# EZmap — Personal Agent Runtime

> **AI-powered navigation for Android. No server. Just your phone.**

EZmap는 서버 없이 Android 앱 안에서 완전히 동작하는 AI 에이전트 내비게이션 앱입니다.
사용자가 본인의 API 키를 직접 입력하면 Gemini가 앱 안에서 Function Calling으로 외부 API를 호출합니다.

**Website:** https://ezmap.pages.dev

---

## 주요 기능

- **AI 음성 에이전트** — "이지야, 강남역 가는 길 알려줘" 한 마디로 목적지 검색부터 경로 안내까지
- **62개 Tool 호출** — 지도, 날씨, 주유소, 충전소, 대중교통, 위키백과, 환율 등
- **서버 없는 설계** — 앱이 곧 에이전트. 사용자 데이터가 외부 서버로 전송되지 않음
- **자기학습 스킬 시스템** — 반복 패턴을 자동으로 스킬로 승격 (Rhino JS 샌드박스)
- **앱 범용 제어** — 접근성 기반 `control_app`으로 다른 앱도 음성으로 조작
- **웨이크워드** — "이지야"로 핸즈프리 호출 (Vosk)

---

## 설치 방법

### 1. APK 다운로드

[Releases 탭](../../releases)에서 최신 APK를 다운로드하세요.

**요구사항:**
- Android 8.0 (API 26) 이상
- 알 수 없는 출처 설치 허용 (설정 → 보안 → 출처를 알 수 없는 앱)

### 2. 필수 API 키 발급

앱 최초 실행 시 온보딩 화면에서 API 키를 입력합니다.

| 키 | 발급처 | 용도 | 필수 여부 |
|----|--------|------|-----------|
| **Gemini API Key** | [Google AI Studio](https://aistudio.google.com/apikey) | AI 에이전트 엔진 | ✅ 필수 |
| **Kakao REST API Key** | [Kakao Developers](https://developers.kakao.com) | 장소 검색, 경로 탐색 | ✅ 필수 |
| **기상청 API Key** | [공공데이터포털](https://www.data.go.kr) | 날씨 정보 | 선택 |
| **Naver Cloud** | [Naver Cloud Platform](https://www.ncloud.com) | 네이버 경로 (듀얼 경로) | 선택 |
| **ODsay Key** | [ODsay Lab](https://lab.odsay.com) | 대중교통 경로 | 선택 |
| **Opinet Key** | [한국석유공사](https://www.opinet.co.kr) | 실시간 주유소 가격 | 선택 |

> **체험 모드**: Gemini 키 없이도 30회/일 시범 사용 가능 (내장 키 활용)

### 3. Kakao 네이티브 앱 키 등록

Kakao Developers에서 Android 플랫폼 등록 시 패키지명을 입력하세요:
```
com.example.ez_capstone
```

---

## 기술 스택

| 항목 | 내용 |
|------|------|
| 언어 | Kotlin 2.0.21 |
| UI | Jetpack Compose + Material 3 (OBSIDIAN 다크 테마) |
| AI | Gemini 2.5 Flash (Function Calling) |
| 지도 | Kakao Map SDK 2.12.18 |
| DB | Room + SQLCipher (AES-256 암호화) |
| 음성 | Vosk (온디바이스 STT) + Android TTS |
| DI | Hilt |
| 빌드 | AGP 8.12.3, Min SDK 26, Target SDK 36 |

---

## 아키텍처

```
사용자 음성 → STT(Vosk) → GeminiAgentEngine
  → Function Calling Loop (최대 6회)
  → ToolExecutor → Kakao/Naver/기상청/오피넷 API
  → AgentResponse → TTS + 동적 카드 UI
```

4대 핵심 축:
1. **Privacy by Design** — 서버 없음, 앱이 에이전트
2. **control_app** — 접근성 기반 범용 앱 제어
3. **AgentLink** — PC Claude Code 원격 연동
4. **Self-Extension** — Rhino JS 샌드박스 자기확장 런타임

---

## 팀

| 이름 | 이메일 | GitHub | 역할 |
|------|--------|--------|------|
| 황동헌 | ng524855@gmail.com | [@eastlaw02](https://github.com/eastlaw02) | 팀장 |
| 최재원 | cjw070690@gmail.com | [@cjw0076](https://github.com/cjw0076) | 개발 |
| 박규리 | rbflefg5805@gmail.com | — | 개발 |
| 진동섭 교수 | — | — | 지도교수 |

IT융합학부 · 2026학년도 1학기 캡스톤디자인

---

## 라이선스

비공개 소스. APK는 학술/시연 목적으로만 배포됩니다.