# Team jAm 차트 대시보드

ZRcamera(iPhone·유료)와 HotSauce(Mac·무료)의 App Store 차트 순위를 한 화면에서 본다.
**파일 하나(`index.html`)뿐이고 서버가 필요 없다** — 브라우저가 애플의 공개 차트 피드를 직접 읽는다.

## 올리는 법 (Netlify)

1. https://app.netlify.com → **Add new site → Deploy manually**
2. 이 폴더(`team-jam-dashboard`)를 통째로 끌어다 놓는다.
3. 끝. 주소는 Site configuration → **Change site name**에서 바꾼다.

고친 뒤에는 같은 화면에 폴더를 다시 끌어다 놓으면 갱신된다.

## 무엇을 보여 주나

| 앱 | 카테고리 차트 | 전체 차트 |
|---|---|---|
| ZRcamera (iPhone·유료) | 사진 및 비디오 유료 | 전체 유료 |
| HotSauce (Mac·무료) | 유틸리티 무료 | 전체 무료 |

나라 = 한국 · 미국 · 일본 · 대만 · 홍콩 · 영국. 앞뒤 경쟁 앱도 함께 보인다(좁은 화면에서는 숨김).

## 알아 둘 것

- 피드는 **하루 한 번쯤** 갱신된다. 실시간이 아니다.
- 차트는 나라마다 100위 안팎까지만 내려온다. `—`는 그 아래라는 뜻이지 판매가 없다는 뜻이 아니다.
- **전체 칸은 옛 iPhone 피드 기준**이라 App Store 앱에 보이는 전체 순위와 다를 수 있다
  (같은 날 한국 = 옛 피드 97위 · 애플 최신 피드 34위). 카테고리 칸이 실제로 겨루는 자리다.
  최신 전체 순위는 `Marketing/scripts/chart_rank.py`가 쓰는 `rss.marketingtools.apple.com`
  피드가 정확한데, 그 피드는 브라우저에서 직접 못 읽는다(CORS 차단) — 필요해지면 Netlify Function을 하나 둔다.
- 카테고리 차트는 애플의 **옛 피드**(`itunes.apple.com/.../rss/...`)라 언젠가 닫힐 수 있다.
- 검색 색인은 막아 뒀다(`noindex`). 주소를 아는 사람만 본다.

## 나라·앱을 더하려면

`index.html` 맨 아래 `COUNTRIES`와 `APPS` 배열만 고치면 된다. 앱을 더할 때는
`id`(App Store 숫자 id)와 차트 종류(`toppaidapplications` · `topfreeapplications` ·
`topfreemacapps` · `toppaidmacapps`)와 `genre`(예: 사진 및 비디오 6008 · 유틸리티 6002)를 적는다.

## 곁가지

터미널에서 같은 값을 보려면 `Marketing/scripts/chart_rank.py`.
