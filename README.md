# Personal Portfolio

전북대학교 컴퓨터인공지능학부 재학생 여경용의 개인 포트폴리오입니다.
관심 분야와 학습 경험, 개인 프로젝트의 개발 과정을 소개합니다.

**[사이트 보기](https://zichana1598.github.io/portfolio-assignment/)**

## 주요 페이지

| 페이지 | 내용 |
|---|---|
| Home | 자기소개와 대표 프로젝트 |
| About Me | 관심 분야, 기술 스택, 학습 목표 |
| Projects | 개인 프로젝트 목록 |
| Notice Monitor | 전북대학교 공지 모니터링 프로젝트 상세 소개 |

## 기술 스택

- Hugo Extended 0.167.0 · Blowfish
- Markdown · TOML · HTML
- GitHub Actions · GitHub Pages

## 로컬 실행

Git과 [Hugo Extended 0.167.0](https://github.com/gohugoio/hugo/releases/tag/v0.167.0)을 설치합니다.
설치 방법은 [Hugo 공식 문서](https://gohugo.io/installation/)를 참고하세요.

```bash
git clone https://github.com/zichana1598/portfolio-assignment.git
cd portfolio-assignment/site
hugo server --config pages.json --environment development --baseURL http://localhost:1313/
```

브라우저에서 http://localhost:1313/ 에 접속합니다.
`pages.json`에 테마 설정이 있으므로 실행할 때 `--config pages.json`을 함께 지정합니다.

### 프로덕션 빌드

`site/` 디렉터리에서 실행합니다.

```bash
hugo --config pages.json --environment production --minify --enableGitInfo=false --baseURL https://zichana1598.github.io/portfolio-assignment/
```

결과물은 `site/public/`에 생성됩니다.

## 프로젝트 구조

실제 사이트는 `site/`에 있습니다. 루트의 테마 파일과 `exampleSite/`는 배포 대상으로 사용하지 않습니다.

```text
.
├── .github/
│   ├── workflows/hugo-pages.yml       # 자동 배포
│   └── pages_build.py                # 배포 빌드 및 경로 보정
├── site/
│   ├── config/_default/              # Hugo·언어·메뉴·화면 설정
│   ├── content/
│   │   ├── _index.md                 # Home
│   │   ├── about/index.md            # About Me
│   │   └── projects/
│   │       ├── _index.md             # 프로젝트 목록
│   │       └── notice-monitor/index.md
│   ├── assets/
│   │   ├── css/custom.css            # Overview·흐름도·Contact 스타일
│   │   └── img/                      # 소셜 공유 이미지
│   ├── static/                       # 파비콘·manifest
│   ├── i18n/ko.yaml                  # 메뉴 접근성 한국어 번역
│   ├── layouts/
│   │   ├── index.html                # 홈페이지 구성
│   │   ├── _default/                 # 목록·제목 렌더링 재정의
│   │   ├── partials/                 # 홈페이지 본문·Footer·파비콘
│   │   └── shortcodes/               # 프로젝트·기술 스택 카드 등
│   ├── pages.json                    # 배포 주소와 테마 설정
│   ├── go.mod                        # 로컬 테마 모듈 연결
│   └── themes/template/              # Blowfish 테마 원본
├── .github-pages.json                # 배포 스크립트 설정
├── prepare_github_pages.py           # 최초 배포 구조 준비
├── README.md
└── LICENSE
```

| 수정 대상 | 위치 |
|---|---|
| 페이지 본문 | `site/content/` |
| 메뉴 | `site/config/_default/menus.ko.toml` |
| 사이트 제목·프로필 | `site/config/_default/languages.ko.toml` |
| 화면 옵션·Contact 연락처 | `site/config/_default/params.toml` (`[contact]`) |
| 프로젝트 카드 | `site/layouts/shortcodes/project-card.html` (`headingLevel`로 제목 수준 지정) |
| 기술 스택 카드 | `site/layouts/shortcodes/tech-grid.html`, `tech-feature.html` |
| Footer 구성 | `site/layouts/partials/footer.html` |
| 표·흐름도·Contact 스타일 | `site/assets/css/custom.css` |
| 제목 앵커의 Tab 제외 | `site/layouts/_default/_markup/render-heading.html` |
| 메뉴의 접근 가능한 이름 | `site/i18n/ko.yaml` |

테마 템플릿을 변경할 때는 원본 대신 `site/layouts/`의 같은 경로에 파일을 두어 재정의합니다.
`site/public/`과 루트 `public/`은 생성 결과물이므로 직접 수정하지 않습니다.

## 배포

GitHub 저장소의 **Settings → Pages → Source**를 **GitHub Actions**로 설정합니다.
`main`에 푸시하면 `.github/workflows/hugo-pages.yml`이 빌드와 배포를 실행합니다.

저장소 루트에서 변경 파일을 커밋하고 푸시합니다. 아래는 홈페이지 수정 예시입니다.

```bash
git add site/content/_index.md
git commit -m "content: update homepage introduction"
git push origin main
```

[Actions](https://github.com/zichana1598/portfolio-assignment/actions)에서 해당 커밋의
`build`와 `deploy` 성공 여부를 확인한 뒤 공개 사이트에서 변경 내용을 확인합니다.

CI는 Hugo Extended 0.167.0을 사용하며, Pages 주소에 맞게 경로를 보정한 결과물을
루트 `public/`에 생성해 배포합니다. 로컬 빌드의 `site/public/`과는 출력 위치가 다릅니다.
배포에 필요한 Python, Node.js, Go, Sass는 워크플로에서 설치합니다.

## 파비콘

`site/static/favicon.svg`가 원본이며, 남색 배경에 파란 `</>` 심볼을 사용합니다.
AI의 도움을 받아 SVG로 제작하고 librsvg와 Pillow로 PNG·ICO를 생성했습니다.

| 파일 (`site/static/`) | 크기·용도 |
|---|---|
| `favicon-16x16.png`, `favicon-32x32.png` | 브라우저 탭 |
| `favicon.ico` | 16·32·48px 호환 아이콘 |
| `apple-touch-icon.png` | 180×180px, Apple 홈 화면 |
| `android-chrome-192x192.png`, `android-chrome-512x512.png` | 192·512px, manifest 아이콘 |
| `site.webmanifest` | 사이트 이름·색상·상대 아이콘 경로 |

아이콘을 바꾸면 SVG뿐 아니라 PNG·ICO도 함께 갱신합니다.
`site/layouts/partials/favicons.html`은 32px PNG의 해시를 URL에 붙여 캐시를 갱신합니다.
다른 크기만 교체하면 이 해시는 바뀌지 않으므로 전체 아이콘을 함께 관리합니다.

로컬에서는 `/favicon-32x32.png`, 배포 후에는
`/portfolio-assignment/favicon-32x32.png`와 브라우저 탭을 확인합니다.

## 소셜 공유 이미지

링크 미리보기에 사용하는 기본 배너는 `site/assets/img/portfolio-social.png`입니다.
1200×630px 크기로 파비콘과 같은 색상을 사용하며, 원본은 같은 폴더의
`portfolio-social.svg`입니다. AI의 도움을 받아 SVG로 제작하고 librsvg로 PNG를 생성했습니다.

기본 이미지 설정은 `site/config/_default/params.toml`에 있습니다.

```toml
defaultSocialImage = "img/portfolio-social.png"
```

문구나 디자인을 수정하면 SVG에서 PNG를 다시 생성합니다. 테마가 `resources.Get`으로
이미지를 읽으므로 파일은 `static/`이 아닌 `assets/`에서 관리합니다.
별도의 마운트 설정은 사용하지 않습니다.

프로덕션 빌드 후 생성된 HTML의 `og:image`와 `twitter:image`를 확인합니다.
현재 기본 이미지 URL은 다음과 같습니다.

```text
https://zichana1598.github.io/portfolio-assignment/img/portfolio-social.png
```

페이지 번들의 `featured`, `cover`, `thumbnail` 이미지가 있으면 테마가 기본 공유 이미지보다
우선 사용할 수 있습니다. 공유 서비스의 이전 미리보기가 남아 있으면 해당 서비스의 캐시도 확인합니다.

## 출처 및 라이선스

- 정적 사이트 생성기: [Hugo](https://gohugo.io/)
- 테마: [Blowfish](https://github.com/nunocoracao/blowfish) — MIT License, © 2022 Nuno Coração
- 배경과 아이콘: Blowfish에 포함된 자산 사용. 아이콘 출처는 [Font Awesome](https://fontawesome.com/), 이용 조건은 [공식 라이선스 안내](https://fontawesome.com/license/free) 참고
- 배포 준비 및 빌드 스크립트: 수업 제공 자료 사용

Blowfish의 저작권 및 라이선스 고지를 [LICENSE](LICENSE)와
[테마 LICENSE](site/themes/template/LICENSE)에 유지합니다.
개인 소개와 프로젝트 설명은 직접 작성했으며, 일부 설정과 템플릿 수정에는 AI 도구의 도움을 받았습니다.
