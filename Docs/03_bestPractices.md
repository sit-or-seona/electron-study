# Performance

# Security

## 보안 권장 사항

### 2. Node.js 통합 비활성화할 것

- (참고) Electron 5.0.0.에선 default 동작이었음

**Why?**

- cross-site-scripting (XSS) 공격

**How?**

```js
// main.js
// Bad
const mainWindow = new BrowserWindow({
  webPreferences: {
    contextIsolation: false,
    nodeIntegration: true,
    nodeIntegrationInWorker: true,
  },
});

mainWindow.loadURL("https://example.com");
```

```js
// main.js
// Good
const mainWindow = new BrowserWindow({
  webPreferences: {
    preload: path.join(app.getAppPath(), "preload.js"),
  },
});

mainWindow.loadURL("https://example.com");
```

```js
// index.html (렌더러 프로세스)
<!-- Bad -->
<webview nodeIntegration src="page.html"></webview>

<!-- Good -->
<webview src="page.html"></webview>
```

- Node.js 통합을 비활성화해도 Node.js 모듈 또는 기능을 사용하는 API를 웹 사이트에 노출할 수 있음
- preload 스크립트는 require 및 Node.js 기능에 접근할 수 있기 때문에 개발자는 contextBridge API를 통해 원격으로 로드된 컨텐츠에 커스텀 API를 노출 가능
