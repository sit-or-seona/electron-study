# 용어 사전

## 1. IPC

- Inter-Process Communication의 약자로 프로세스 간 통신을 의미
- 일렉트론이 main process와 renderer process 간 직렬화된 JSON 메세지를 주고 받기 위해 사용

## 2. process

- 실행 중인 컴퓨터 프로그램의 인스턴스
- 일렉트론 앱은 main과 하나 이상의 renderer process 사용해 여러 프로그램을 동시에 실행
- `process` 객체 (전역 객체)
  - Node.js와 일렉트론에서 실행 중인 각각의 프로세스는 process 객체를 가지고 있음
  - 현재의 process에 대한 정보와 제어를 제공
  - 전역 객체로써 `require()` 작성 없이 사용 가능

## 3. main process

- 모든 일렉트론 앱의 진입점
- 일반적으로 `main.js` 라는 파일명을 지정
- 역할
  - 시작부터 종료까지 앱의 수명을 제어
  - 기본 요소(메뉴, 메뉴바 등)을 관리
  - 앱에서 새로운 renderer process를 생성하는 일을 담당
- Node API가 내장되어 있음
- 모든 앱의 main process 파일은 `package.json`에 `main` 프로퍼티로 지정
  - 이 때문에 `electron .`이 시작할 때 실행할 파일을 알 수 있음
- Chromium에서는 이 process는 "browser process"라고 지칭

## 4. renderer process

- 앱의 브라우저 창
- main process와 달리, 여러 개가 있을 수 있고 각각 별도의 process에서 작동
- 숨기기 가능

## 5. utility process

- main process의 하위 프로세스
- main process에서 실행할 수 없는 신뢰할 수 없는 서비스를 실행 가능
- Chromium은 utility process를 사용해 네트워크 I/O, 오디오/비디오 처리, 기기 입력 등을 수행
- UtilityProcess API를 사용해 utility process 생성

## 6. preload script

- renderer process에서 웹 콘텐츠가 로드되기 전에 실행되는 코드를 preload script에 작성
- renderer context 내에서 실행되지만 Node.js API를 엑세스할 수 있기 때문에 더 많은 권한이 부여됨
