---
description: 현재 폴더에 CLAUDE.md, DEVELOPMENT.md, WIKI_SPEC.md를 생성하고 {WIKI_ROOT}를 치환한다
---

# /init-claude-project

다음 순서를 **정확히** 따른다. 템플릿은 `${CLAUDE_PLUGIN_ROOT}/templates/` 에 있다
(`${CLAUDE_PLUGIN_ROOT}` 는 Claude Code가 자동으로 제공하는 플러그인 루트 경로다).

## 1. WIKI_ROOT 입력받기
사용자에게 위키 루트 절대경로를 물어본다 (예: `/Users/me/Documents/wiki`).
- 입력이 비어 있으면 다시 물어보고, 값을 받기 전에는 다음 단계로 진행하지 않는다.
- 상대경로가 들어오면 명령이 실행된 현재 작업 디렉토리(플러그인 디렉토리가 아님) 기준 절대경로로 정규화한다.
- 정규화된 절대경로를 `WIKI_ROOT_VALUE` 로 둔다.

## 2. 기존 파일 확인
현재 작업 디렉토리에 `CLAUDE.md`, `DEVELOPMENT.md`, `WIKI_SPEC.md` 가 이미 있는지 각각 검사한다.
존재하는 파일이 있으면 **파일별로** "덮어쓸지 / 건너뛸지" 사용자에게 확인한다.
건너뛰기로 선택한 파일은 3단계에서 제외한다.

## 3. 지침 파일 생성
승인된 파일에 대해, `${CLAUDE_PLUGIN_ROOT}/templates/<파일명>` 을 현재 폴더로 복사한다.
- `CLAUDE.md` 와 `WIKI_SPEC.md` 는 복사 후 파일 내 모든 `{WIKI_ROOT}` 를 `WIKI_ROOT_VALUE` 로 치환한다.
- `DEVELOPMENT.md` 는 `{WIKI_ROOT}` 가 없으므로 치환 없이 그대로 둔다.

## 4. 디렉토리 구조 생성
`WIKI_ROOT_VALUE` 하위에 `raw/`, `wiki/`, `assets/` 를 생성한다 (`mkdir -p`, 이미 있으면 그대로 둔다).
모든 파일을 건너뛰었더라도 이 단계는 수행한다.

## 5. 결과 보고
생성한 파일, 건너뛴 파일, 생성한 디렉토리 목록과 치환에 사용한 WIKI_ROOT 값을 요약 출력한다.
