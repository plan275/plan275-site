# plan275-site

plan275 앱의 공개 페이지(홍보·지원, 개인정보처리방침). GitHub Pages로 배포한다.

## 구조

```
plan275-site/
├── index.html         # 빈 페이지 (용도는 나중에 정한다)
├── style.css          # 모든 페이지가 함께 쓰는 스타일
├── 404.html
├── robots.txt         # 크롤링 허용 + 사이트맵 위치
├── sitemap.xml        # 검색에 노출하는 페이지 목록 (hreflang 포함)
├── .nojekyll          # Jekyll 처리 없이 파일 그대로 배포
├── CNAME              # 사용자 도메인 plan275.com
└── <앱>/              # 앱마다 디렉터리 하나
    ├── index.html     # en/으로 리다이렉트 (사라락)
    ├── sararak.css    # 홍보 페이지 전용 스타일 (사라락)
    ├── img/           # 아이콘, 공유 이미지(og), 화면 캡처 (언어별 ko/, en/)
    ├── ko/            # 한국어: index.html(홍보·지원), privacy/(개인정보처리방침)
    └── en/            # 영어: index.html, privacy/
```

| 페이지 | 경로 |
|---|---|
| 사라락 (리다이렉트) | `/sararak/` → `/sararak/en/` |
| 사라락 홍보·지원 | `/sararak/ko/`, `/sararak/en/` |
| 사라락 개인정보처리방침 | `/sararak/ko/privacy/`, `/sararak/en/privacy/` |

- 2026-10-31에 지원 페이지를 홍보 페이지로 키웠다 (방침 링크는 그 안. 문의 메일은 2026-10-31 사용자 결정으로 홍보 페이지에서 뺐다: 검색에 노출되는 페이지에 메일 주소를 두지 않는다. 메일은 noindex인 방침 페이지에만 있다). 홍보 페이지의 문의 절과 바닥글은 방침의 연락처 절(`privacy/#contact`)로 링크한다. 방침의 `id="contact"`를 지우지 않는다. App Store 지원 URL(ko·en)과 Play 웹사이트(`/sararak/`)가 그대로 홍보 페이지로 온다. `/sararak/`은 언어 선택에서 `en/` 리다이렉트로 바꿨다 (사용자 결정).
- 2026-10-24에 한국어 페이지를 `/sararak/`·`/sararak/privacy/`에서 `ko/` 아래로 옮겼다 (출시 전, 영어와 같은 구조로). 옛 방침 주소는 남기지 않았다.

## 규칙

- 빌드 도구 없이 HTML을 직접 쓴다. 웹 글꼴은 넣지 않는다. JS는 쓰되 최소로, HTML·CSS만으로 할 때보다 효과가 나을 때만 쓴다 (2026-11-01 사용자 결정. 그 전에는 JS를 넣지 않았다). 구조화 데이터(`<script type="application/ld+json">`)는 실행되지 않는 데이터다.
  - 방침·404·루트 페이지는 공통 `style.css`만 쓰고 꾸밈 요소를 넣지 않는다.
  - 앱 홍보 페이지(`<앱>/ko/`, `<앱>/en/`)는 앱 디렉터리의 전용 CSS(`sararak.css`)를 쓰고 이미지(아이콘, 화면 캡처)를 넣는다 (2026-10-31 사용자 결정).
- **검색 노출** (2026-10-31 사용자 결정, 그 전에는 모든 페이지가 noindex였다):
  - 색인을 허용하는 페이지는 앱 홍보 페이지와 리다이렉트 페이지(`/sararak/`)뿐이다. `sitemap.xml`에 홍보 페이지를 적는다.
  - **방침·404·루트 `index.html`은 `<meta name="robots" content="noindex">`를 둔다.** 한국어 방침에는 보호책임자 실명이 있어 검색 결과에 나오지 않게 한다.
  - `robots.txt`로 크롤링을 막지 않는다. 막으면 검색 엔진이 noindex를 읽지 못해 외부 링크로 주소가 색인될 수 있다.
