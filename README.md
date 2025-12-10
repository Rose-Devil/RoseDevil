


# WebRTC P2P 화상 통화 (Vite + React)

Socket.IO 시그널링 서버를 사용해 1:1 WebRTC P2P 화상/음성 통화, 화면 공유, 파일 전송을 지원하는 데모입니다.

# WebRTC P2P 화상통화 & 파일전송

> 브라우저 간 직접 연결(P2P)을 통한 실시간 화상통화 및 파일 전송

## 프로젝트 소개

WebRTC를 활용한 브라우저 간 P2P 화상통화 및 파일 전송 애플리케이션입니다.

### 주요 기능

- 🎥 **실시간 화상통화** - HD 영상/음성 통신
- 🖥️ **화면 공유** - 전체 화면 또는 특정 창 공유
- 📁 **P2P 파일 전송** - 서버를 거치지 않는 직접 전송
- 🔒 **보안** - DTLS/SRTP 암호화

## 기술 스택

**Frontend**
- React 18 + Vite
- Socket.IO Client
- WebRTC API

**Backend**
- Node.js + Express
- Socket.IO

## 설치 및 실행

### 1. 프로젝트 클론

```bash
git clone https://github.com/your-username/webrtc-p2p.git
cd webrtc-p2p
```

### 2. 의존성 설치

```bash
# 서버
cd server
npm install

# 클라이언트
cd ..
npm install
```

### 3. 실행 (3개 터미널 필요)

#### 터미널 1: 시그널링 서버

```bash
cd server
node server.js
```

#### 터미널 2: React 앱

```bash
npm run dev
```

브라우저에서 자동으로 `http://localhost:5173` 열림

#### 터미널 3: ngrok (외부 접속용, 선택사항)

```bash
# ngrok 설치
brew install ngrok  # macOS
# 또는
choco install ngrok  # Windows

# 시그널링 서버 터널링
ngrok http 3001
```

**ngrok URL 복사 후 환경변수 설정:**

```bash
# .env.local 파일 생성
VITE_SIGNALING_URL=https://your-ngrok-url.ngrok.io
```

## 사용 방법

### 로컬 테스트

1. **첫 번째 탭**: `http://localhost:5173` 접속 → 방 ID 입력 → 참가
2. **두 번째 탭**: 새 탭 열기 → 같은 방 ID 입력 → 참가
3. P2P 연결 자동 성립

### 외부 테스트 (ngrok 사용)

1. ngrok으로 시그널링 서버 터널링
2. `.env.local`에 ngrok URL 설정
3. React 앱도 터널링 (선택): `ngrok http 5173`
4. 스마트폰이나 외부 네트워크에서 접속 가능

## 프로젝트 구조

```
webrtc-p2p/
├── server/
│   ├── server.js              # Express + Socket.IO 서버
│   └── package.json
├── src/
│   ├── App.jsx                # 메인 앱
│   ├── services/
│   │   ├── SignalingService.js    # Socket.IO 시그널링
│   │   ├── WebRTCService.js       # WebRTC 연결
│   │   ├── MediaService.js        # 미디어 관리
│   │   └── FileTransferService.js # 파일 전송
│   └── main.jsx
├── package.json
└── vite.config.js
```

## 핵심 기술

### WebRTC 3대 API

- **getUserMedia**: 카메라/마이크 접근
- **RTCPeerConnection**: P2P 연결
- **RTCDataChannel**: 데이터 전송 (파일)

### 시그널링 프로토콜

Socket.IO를 통한 WebRTC 메타데이터 교환:
- `join-room`: 방 참가
- `offer/answer`: SDP 교환
- `ice-candidate`: NAT 통과 정보
- `user-left`: 연결 해제

## 문제 해결

### 카메라/마이크 권한 오류

브라우저 주소창 → 자물쇠 아이콘 → 권한 허용

### P2P 연결 실패

방화벽 또는 대칭형 NAT 환경일 경우 TURN 서버 추가 필요

### ngrok CORS 오류

```javascript
// server/server.js
cors: {
  origin: ['http://localhost:5173', 'https://*.ngrok.io']
}
```


## 참고 자료

- [WebRTC API](https://developer.mozilla.org/en-US/docs/Web/API/WebRTC_API)
- [Socket.IO Docs](https://socket.io/docs/v4/)
- [ngrok Docs](https://ngrok.com/docs)
