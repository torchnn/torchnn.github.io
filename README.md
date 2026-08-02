# torchnn.github.io

torchnn 계정의 **루트 GitHub Pages**. 계정 공용 루트 파일과 앱별 정책·지원 페이지를 한 레포에 둔다.

## 구조
```
app-ads.txt              AdMob 퍼블리셔 인증(pub-8999074049545423) — torchnn 전 앱 공용.
                         크롤러가 도메인 루트에서만 찾으므로 여기(루트)에 둔다.
policy/                  앱별 정책·지원 페이지 (구 torchnn/policies 를 통합)
  index.html             허브(앱 목록)
  assets/style.css       공용 스타일(라이트/다크)
  <앱-slug>/{index,privacy,support}.html
```

## 앱별 URL (App Store Connect 입력용)
| 앱 | 개인정보 처리방침 | 지원 |
|---|---|---|
| 생활투자 지도 | https://torchnn.github.io/policy/life-invest-map/privacy.html | .../support.html |
| 라스트 마일 | https://torchnn.github.io/policy/last-mile/privacy.html | .../support.html |
| 이달의 재료 | https://torchnn.github.io/policy/monthly-ingredients/privacy.html | .../support.html |
| qr_rxtx | https://torchnn.github.io/policy/qr_rxtx/privacy.html | .../support.html |
| 리얼리치 | https://torchnn.github.io/policy/real-rich/privacy.html | .../support.html |
| 밤티 맵 | https://torchnn.github.io/policy/bamti-map/privacy.html | .../support.html |
| 프로의포폴 | https://torchnn.github.io/policy/portfolio-review/privacy.html | .../support.html |
| 이달의 산 | https://torchnn.github.io/policy/monthly-mountains/privacy.html | .../support.html |
| 포토식스 | https://torchnn.github.io/policy/photo-six/privacy.html | .../support.html |
| 판세 | https://torchnn.github.io/policy/fun-chart/privacy.html | .../support.html |
| 기영차트 | https://torchnn.github.io/policy/giyeong-chart/privacy.html | .../support.html |
| 땅따 | https://torchnn.github.io/policy/ddang-dda/privacy.html | .../support.html |

## 새 앱 추가
1. `policy/<앱-slug>/` 에 index·privacy·support.html 추가(기존 앱 복사 후 교체).
2. `policy/index.html` 허브에 카드 한 장 추가.
3. 이 README 의 URL 표에 행 추가.
4. commit & push → 1~2분 뒤 Pages 반영.
5. **라이브 확인** — Pages 는 조용히 404 를 낸다:
   ```bash
   curl -s -o /dev/null -w '%{http_code}\n' https://torchnn.github.io/policy/<slug>/privacy.html
   ```
   200 이 아니면 App Store Connect 에 넣지 말 것.

새 광고 파트너(미디에이션) 추가 시 `app-ads.txt` 에 라인만 더하면 전 앱에 적용된다.
