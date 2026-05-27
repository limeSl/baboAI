# baboAI — 개발 컨텍스트

## 무엇을 만들고 있나?

중학교 수행평가용 웹앱. 학생이 Teachable Machine으로 직접 만든 이미지 분류 모델을 바탕으로, 클래스별 결과 카드(이미지 + 제목 + 설명)를 편집하면 완성된 분류 앱을 **HTML 파일 하나**로 다운로드해주는 빌더 툴.

학생이 만든 `app.html`이 수행평가 결과물이 된다.

## 구조

```
C:\Users\wcdus\baboAI\
  index.html    ← 편집기 (단일 파일, 전체 구현)
```

- GitHub 레포: `github.com/limeSl/baboAI`
- 배포: GitHub Pages → `https://limesl.github.io/baboAI/`
- 빌드 없음, 순수 HTML/JS/CSS

## 사용 흐름

```
① 학생이 baboAI 접속
② 티쳐블 머신 export 파일 3개 업로드 (model.json, weights.bin, metadata.json)
   또는 TM 공유 URL 입력
③ 클래스별 결과 이미지 + 제목 + 설명 입력
④ "완료 → 앱 다운로드" 클릭 → app.html 다운로드
⑤ 학생이 app.html을 브라우저로 열면 → 웹캠/사진 업로드 → AI 분류 → 결과 카드
```

## 기술 핵심

- CDN: `@tensorflow/tfjs@1.3.1` + `@teachablemachine/image@0.8`
- 모델 파일 업로드 시 → base64로 인코딩해서 output HTML에 임베드
- URL 방식은 그대로 URL을 임베드
- 생성된 `app.html`은 완전 자급자족 (모델 + 템플릿 설정 모두 포함)
- AI 추론은 브라우저에서 로컬 실행 → 서버 부하 없음, 동접 제한 없음

## 디자인

myEZtool의 미니멀 스타일과 **다름** — baboAI는 중학생 대상이라 산뜻한 웹앱 스타일.

- 배경: `#f0f2ff` (연보라)
- 카드: 흰색 + `box-shadow`
- 액센트: `#6366f1` (인디고)
- 버튼: 크고 색깔 있게, 라운드 코너
- 편집기와 생성된 앱 둘 다 동일 테마 적용

## 현재 상태

- `index.html` 구현 완료 및 배포됨
- 로컬 테스트: `python -m http.server 8080` 후 `http://localhost:8080`

## 남은 것 (추후 과제)

- 실제 TM 모델 파일로 end-to-end 테스트 미완
- 생성된 app.html의 앱 제목 커스터마이즈 기능 없음
- 결과 배경색 등 스타일 커스터마이즈 미구현
- 클래스별 설명 입력란이 한 줄 input — textarea로 바꾸면 더 좋을 수 있음
