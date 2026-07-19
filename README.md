# 기구표 메이커 · 조직도

조직도·기구표를 만들고 A3/A4 PDF로 출력하는 도구입니다. 서버 없이 정적 파일만으로 동작하는 오프라인 PWA이며, 모든 데이터는 브라우저에만 저장됩니다.

**배포:** https://mogoon.github.io/orgchart/

## 기능

- **조직도 편집** — 카드 클릭 후 바로 입력(contenteditable), 하위/형제 추가, 레벨 승격·강등, 드래그로 이동
- **레이아웃** — 행(깊이)별 글자 크기·색, 가로/세로 배치 전환, 같은 행 높이 자동 정렬
- **데이터 입력기** — 표 형태로 빠르게 입력, 엑셀(.xlsx)/CSV 가져오기·양식 내려받기 (외부 라이브러리 없이 자체 zip/xlsx 파서)
- **출력** — A3/A4 · 가로/세로, 인쇄 및 PDF 저장 (html2canvas + jsPDF 인라인)
- **사진** — 카드에 사진 첨부(자동 축소 후 data URL 저장)
- **저장** — localStorage 자동 저장, JSON 내보내기/불러오기
- **PWA** — 홈 화면 설치, 완전 오프라인 동작

## 구조

앱 전체(CSS/JS/PDF 라이브러리)가 `index.html` 하나에 인라인되어 있습니다. 별도 빌드 과정 없이 이 저장소 루트가 곧 배포 결과물입니다.

```
index.html     앱 전체 (라이브러리 인라인 포함)
manifest.json  PWA 매니페스트 (scope: /orgchart/)
sw.js          서비스워커 — index.html 캐시로 완전 오프라인
icon-*.png     아이콘 (icon.svg가 원본)
```

`index.html` 내부 구성: `<style>`(17행~) → html2canvas/jsPDF 인라인(482~879행) → 앱 스크립트(880행~, State/Render/Editing/DnD/Persist/Export 섹션).

## 로컬 실행

서비스워커 때문에 HTTPS 또는 `localhost`가 필요합니다.

```bash
python3 -m http.server 8000
# → http://localhost:8000
```

## 배포

`main` 브랜치 푸시 시 GitHub Pages(main / root)가 자동 반영합니다. 서비스워커가 navigate 요청을 네트워크 우선으로 처리하므로 새 배포는 온라인 상태에서 즉시 반영됩니다.
