# CLAUDE.md

이 파일은 Claude Code가 이 리포에서 작업할 때 참고하는 안내서다.

## Project Overview

조직도·기구표를 만들어 A3/A4 PDF로 출력하는 오프라인 PWA. 앱 전체(CSS/JS/PDF 라이브러리)가 `index.html` 하나에 인라인되어 있으며 빌드 과정 없음. 배포: https://mogoon.github.io/orgchart/

## Tech Stack

- 단일 HTML (`index.html`) — 인라인 CSS/JS + html2canvas + jsPDF
- 자체 zip/xlsx 파서 (엑셀 import를 위해 외부 라이브러리 없이 구현)
- PWA (`sw.js`) — scope `/orgchart/`
- localStorage 자동 저장 + JSON export/import
- GitHub Pages 배포 (main 브랜치 루트)

## Development Commands

```bash
python3 -m http.server 8000    # 로컬 확인 (SW 때문에 localhost/HTTPS 필요)
```

## Project Structure

- `index.html` — 앱 전체 (`<style>` → html2canvas/jsPDF 인라인 → 앱 스크립트)
- `manifest.json` — PWA 매니페스트 (scope `/orgchart/`)
- `sw.js` — 서비스워커 (navigate는 네트워크 우선)
- `icon-*.png`, `icon.svg` — 아이콘

## Notes for Claude

- 파일 하나 정책 — 별도 파일로 쪼개지 말고 `index.html` 안에서 편집. 배포 결과물이 곧 소스.
- 사진은 자동 축소 후 data URL로 저장(용량 관리).
- scope가 `/orgchart/`라 배포 경로 변경 시 manifest도 함께 수정 필요.
- 새 배포 반영: SW navigate는 네트워크 우선이라 온라인에서 즉시 반영됨.
- 관련 프로젝트: `directory` (같은 조직 도메인이지만 목적이 다름 — 이쪽은 도식, 저쪽은 연락처). 코드 공유하지 말 것.
