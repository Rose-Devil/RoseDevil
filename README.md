# WebRTC P2P 화상 통화 (Vite + React)

Socket.IO 시그널링 서버를 사용해 1:1 WebRTC P2P 화상/음성 통화, 화면 공유, 파일 전송을 지원하는 데모입니다.

## 주요 기능
- 방 ID로 빠르게 연결 (새 사용자가 참여·퇴장 시 자동 알림)
- 카메라/마이크 ON·OFF 토글
- 화면 공유 (화면 전환 시 원본 카메라로 복귀)
- 파일 전송(DataChannel)
- 상대방 퇴장 시 자동 정리

## 프로젝트 구조
- `src/` 프론트엔드 (React + Vite)
- `server/` Socket.IO 기반 시그널링 서버 (Express)

## 설치 & 실행
### 1) 시그널링 서버
```bash
cd server
npm install
npm start   # 기본 포트: 3001
```

### 2) 프론트엔드
```bash
npm install
npm run dev -- --host   # 기본 포트: 5173
```

## 시그널링 서버 주소 변경 (선택)
클라이언트는 기본적으로 `https://averse-estella-washed.ngrok-free.dev`에 연결합니다. 로컬 서버를 사용할 경우 `src/services/SignalingService.js`의 `connect(serverUrl)` 호출 시 `http://localhost:3001` 등을 인자로 넘기세요.

```js
// App.jsx 등에서
signalingRef.current.connect("http://localhost:3001");
```

## 사용 방법
1. 서버와 프론트를 각각 실행합니다.
2. 브라우저 두 개(또는 시크릿 창 포함)를 열어 동일한 방 ID로 접속합니다.
3. 권한 허용 후 통화, 화면 공유, 파일 전송을 테스트합니다.
4. 종료 시 통화 종료 버튼으로 방을 정상적으로 떠날 수 있습니다.

## 기타
- 포트가 다르면 CORS 설정을 맞춰야 합니다. 기본 서버 CORS는 `http://localhost:5173`을 허용합니다.
- 추가 기능/버그 수정이 필요하면 `server/server.js`와 `src/services/SignalingService.js`를 참고하세요.
