# plan275-site

plan275 앱의 공개 페이지(지원, 개인정보처리방침). GitHub Pages로 배포한다.

## 구조

```
plan275-site/
├── index.html         # 빈 페이지 (용도는 나중에 정한다)
├── style.css          # 모든 페이지가 함께 쓰는 스타일
├── 404.html
├── .nojekyll          # Jekyll 처리 없이 파일 그대로 배포
├── CNAME              # 사용자 도메인 plan275.com
└── <앱>/              # 앱마다 디렉터리 하나
    ├── index.html     # 언어 선택 (한국어, English 링크만)
    ├── ko/            # 한국어: index.html(지원), privacy/(개인정보처리방침)
    └── en/            # 영어: index.html, privacy/
```

| 페이지 | 경로 |
|---|---|
| 사라락 언어 선택 | `/sararak/` |
| 사라락 지원 | `/sararak/ko/`, `/sararak/en/` |
| 사라락 개인정보처리방침 | `/sararak/ko/privacy/`, `/sararak/en/privacy/` |

- 2026-10-24에 한국어 페이지를 `/sararak/`·`/sararak/privacy/`에서 `ko/` 아래로 옮겼다 (출시 전, 영어와 같은 구조로). 옛 방침 주소는 남기지 않았다.

## 규칙

- 빌드 도구 없이 HTML을 직접 쓴다. 스타일은 `style.css` 하나만 쓰고, 꾸밈 요소(이미지, 웹 글꼴, 스크립트)를 넣지 않는다.
- **모든 페이지에 `<meta name="robots" content="noindex">`를 둔다** (검색 결과에 나오지 않게).
  `robots.txt`로 크롤링을 막지 않는다. 막으면 검색 엔진이 noindex를 읽지 못해 외부 링크로 주소가 색인될 수 있다.
- 링크와 `style.css`는 상대 경로로 쓴다. `404.html`만 어느 경로에서나 쓰이므로 `/style.css`를 쓴다 (사용자 도메인 루트 기준).
- 한국어와 영어 페이지는 서로 링크한다 (상단 `nav`, 2026-10-22에 되살렸다). Play Console에는 방침 URL을 하나만 넣을 수 있어 영어판을 넣고, 거기서 한국어판으로 간다.
- 앱은 방침을 주소 끝에 `#app`을 붙여 앱 안 웹 뷰로 연다. 그때는 다른 페이지로 옮겨 가지 않게 링크를 없앤다: 방침 페이지 `<body>` 맨 앞의 `<span id="app"></span>`와 `style.css`의 `#app:target` 규칙이 `nav`를 숨기고, 본문의 사이트 안 링크(`class="site-link"`)를 누를 수 없게 한다.
  방침 본문에 사이트 안 링크를 더하면 `class="site-link"`를 붙인다. 바깥 링크(다른 사이트, `mailto:`)는 앱이 밖으로 연다.
- 새 앱은 `sararak/`을 복사해 내용을 바꾼다. 언어별 페이지는 `ko/`, `en/` 아래에 두고 앱 디렉터리의 `index.html`은 언어 선택만 한다. 루트 `index.html`에는 링크를 두지 않는다 (빈 페이지).

## 개인정보처리방침 원문

방침 원문은 앱 저장소의 마크다운이다. 방침을 고칠 때는 원문과 이 사이트의 HTML을 함께 고친다.

| 앱 | 원문 |
|---|---|
| 사라락 | `soundring-project/sararak/docs/legal/privacy-policy.{ko,en}.md` |

- 고치면 "시행일"과 맨 아래 변경 이력을 바꾸고, 시행 7일 전(중요한 변경은 30일 전)에 올린다 (방침의 변경 조항).
  - 앱 출시 전에는 이 규정을 적용하지 않는다 (이용자가 없다). 시행일·이력을 그대로 두고 고친다 (2026-10-22 사용자 결정). 사라락이 한 스토어에라도 출시되면 그 뒤부터 지킨다.
- 앱 안의 방침 링크가 이 주소를 가리키므로 경로를 바꾸지 않는다 (출시 뒤). 출시 전에 바꾸면 앱의 링크 상수(iOS `PrivacyPolicyView.swift`, Android `PrivacyPolicy.kt`)도 함께 바꾼다.

## 미리 보기

디렉터리 링크(`privacy/`)는 파일을 직접 열면 동작하지 않는다. 로컬 서버로 연다.

```sh
python3 -m http.server -d . 8000   # http://localhost:8000/
```

## 배포

- GitHub 공개 저장소의 Settings > Pages에서 `main` 브랜치 루트를 배포한다.
- 사용자 도메인을 연결할 때 저장소 루트에 `CNAME` 파일(도메인 한 줄)을 두고, DNS를 설정하고, "Enforce HTTPS"를 켠다.

## 할 일

- [x] GitHub 공개 저장소를 만들고 push한다 (2026-10-20, 조직 `plan275`의 `plan275/plan275-site`). 커밋 작성자는 `plan275 <team.plan275@gmail.com>`이다 (저장소 로컬 `user.email`)
- [x] Pages를 켜고 도메인을 연결한다 (2026-10-20 공개, Let's Encrypt 인증서). 도메인은 `plan275.com` (2026-10-20, 가비아). `CNAME` 파일은 넣었다
- [x] 시행일을 공개한 날(2026-10-20)로 고쳤다 (원문과 함께)
- [ ] 루트 `index.html`의 용도를 정한다 (지금은 빈 페이지)
