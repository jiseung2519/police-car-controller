# Police Car Controller 설치 안내 (Android)

이 폴더는 네이티브 APK가 아니라 Android Chrome에 설치할 수 있는 PWA(웹앱) 패키지입니다. BLE 권한과 Web Bluetooth API를 사용하므로 HTTPS로 호스팅해야 합니다. PC의 `file://`로 직접 열거나 일반 HTTP 주소로 열면 BLE 연결이 차단될 수 있습니다.

## 1. GitHub Pages로 공개 배포

1. GitHub에 로그인하고 새 repository를 만듭니다. 예: `police-car-controller`.
2. 이 ZIP을 풀고 `index.html`, `manifest.webmanifest`, `sw.js`, `icons/` 폴더를 repository 최상위(root)에 업로드합니다.
3. repository의 **Settings → Pages**로 이동합니다.
4. **Build and deployment → Deploy from a branch**를 선택합니다.
5. Branch는 `main`, folder는 `/(root)`로 설정하고 Save 합니다.
6. Pages가 배포되면 `https://<GitHub계정>.github.io/police-car-controller/` 형태의 주소가 만들어집니다.

GitHub Pages 공식 안내: https://docs.github.com/pages/getting-started-with-github-pages/creating-a-github-pages-site

주의: 공개 repository에 업로드할 파일에는 비밀번호나 개인 키가 없어야 합니다. 이 앱 파일에는 그런 비밀정보를 넣지 않았습니다.

## 2. Android 스마트폰에 설치

1. Android에서 Chrome을 실행합니다.
2. 위의 HTTPS Pages 주소를 엽니다.
3. 페이지가 완전히 열린 뒤 우측 상단 ⋮ 메뉴를 누릅니다.
4. **Install app** 또는 **Install and create shortcut**을 선택합니다. 메뉴 이름은 Chrome 버전에 따라 다를 수 있습니다.
5. 설치가 끝나면 홈 화면/앱 목록에 `Police Car` 아이콘이 생깁니다.

Google Chrome 안내: https://support.google.com/chrome/answer/9658361

## 3. 차량 연결

1. XIAO ESP32S3 Sense에 해당 펌웨어를 업로드하고 전원을 켭니다.
2. XIAO가 BLE 장치 `PoliceCar-XIAO`로 광고하는지 확인합니다.
3. 스마트폰에서 설치한 `Police Car`를 실행하고 **XIAO 연결**을 누릅니다.
4. Bluetooth 기기 선택창에서 `PoliceCar-XIAO`를 선택합니다.
5. 처음에는 차체를 받침대에 올려 구동륜이 바닥에서 뜬 상태로 STOP, 상태 확인, 저속 수동 구동을 시험합니다.

## 지원 및 제한

- 권장: Android + 최신 Chrome. Web Bluetooth는 HTTPS 보안 컨텍스트에서 사용해야 합니다.
- iPhone/iPad의 기본 Safari 및 Chrome(iOS)은 Web Bluetooth를 지원하지 않으므로 현재 BLE 연결 기능을 그대로 사용할 수 없습니다. iOS를 지원하려면 별도 네이티브 앱(예: Swift/CoreBluetooth) 또는 BLE 브리지를 개발해야 합니다.
- 서비스 워커는 웹 페이지 리소스를 캐시하지만, BLE 연결 자체는 XIAO가 켜져 있고 Bluetooth가 활성화되어 있어야 합니다.
- 이 앱은 로봇 펌웨어와 UUID가 일치하도록 만들어졌습니다. XIAO BLE 서비스 UUID 및 특성 UUID를 임의로 바꾸면 연결되지 않습니다.
