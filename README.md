# 에너지 전환 보드게임 · 온라인 대전 사이트

친구들이 각자 자기 폰이나 컴퓨터로 같은 방에 들어와서 대전하는 웹사이트예요. 홈 화면에 추가하면 앱처럼 쓸 수 있어요.
처음 한 번만 아래 순서대로 설정하면 돼요. 모두 무료예요. (20~30분)

## 파일 구성
- `index.html` : 게임 본체 (한 기기 모드 + 온라인 대전)
- `config.js` : Firebase 설정을 붙여 넣는 파일 ← **여기만 고치면 돼요**
- `database.rules.json` : Firebase 보안 규칙 (복사해서 붙여 넣기용)
- `manifest.webmanifest`, `sw.js`, `icon-*.png` : 폰에 앱처럼 설치하기 위한 파일

## 1단계. Firebase 프로젝트 만들기
1. https://console.firebase.google.com 에 구글 계정으로 로그인
2. **프로젝트 추가** → 이름 예: `energy-game` → Google 애널리틱스는 **사용 안 함** → 만들기

## 2단계. 데이터베이스와 로그인 켜기
1. 왼쪽 메뉴 **빌드 → Realtime Database → 데이터베이스 만들기**
   - 위치: **싱가포르 (asia-southeast1)** (한국에서 가장 가까움)
   - 보안 규칙: **잠금 모드로 시작**
2. 만들어지면 **규칙** 탭 → 내용을 지우고 `database.rules.json` 내용을 그대로 붙여 넣기 → **게시**
3. 왼쪽 메뉴 **빌드 → Authentication → 시작하기 → 로그인 방법 → 익명 → 사용 설정 → 저장**
   (친구들이 회원가입 없이 바로 들어올 수 있게 해 주는 설정이에요)

## 3단계. 설정값을 config.js에 붙여 넣기
1. 왼쪽 위 **톱니바퀴 → 프로젝트 설정 → 일반** 탭 아래 **내 앱 → 웹(</>) 아이콘**
2. 앱 닉네임 아무거나 → **앱 등록** (Firebase 호스팅 체크는 안 해도 됨)
3. 화면에 나오는 `const firebaseConfig = { ... }` 의 중괄호 부분을 복사
4. `config.js`를 메모장으로 열어서 `window.FIREBASE_CONFIG = null;` 을 아래처럼 바꾸기
   ```js
   window.FIREBASE_CONFIG = { apiKey: "...", authDomain: "...", databaseURL: "...", projectId: "...", appId: "..." };
   ```
   - **databaseURL** 이 꼭 들어 있어야 해요. 없으면 Realtime Database 화면 맨 위의 주소(https://...firebasedatabase.app)를 직접 넣어 주세요.
   - apiKey는 공개돼도 괜찮은 값이에요. 실제 보호는 2단계의 보안 규칙이 해요.

## 4단계. GitHub Pages로 사이트 올리기
1. https://github.com 로그인 → 오른쪽 위 **+ → New repository** → 이름 예: `energy-game` → **Public** → Create
2. **uploading an existing file** 링크 → 이 폴더의 파일을 **전부** 끌어다 놓기 → **Commit changes**
3. 저장소의 **Settings → Pages** → Branch: `main` / `(root)` → **Save**
4. 1~2분 뒤 `https://내아이디.github.io/energy-game/` 주소가 생겨요. 이 주소가 게임 사이트예요.

## 5단계. 친구들과 하기
1. 사이트에서 **온라인 대전 → 이름 적기 → 방 만들기** → 4글자 방 코드가 나와요
2. 친구들은 같은 사이트에서 **방 코드로 참가**
3. 2~4명이 모이면 방장이 **게임 시작**
4. 폰에서는 브라우저 메뉴의 **홈 화면에 추가**를 누르면 앱처럼 설치돼요
5. 보고서·발표용 QR 코드는 사이트 주소로 만들면 돼요

## 안 될 때
- **"테스트 모드" 문구가 보여요** → config.js가 아직 `null`이거나 databaseURL이 빠졌어요
- **방 만들기를 눌러도 반응이 없어요** → 2단계의 익명 로그인을 켰는지, 규칙을 게시했는지 확인
- **사이트가 예전 버전으로 보여요** → 새로고침을 두 번 하거나, 홈 화면 앱을 지웠다 다시 추가
- 게임 중에 창을 닫았다면 **온라인 대전 → 지난 방으로 돌아가기**로 같은 자리에 다시 들어갈 수 있어요

## 알아 둘 점
- 라운드 끝 정산은 방장이 눌러요. 방장이 나가면 그 판은 더 진행할 수 없어요.
- 무료 요금제(Spark)로 반 친구들끼리 하기에는 충분해요.