- **홍보 페이지의 SEO 요소**: `title`, `meta description`, 절대 주소 `canonical`, `hreflang`(ko, en, x-default=en), Open Graph·Twitter 카드(언어별 `img/<언어>/og.png`), `MobileApplication` 구조화 데이터, 이미지의 `alt`·`width`·`height`.
  첫 화면 이미지 말고는 `loading="lazy"`. 두 언어판의 내용을 같게 유지하고, 고치면 `sitemap.xml`의 `lastmod`도 바꾼다.
- **홍보 문구 원칙** (2026-10-31 사용자 결정): 쓰는 상황(공부, 잠들기 전 등)과 소개 문구는 쓰되 효과(수면 개선, 스트레스 완화 등)를 주장하지 않는다. 기능 설명은 앱 저장소의 스토어 문구(`docs/agent_docs/GUIDE-20261024-0001-store-listing.md`)와 같은 사실만 쓴다. 앱이 바뀌면 그 문서의 "앱이 바뀌면 함께 고칠 곳"을 따라 이 페이지도 고친다.
- **이미지**: 화면 캡처는 Play 스토어용 원본(1080×1920, 1920×1080)을 `cwebp -q 80 -resize 540 960`(가로는 `960 540`)으로 줄인다. `icon.svg`는 앱 저장소 `scripts/icon/make_icons.py`의 `svg('any')` 출력이다. 아이콘이나 화면이 바뀌면 다시 만든다.
- 링크와 `style.css`는 상대 경로로 쓴다. `404.html`만 어느 경로에서나 쓰이므로 `/style.css`를 쓴다 (사용자 도메인 루트 기준).
- 한국어와 영어 페이지는 서로 링크한다 (상단 `nav`, 2026-10-22에 되살렸다). Play Console에는 방침 URL을 하나만 넣을 수 있어 영어판을 넣고, 거기서 한국어판으로 간다.
- 앱은 방침을 주소 끝에 `#app`을 붙여 앱 안 웹 뷰로 연다. 그때는 다른 페이지로 옮겨 가지 않게 링크를 없앤다: 방침 페이지 `<body>` 맨 앞의 `<span id="app"></span>`와 `style.css`의 `#app:target` 규칙이 `nav`를 숨기고, 본문의 사이트 안 링크(`class="site-link"`)를 누를 수 없게 한다.
  방침 본문에 사이트 안 링크를 더하면 `class="site-link"`를 붙인다. 바깥 링크(다른 사이트, `mailto:`)는 앱이 밖으로 연다.
- 새 앱은 `sararak/`을 복사해 내용을 바꾼다. 언어별 페이지는 `ko/`, `en/` 아래에 두고 앱 디렉터리의 `index.html`은 `en/`으로 보낸다 (GitHub Pages에 서버 리다이렉트가 없어 `<head>` 맨 앞의 `location.replace("en/")`로 바로 넘기고, JS가 꺼진 환경과 검색 엔진을 위해 0초 `meta refresh` + `canonical`을 함께 둔다. 넘어가는 동안 글자가 비치지 않게 대체 링크는 CSS로 숨겼다가 2초 뒤에 보이고, 바탕은 홍보 페이지와 같은 색으로 인라인 CSS에 둔다). 루트 `index.html`에는 링크를 두지 않는다 (빈 페이지).

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
- [ ] 루트 `index.html`의 용도를 정한다 (지금은 빈 페이지). Google 검색 결과의 파비콘은 호스트 루트 페이지의 것만 쓰므로, 루트에 아이콘이 없으면 사라락 페이지에도 기본 아이콘이 보인다
- [ ] Google Search Console과 네이버 서치어드바이저에 `plan275.com`을 등록하고 `sitemap.xml`을 제출한다 (소유 확인은 사용자)
- [ ] "폴더블과 아이폰 듀오" 절에 화면 캡처를 더한다 (아이폰 듀오 펼침 또는 Android 폴더블 테이블탑). 2026-10-31에는 시뮬레이터를 명령으로 펼칠 수 없어 글만 넣었다 (`simctl`에 접기 명령 없음)
- [ ] 스토어에 출시되면 홍보 페이지의 "출시 예정"을 스토어 링크(배지)로 바꾸고, 구조화 데이터에 스토어 주소(`sameAs` 등)를 더한다
