# 📊 Google Sheets 온라인 저장 설정 가이드

GitHub Pages에서 교과목 추천 결과를 온라인으로 자동 저장하는 방법입니다.

## 🎯 개요

- **목적**: 추천 결과를 Google Sheets에 자동으로 누적 저장
- **장점**: 무료, 설정 간단, 실시간 확인 가능, 데이터 분석 용이
- **소요 시간**: 약 5-10분

---

## 📝 설정 단계

### 1단계: Google 스프레드시트 생성

1. [Google Drive](https://drive.google.com) 접속
2. **새로 만들기** → **Google Sheets** → **빈 스프레드시트** 클릭
3. 스프레드시트 이름을 `교과목추천_데이터` 로 변경

### 2단계: Apps Script 열기

1. 생성한 스프레드시트에서 **확장 프로그램** → **Apps Script** 클릭
2. 새 창이 열리면 기본 코드를 모두 삭제

### 3단계: 스크립트 코드 붙여넣기

1. `google-apps-script.js` 파일의 전체 내용을 복사
2. Apps Script 에디터에 붙여넣기
3. 파일 이름을 `코드.gs`로 변경 (선택사항)
4. **저장** 버튼 클릭 (💾 아이콘)

### 4단계: 웹 앱으로 배포

1. 오른쪽 상단의 **배포** → **새 배포** 클릭
2. 설정:
   - **유형 선택**: ⚙️ 아이콘 클릭 → **웹 앱** 선택
   - **설명**: `교과목 추천 데이터 수집` (선택사항)
   - **실행 계정**: "나" 선택
   - **액세스 권한**: **"모든 사용자"** 선택 ⚠️ 중요!
3. **배포** 버튼 클릭
4. 권한 승인 과정:
   - Google 계정 선택
   - "고급" 클릭
   - "안전하지 않은 페이지로 이동" 클릭 (안전함)
   - "허용" 클릭

### 5단계: 배포 URL 복사

1. 배포 완료 후 **웹 앱 URL** 복사
   - 예시: `https://script.google.com/macros/s/AKfycby.../exec`
2. 이 URL을 메모장에 저장

### 6단계: index.html 수정

1. `index.html` 파일 열기
2. 다음 줄 찾기 (약 114줄):
   ```javascript
   const GOOGLE_SCRIPT_URL = ''; // 예: 'https://script.google.com/macros/s/YOUR_SCRIPT_ID/exec'
   ```
3. 복사한 URL을 붙여넣기:
   ```javascript
   const GOOGLE_SCRIPT_URL = 'https://script.google.com/macros/s/AKfycby.../exec';
   ```
4. 파일 저장

---

## ✅ 테스트

### 로컬 테스트

1. `index.html` 파일을 웹 브라우저에서 열기
2. 설문 작성 후 "추천 과목 보기" 클릭
3. 결과 화면에서 "✅ 온라인 저장 완료" 메시지 확인

### 스프레드시트 확인

1. Google 스프레드시트로 돌아가기
2. 새로고침 (F5)
3. 다음 헤더가 자동으로 생성되었는지 확인:
   - 제출시간 | 전공 | 학번 | 한국어 수준 | 원하는 분야 | 상호작용 | 추천 과목 수 | 추천 과목 목록
4. 테스트 데이터 행 확인

---

## 🚀 GitHub Pages 배포

### 배포 방법

1. GitHub 저장소 생성 (예: `course-recommender`)
2. 파일 업로드:
   - `index.html`
   - `styles.css`
   - `courses_new.csv` (선택사항, 참고용)
3. 저장소 설정:
   - **Settings** → **Pages**
   - **Source**: `main` 브랜치 선택
   - **Save** 클릭
4. 5-10분 후 URL로 접속:
   - 예: `https://[username].github.io/course-recommender/`

### 주의사항

- `google-apps-script.js` 파일은 업로드하지 않아도 됨 (참고용)
- `GOOGLE_SCRIPT_URL`이 설정되어 있어야 온라인 저장 작동
- 로컬 TXT 다운로드는 항상 작동 (백업용)

---

## 📊 데이터 활용

### 스프레드시트에서 할 수 있는 것

1. **실시간 모니터링**: 학생들의 추천 결과 즉시 확인
2. **데이터 분석**:
   - 가장 많이 선택된 한국어 수준
   - 인기 있는 분야
   - 추천 과목 통계
3. **필터링 및 정렬**: 학번, 전공, 날짜별 정렬
4. **차트 생성**: 시각화 차트 자동 생성
5. **데이터 내보내기**: Excel, CSV로 내보내기

### 데이터 관리 팁

- 정기적으로 데이터 백업 (다운로드)
- 학기별로 시트 분리 (시트 추가 기능 사용)
- 민감한 정보 주의 (학번 일부만 저장 등)

---

## 🔧 문제 해결

### "온라인 저장 실패" 메시지가 나올 때

1. **GOOGLE_SCRIPT_URL 확인**
   - URL이 정확히 입력되었는지 확인
   - 따옴표 안에 URL이 있는지 확인

2. **Apps Script 배포 재확인**
   - "모든 사용자" 권한으로 배포되었는지 확인
   - 새 배포 버전으로 다시 배포 시도

3. **브라우저 콘솔 확인**
   - F12 → Console 탭
   - 에러 메시지 확인

### 데이터가 저장되지 않을 때

1. Apps Script 실행 로그 확인:
   - Apps Script 에디터 → **실행 로그** 클릭
   - 오류 메시지 확인

2. 권한 재설정:
   - 배포 → 배포 관리
   - 기존 배포 삭제
   - 새 배포 다시 생성

---

## 💡 추가 기능 (선택사항)

### 이메일 알림 설정

Apps Script에 다음 함수 추가:

```javascript
function sendEmailNotification(data) {
  const email = 'your-email@example.com';
  const subject = '새 교과목 추천 제출: ' + data.studentId;
  const body = `
    전공: ${data.major}
    학번: ${data.studentId}
    한국어 수준: ${data.koreanLevel}
    추천 과목 수: ${data.recommendedCount}
  `;

  MailApp.sendEmail(email, subject, body);
}
```

그리고 `doPost` 함수의 `sheet.appendRow` 다음 줄에 추가:

```javascript
sendEmailNotification(data);
```

### 자동 정리 스크립트

매주 월요일 자동으로 정리:

```javascript
function autoArchive() {
  const sheet = SpreadsheetApp.getActiveSpreadsheet().getActiveSheet();
  const lastWeek = new Date();
  lastWeek.setDate(lastWeek.getDate() - 7);

  // 일주일 이상 된 데이터를 다른 시트로 이동
  // ... 구현 코드
}

// 트리거 설정: 매주 월요일 오전 9시
```

---

## 📞 지원

문제가 발생하면:
1. 이 문서의 **문제 해결** 섹션 참고
2. Apps Script 공식 문서: https://developers.google.com/apps-script
3. GitHub Issues에 문의

---

## ⚖️ 개인정보 보호

- 학생 정보는 Google Drive에 안전하게 저장됨
- 스프레드시트 공유 설정 주의
- 민감한 정보는 익명화 권장
- GDPR 및 개인정보보호법 준수 필요

---

**설정이 완료되었습니다!** 🎉

이제 GitHub Pages에서 실행될 때마다 자동으로 Google Sheets에 데이터가 저장됩니다.
