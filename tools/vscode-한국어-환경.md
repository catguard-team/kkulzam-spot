# VS Code 한국어 환경 첫 셋업

> macOS/Windows에 VS Code 깐 직후, 한글이 안 어울리거나 글자가 짤리는 시기를 빠르게 넘기는 법.

## 상황

- 갓 깐 VS Code의 기본 한글 폰트가 보기 어색하거나, 일부 문자가 □(두부)로 보임
- 한국어 메뉴를 원함
- 자동저장·줄바꿈·탭 너비가 본인 취향과 안 맞음

## 그루밍

### 1) 한국어 메뉴

`Cmd+Shift+P` (mac) 또는 `Ctrl+Shift+P` (Win/Linux) → `Configure Display Language` 입력 → **한국어** 선택. 없으면 **Install additional languages...** → "Korean Language Pack for Visual Studio Code" 설치 → 재시작.

### 2) 한글이 잘 보이는 폰트

`Settings` (`Cmd/Ctrl+,`) → `Editor: Font Family` 검색 → 다음 중 하나 입력:

```
'D2Coding ligature', 'D2Coding', 'Menlo', 'Consolas', monospace
```

D2Coding은 [네이버 D2Coding 깃헙](https://github.com/naver/d2codingfont)에서 무료. 라이선스 OFL.

> 'D2Coding ligature'는 `=>`, `!=` 같은 기호를 합쳐서 그려주는 ligature 버전. 싫으면 그냥 'D2Coding'.

### 3) 자주 쓰는 기본값

`Settings` 검색창에 다음을 차례로 넣고 체크/입력:

| 검색어 | 권장값 |
|--------|--------|
| `Files: Auto Save` | `afterDelay` |
| `Editor: Tab Size` | `2` (또는 4) |
| `Editor: Insert Spaces` | ✅ 체크 |
| `Editor: Word Wrap` | `on` |
| `Editor: Render Whitespace` | `boundary` |
| `Files: Trim Trailing Whitespace` | ✅ |
| `Files: Insert Final Newline` | ✅ |

### 4) 처음 깔면 좋은 확장

- **Korean Language Pack** (위 1번에서 자동 설치됨)
- **Hangul (Korean) Word Wrap** — 한글 띄어쓰기 기준 줄바꿈
- **Path Intellisense** — 파일 경로 자동완성
- **GitLens** — Git 히스토리 보기 좋게

> Copilot/Claude 같은 AI 확장은 [`ai/`](../ai/) 폴더 글 참조.

## 출처/참고

- [네이버 D2Coding](https://github.com/naver/d2codingfont)
- VS Code 공식: [Display Language](https://code.visualstudio.com/docs/getstarted/locales)
- 본인 노트북 새로 살 때마다 매번 까는 절차

---
**발견자**: @GoGoComputer · 2026-04-27
