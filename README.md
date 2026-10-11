# plan275-site

plan275 앱의 공개 페이지(지원, 개인정보처리방침). GitHub Pages로 배포한다.

## 구조

```
plan275-site/
├── index.html         # 빈 페이지 (용도는 나중에 정한다)
├── style.css          # 모든 페이지가 함께 쓰는 스타일
├── 404.html
├── .nojekyll          # Jekyll 처리 없이 파일 그대로 배포
└── <앱>/              # 앱마다 디렉터리 하나
    ├── index.html     # 지원 페이지 (한국어)
    ├── privacy/       # 개인정보처리방침 (한국어)
    └── en/            # 영어: index.html, privacy/
```

| 페이지 | 경로 |
|---|---|
| 사라락 지원 | `/sararak/`, `/sararak/en/` |
| 사라락 개인정보처리방침 | `/sararak/privacy/`, `/sararak/en/privacy/` |

## 규칙

- 빌드 도구 없이 HTML을 직접 쓴다. 스타일은 `style.css` 하나만 쓰고, 꾸밈 요소(이미지, 웹 글꼴, 스크립트)를 넣지 않는다.
- **모든 페이지에 `<meta name="robots" content="noindex">`를 둔다** (검색 결과에 나오지 않게).
  `robots.txt`로 크롤링을 막지 않는다. 막으면 검색 엔진이 noindex를 읽지 못해 외부 링크로 주소가 색인될 수 있다.
- 링크와 `style.css`는 상대 경로로 쓴다. `404.html`만 어느 경로에서나 쓰이므로 `/style.css`를 쓴다 (사용자 도메인 루트 기준).
- 한국어와 영어 페이지는 서로 링크한다 (상단 `nav`).
- 새 앱은 `sararak/`을 복사해 내용을 바꾼다. 루트 `index.html`에는 링크를 두지 않는다 (빈 페이지).

## 개인정보처리방침 원문

방침 원문은 앱 저장소의 마크다운이다. 방침을 고칠 때는 원문과 이 사이트의 HTML을 함께 고친다.

| 앱 | 원문 |
|---|---|
| 사라락 | `soundring-project/sararak/docs/legal/privacy-policy.{ko,en}.md` |

- 고치면 "시행일"과 맨 아래 변경 이력을 바꾸고, 시행 7일 전(중요한 변경은 30일 전)에 올린다 (방침의 변경 조항).
- 앱 안의 방침 링크가 이 주소를 가리키므로 경로를 바꾸지 않는다.

## 미리 보기

디렉터리 링크(`privacy/`)는 파일을 직접 열면 동작하지 않는다. 로컬 서버로 연다.

```sh
python3 -m http.server -d . 8000   # http://localhost:8000/
```

## 배포

- GitHub 공개 저장소의 Settings > Pages에서 `main` 브랜치 루트를 배포한다.
- 사용자 도메인을 연결할 때 저장소 루트에 `CNAME` 파일(도메인 한 줄)을 두고, DNS를 설정하고, "Enforce HTTPS"를 켠다.

## 할 일

- [ ] GitHub 공개 저장소를 만들고 push한다 (아직 원격이 없다. 2026-10-11 기준 로컬 커밋만 있다)
- [ ] Pages를 켜고 도메인을 연결한다 (`CNAME`, DNS, Enforce HTTPS). 도메인은 나중에 정한다
- [ ] 공개한 날이 방침 시행일(2026-10-11)보다 늦으면 시행일을 원문과 함께 고친다
- [ ] 루트 `index.html`의 용도를 정한다 (지금은 빈 페이지)
