# 플랜두씨 다이어리 1

로그인 없이 계획 → 실제로 한 일 → 돌아보기를 Supabase에 저장하는 정적 웹앱입니다.

## 1. 파일

- `index.html` — 화면
- `styles.css` — UI
- `app.js` — Supabase 연동 및 기능
- `supabase.sql` — DB 표/관계/RLS/RPC
- `contracts/pds-schema-v2.json` — 최종 DB 계약서

## 2. Supabase 연동

1. Supabase에서 새 프로젝트를 만듭니다.
2. SQL Editor에 `supabase.sql` 전체를 붙여 넣고 Run 합니다.
3. Project Settings → API에서 **Project URL**과 **anon/publishable key**를 확인합니다.
4. `app.js` 맨 위의 두 상수를 교체합니다.

```js
const SUPABASE_URL = "https://YOUR_PROJECT.supabase.co";
const SUPABASE_ANON_KEY = "YOUR_SUPABASE_ANON_OR_PUBLISHABLE_KEY";
```

브라우저에 넣어도 되는 것은 Project URL + anon/publishable key뿐입니다. `service_role`/secret key는 절대 넣지 않습니다.

5. `index.html`과 `styles.css`, `app.js`, `contracts/`를 같은 웹 호스트에 올립니다.
6. 첫 화면에서 "Supabase 연결됨"을 확인합니다.

## 3. 실제 자료 입력 순서

1. 계획에서 지금 실제로 하고 있는 일을 1개 추가합니다.
2. 그 계획에 할 일을 5개 이상 추가합니다.
3. 완료/되돌리기, 실행 기록 3개 이상을 실제로 사용합니다.
4. 계획을 한 번 수정해 "수정 이력"에서 이전 값을 확인합니다.
5. 돌아보기의 숫자를 눌러 근거 기록을 확인합니다.
6. "전체 자료 JSON 내보내기"로 백업합니다.
7. 새로고침해서 값이 그대로인지 확인합니다.

## 4. 제출 전 점검

- 새 시크릿 창에서 로그인 없이 열리는가?
- 첫 화면 공개 안내가 보이는가?
- 실제 계획 1개 이상 / 할 일 5개 이상 / 실행 기록 3개 이상인가?
- 계획 수정 전 값이 `plan_versions`에 남는가?
- 완료 버튼을 연속 두 번 눌러도 `task_completions`가 1건인가?
- 서울 시간 기준 지연 계산이 맞는가?
- 예상/실제/차이가 맞는가?
- JSON export가 되는가?
- `<script>` 같은 문자열을 입력해도 실행되지 않는가?
- 브라우저 코드/네트워크 응답/콘솔/Git 기록에 secret/service_role key가 없는가?

## 5. 4줄 확인 방법

① 어디로 가나요: 배포 주소를 새 시크릿 창에서 엽니다.  
② 세 단계 안에 무엇을 하나요: 계획 → 할 일 → 실행 기록으로 이동합니다.  
③ 무엇이 보이면 통과인가요: 저장한 값이 새로고침 뒤에도 남고, 돌아보기 숫자와 근거 기록이 일치합니다.  
④ 안 될 때는 무엇이 보이나요: 첫 화면의 "Supabase 연결이 필요합니다" 또는 하단 오류 메시지를 확인합니다.

## 6. AI와 내 판단 3줄

① AI에게 맡긴 일: 데이터 모델, RLS/RPC, 화면과 CRUD 구현 초안을 맡겼습니다.  
② 내가 직접 판단한 일: 로그인 없는 공개 단계, 실제 데이터 입력 방식, 계획 이력/완료 중복 방지/서울 시간 집계 규칙을 확인합니다.  
③ AI 말을 따르지 않은 일: 실제 개인 데이터는 AI가 알 수 없으므로 예시 데이터를 넣지 않고 내가 직접 입력합니다.
