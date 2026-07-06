# artifacts

공개해도 되는 작업 산출물 모음. 실측 정리·리서치·시각화를 정적 HTML로 담고 GitHub Pages로 서빙한다.

개인 식별 정보(시리얼·자격증명·집 네트워크 주소·호스트명)는 제거한 것만 올린다.

- 사이트: https://nacyot.github.io/artifacts/

## 목록

| 산출물 | 설명 |
|---|---|
| [bambu-p1s-scripting](./bambu-p1s-scripting/) | Bambu Lab P1S를 앱 없이 MQTT·FTPS 프로토콜만으로 제어한 실측 정리 + d3.js 시각화 |

## 구조

```
├── index.html                    랜딩(산출물 목록)
├── vendor/d3.v7.min.js           공용 d3 (상대경로로 참조)
└── <slug>/index.html             각 산출물
```

정적 파일뿐이라 빌드 단계는 없다. `main` 브랜치 루트를 그대로 Pages가 서빙한다.
