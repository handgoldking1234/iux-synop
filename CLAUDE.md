# 시놉 (iux-synop) — 작업 안내서

## 한 줄 요약
영화·드라마·숏폼 드라마·웹툰·웹소설 시놉시스를 쓰는 단일 HTML 웹툴. **이 저장소가 정본**이다 (`synop` 저장소는 같은 파일의 예전 사본).

- 주소: https://synop.iux.kr

## 확정된 결정
| 항목 | 결정 |
|---|---|
| 구조 | `index.html` 한 파일 |
| 양식 | 작품 유형 선택 → 로그라인·기획의도·세계관·등장인물·줄거리(3막/기승전결)·셀링포인트 |
| 인물 관계도 | 얼굴 사진 업로드, 드래그 배치·연결, 클릭 시 관련 인물만 강조 |
| 내보내기 | 마크다운, 일반 텍스트, AI 프롬프트 |
| AI | 전체/항목별 생성, 캐릭터 시트 모드(레퍼런스 사진 분석 → 이미지 프롬프트, 그림은 외부 이미지 AI) |
| 디자인 | 스포티파이 (다크 + 그린) |
| 통합 | 웹툰보드(iux-webtoon)의 기획 팝업으로 통합 예정 — 고치면 웹툰보드 쪽도 확인 |

## 코드 지도 (index.html)
- 데이터: `blank`, `save`, `load`, `sample`, `assemble`
- 화면: `renderTypeChips`, `renderGenreChips`, `renderChars`, `charCard`, `renderPlot`, `renderDoc`, `progress`
- 사진: `readPhoto`, `openCropper`
- 관계도: `layoutCircle`, `layoutGrid`, `layoutRadial`, `layoutRoles`, `layoutGroups`, `edgeType`
- 내보내기·AI: `toMarkdown`, `toPlain`, `toAIPrompt`, `aiGenerate`, `aiSection`, `applyAI`
- 테마: `initTheme` (localStorage `synop.theme`)

---

## 공통 작업 원칙 (IUX 프로젝트 전체)
- **언어:** 화면 문구·문서·커밋 메시지는 한국어. 쉬운 말, 기술 용어 최소화.
- **퍼블리싱 시안:** 순수 HTML/CSS + 간단한 스크립트만 넣는다. 서버·DB 연동 코드는 개발 단계에서 따로 붙인다.
- **아이콘:** Lucide. 디자인 시스템을 따로 정하지 않았으면 스포티파이 스타일(다크/화이트 + 포인트 컬러)을 기본으로 쓴다.
- **배포:** GitHub `main` → Vercel 자동 배포. 도메인은 가비아 `iux.kr`의 서브도메인(`*.iux.kr` CNAME → Vercel)을 쓴다.
- **DB:** Supabase 무료 플랜은 활성 프로젝트 2개까지라, 새 프로젝트를 만들지 말고 기존 `iux-cloud`(studio) 프로젝트에 테이블을 얹는 것을 먼저 검토한다.
- **비밀값:** 공개 저장소다. 서비스 키·AI 키·비밀번호는 절대 커밋하지 않는다. 키는 Vercel 환경 변수나 Supabase secrets에 둔다. Supabase anon(public) 키만 코드에 넣을 수 있다.
- **확인:** 고친 뒤에는 브라우저 콘솔 오류 0개, 모바일(390px)과 PC 화면을 눈으로 확인하고 나서 완료라고 한다.
- **브랜치:** `main`은 배포 중인 상태. 큰 작업이나 검증 전 작업은 브랜치(`wip/…`, `claude/…`)에 올리고, `main`을 강제 푸시(-f)로 덮어쓰지 않는다.
- **전체 프로젝트 목록:** https://github.com/handgoldking1234/iux-app/blob/main/docs/PROJECTS.md
