# photo-six 콘텐츠 피드

포토식스(iOS) 앱의 **홈 탭에 뜨는 글 목록**입니다. 앱이 실행될 때
`https://torchnn.github.io/content/photo-six/articles.json` 을 받아 갑니다.

## 왜 여기 있나

앱이 원격에서 받아야 하는 건 이 글 목록 하나뿐입니다. 그것 때문에 Firebase 를 붙이면
SDK 가 gRPC·BoringSSL 을 줄줄이 끌고 와 빌드가 느려지고 앱이 커집니다.
정적 JSON 으로 두면 **`git push` 한 번에 반영**되고(심사 불필요), 변경 이력이 남고,
PR 로 검토할 수 있습니다. 무엇보다 앱이 **서버로 아무것도 보내지 않는 구조**가 됩니다.

## 글 추가·수정

`articles.json` 의 `articles` 배열에 항목을 넣고 커밋하면 끝입니다.
앱은 `date` 내림차순으로 정렬해 보여 주고, ETag 로 변경 여부만 확인하므로
바뀌지 않았으면 본문을 다시 받지 않습니다.

```json
{
  "id": "고유-슬러그",
  "title": "제목",
  "subtitle": "한 줄 부제",
  "imageURL": "symbol:photo.stack",
  "date": "2026-07-20",
  "body": "문단.\n\n빈 줄로 문단을 나눕니다.",
  "link": "https://... (선택)"
}
```

| 필드 | 설명 |
|---|---|
| `id` | 고유값. 바꾸면 앱에서 다른 글로 취급됩니다 |
| `imageURL` | `symbol:<SF Symbol 이름>` 이면 앱이 암실 톤 커버를 직접 그립니다. `https://…` 이미지도 가능 |
| `date` | `YYYY-MM-DD` (KST 기준) 또는 ISO8601 |
| `body` | 문단 사이는 빈 줄(`\n\n`). 마크다운은 렌더링되지 않습니다 |
| `link` | 있으면 리더뷰 하단에 "원문 보기" 버튼 |

## 주의

- **앱에도 같은 글 5편이 시드로 들어 있습니다**(`PhotoSix/Model/SeedArticles.swift`).
  이 파일을 못 받아오면 시드가 뜹니다. 시드는 오프라인·첫 실행의 바닥이라 지우지 마세요.
- JSON 문법이 깨지면 앱이 조용히 캐시/시드로 내려갑니다. 커밋 전에
  `python3 -m json.tool articles.json > /dev/null` 로 확인해 주세요.
