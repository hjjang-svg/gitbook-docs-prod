---
layout:
  width: default
  title:
    visible: true
  description:
    visible: false
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
  metadata:
    visible: true
  tags:
    visible: true
  actions:
    visible: true
---

# URL 설정 가이드

앱 설치 유도하기 광고를 집행하려면 광고주 앱에 딥링크를 구현하고, 앱 성과 측정 도구(MMP) 콘솔에서 딥링크를 적용한 트래킹 링크를 만들어야 해요. 이 가이드에서는 딥링크 구현부터 트래킹 링크 생성, 테스트까지 필요한 과정을 순서대로 안내해요.

딥링크를 적용하지 않은 링크는 광고 클릭 이후 중간 웹페이지를 거쳐요. 이미 앱을 설치한 유저가 광고를 눌렀을 때 불필요한 단계를 거치게 되어, 실제 앱 실행 전환율을 떨어뜨리는 요인이 될 수 있어요. 딥링크를 적용하면 기설치 유저가 광고를 누르는 순간 앱이 곧바로 실행되어 랜딩 경험이 크게 개선돼요.

{% hint style="info" %}
소재 규격과 링크 제출 규칙은 [앱 설치 소재 가이드](creative.md)에서 안내하고 있어요.
{% endhint %}

## 한눈에 보기

딥링크 설정은 개발팀과 마케팅팀이 아래 순서로 진행해요.

<table><thead><tr><th width="232.46484375">단계</th><th width="128.1875">담당</th><th>하는 일</th></tr></thead><tbody><tr><td>1. 앱에 딥링크 구현하기</td><td>개발팀</td><td>앱 코드와 웹 서버에서 앱 스킴, Universal Link, App Link가 작동하도록 구현하고 빌드를 배포해요.</td></tr><tr><td>2. 구현 값 전달하기</td><td>개발팀</td><td>앱 스킴, Bundle ID, SHA256 fingerprint 등 마케팅팀이 MMP 콘솔에 입력할 값을 전달해요.</td></tr><tr><td>3. MMP에서 트래킹 링크 만들기</td><td>마케팅팀</td><td>전달받은 값을 MMP 콘솔에 등록하고, 딥링크를 적용한 트래킹 링크를 생성해요.</td></tr><tr><td>4. 트래킹 링크 테스트하기</td><td>마케팅팀</td><td>생성한 링크가 중간 브라우저 화면 없이 앱을 바로 여는지 확인해요.</td></tr></tbody></table>

개발자라면 앱에 딥링크 구현하기 섹션부터, 마케팅 담당자라면 MMP에서 트래킹 링크 만들기 섹션부터 확인하면 돼요.

## 앱에 딥링크 구현하기

개발팀이 진행하는 단계예요. 진행할 작업은 다음과 같아요.

* 앱 스킴 등록
* Universal Link 등록 (iOS)
* App Link 등록 (Android)
* 빌드 배포해서 반영
* 마케팅팀에 구현 값 전달

### 앱 스킴 (커스텀 URL 스킴) 구현하기

앱 스킴(커스텀 URL 스킴)은 앱이 설치된 상태에서 앱을 직접 실행할 수 있는 딥링크 방식이에요. 예를 들어 `brandapp://event/123` 형태예요.

iOS와 Android에서 동일한 앱 스킴을 사용하는 것을 권장해요.

앱 스킴은 아래 위치에서 확인할 수 있어요.

| 플랫폼     | 확인 위치               | 확인 항목                                           |
| ------- | ------------------- | ----------------------------------------------- |
| iOS     | Info.plist          | CFBundleURLTypes > CFBundleURLSchemes           |
| Android | AndroidManifest.xml | intent-filter 내 `<data android:scheme="..." />` |
| 공통      | 앱 내부 routing logic  | scheme URL 클릭 시 앱 실행 및 기대 화면 랜딩                 |

#### 1. 앱 스킴 등록하기

앱에서 사용할 고유한 스킴 값을 정해 파일 안에 등록해요. iOS와 Android에서 동일한 스킴과 소문자 사용을 권장하고, http/https는 사용할 수 없어요.

| 구성     | 예시 값     |
| ------ | -------- |
| scheme | brandapp |
| host   | event    |
| path   | /123     |

{% tabs %}
{% tab title="iOS" %}
Xcode TARGET > Info > URL Types에서 추가하거나 Info.plist에 직접 입력해요.

```xml
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLSchemes</key>
    <array><string>brandapp</string></array>
  </dict>
</array>
```

{% hint style="warning" %}
전체 URL(`brandapp://`)이 아니라 scheme 이름(`brandapp`)만 등록해요.
{% endhint %}
{% endtab %}

{% tab title="Android" %}
AndroidManifest.xml의 intent-filter에 등록해요.

```xml
<intent-filter>
  <action android:name="android.intent.action.VIEW" />
  <category android:name="android.intent.category.DEFAULT" />
  <category android:name="android.intent.category.BROWSABLE" />
  <data android:scheme="brandapp" />
</intent-filter>
```

{% hint style="warning" %}
`android:scheme`에는 http/https가 아닌 앱 고유 scheme 값을 입력해요. 외부에서 Activity를 열 수 있어야 하므로 `android:exported="true"`가 필요할 수 있어요.
{% endhint %}
{% endtab %}
{% endtabs %}

#### 2. 앱 내부 라우팅 구현하기 (들어온 URL 처리)

{% tabs %}
{% tab title="iOS" %}
```swift
.onOpenURL { url in
    // url == brandapp://event/123
    guard url.scheme == "brandapp" else { return }
    router.handle(host: url.host, path: url.path)
}
```

커스텀 앱 스킴은 `onOpenURL` 또는 `application(_:open:options:)`로 들어오고, Universal Link는 별도 진입점(`onContinueUserActivity` / `continueUserActivity`)에서 처리해요.
{% endtab %}

{% tab title="Android" %}
```kotlin
// onCreate / onNewIntent
val data: Uri? = intent?.data        // brandapp://event/123
if (data?.scheme == "brandapp") {
    router.handle(data.host, data.pathSegments)
}
```
{% endtab %}
{% endtabs %}

### Universal Link 등록하기 (iOS)

MMP tracking domain 기준으로 동작한다면 MMP가 AASA 파일을 생성하고 호스팅해요. 이 경우 개발자는 해당 도메인을 앱 설정에 반영만 하면 돼요.

자사 domain 기준으로 동작한다면 1\~3단계를 모두 완료해 주세요.

#### 1. Xcode에서 도메인 등록하기

**Xcode > Signing & Capabilities > Associated Domains**에 접속해서 도메인을 등록해요.

| 구성         | 예시 값                                                                        |
| ---------- | --------------------------------------------------------------------------- |
| 자사 도메인 예시  | applinks:go.brand.com                                                       |
| MMP 도메인 예시 | applinks:brand.onelink.me, applinks:brand.sng.link, applinks:brand.app.link |

{% hint style="warning" %}
Adjust 사용 시, 기존에 `xxx.adj.st`를 universal link domain으로 쓰고 있었다면 제거하지 말고, 브랜디드 도메인(`brand.go.link`)과 함께 Associated Domains에 유지해주세요. (Adjust 공식 권장)
{% endhint %}

#### 2. 서버에 AASA 파일 호스팅

`https://go.brand.com/.well-known/apple-app-site-association` 경로에 AASA 파일을 호스팅해요.

```json
{
  "applinks": {
    "apps": [],
    "details": [
      {
        "appID": "ABCDE12345.com.brand.app",
        "paths": ["/event/*", "/product/*"]
      }
    ]
  }
}
```

* HTTP 200으로 응답하고, JSON 형식이어야 하며, redirect 없이 접근 가능해야 해요.
* iOS는 AASA 파일을 캐싱하므로 수정 후 즉시 반영되지 않을 수 있어요. 개발 중에는 필요에 따라 `applinks:<domain>?mode=developer` 사용을 검토해주세요.

#### 3. 들어온 Universal Link 처리하기

```swift
.onContinueUserActivity(NSUserActivityTypeBrowsingWeb) { activity in
    guard let url = activity.webpageURL else { return }
    // url == https://go.brand.com/event/123
    router.handle(url)
}
```

### App Link 등록하기 (Android)

MMP tracking domain 기준으로 동작한다면 MMP가 AASA 파일을 생성하고 호스팅해요. 이 경우 개발자는 해당 도메인을 앱 설정에 반영만 하면 돼요.

자사 domain 기준으로 동작한다면 1\~2단계를 모두 완료해 주세요.

#### 1. AndroidManifest.xml에서 도메인 등록

intent-filter 코드에서 도메인을 등록해요.

```xml
<intent-filter android:autoVerify="true">
  <action android:name="android.intent.action.VIEW" />
  <category android:name="android.intent.category.DEFAULT" />
  <category android:name="android.intent.category.BROWSABLE" />
  <data
      android:scheme="https"
      android:host="go.brand.com"
      android:pathPrefix="/event" />
</intent-filter>
```

* `autoVerify="true"`를 설정해도 SHA256 fingerprint나 assetlinks.json이 맞지 않으면 검증이 실패할 수 있어요.
* path를 지정하지 않으면 해당 host의 더 넓은 범위 URL이 앱으로 열릴 수 있으니, 필요한 path 범위를 명확히 설정하는 것을 권장해요.

#### 2. 서버에 assetlinks.json 호스팅

`https://<domain>/.well-known/assetlinks.json` 경로에 파일을 호스팅해요.

```json
[
  {
    "relation": ["delegate_permission/common.handle_all_urls"],
    "target": {
      "namespace": "android_app",
      "package_name": "com.brand.app",
      "sha256_cert_fingerprints": ["AA:BB:CC:..."]
    }
  }
]
```

* HTTP 200으로 응답하고, JSON 형식이어야 하며, redirect 없이 접근 가능해야 해요.
* Google Play App Signing을 사용한다면 로컬 keystore가 아니라 Play Console에 표시된 App signing key certificate의 SHA256 fingerprint를 사용해요.
* debug, release, Play signing 등 필요한 fingerprint가 다를 수 있으므로 테스트 환경과 운영 환경을 구분해주세요.

### 마케팅팀에 구현 값 전달하기

구현과 빌드 배포를 마쳤다면, 마케팅팀이 MMP 콘솔에 입력할 아래 값을 전달해주세요.

<table data-search="false"><thead><tr><th>항목</th><th>예시</th></tr></thead><tbody><tr><td>앱 스킴</td><td>brandapp://</td></tr><tr><td>앱 스킴 테스트 URL</td><td>brandapp://home</td></tr><tr><td>iOS Bundle ID</td><td>com.brand.app</td></tr><tr><td>iOS Team ID 또는 App ID Prefix</td><td>ABCDE12345</td></tr><tr><td>Android Package Name</td><td>com.brand.app</td></tr><tr><td>Android SHA256 Certificate Fingerprint</td><td>AA:BB:CC:...</td></tr><tr><td>앱 내 랜딩 path 또는 deep link value</td><td>/event/123, event_detail, product_id, /home, /</td></tr></tbody></table>

## MMP에서 트래킹 링크 만들기

마케팅팀이 진행하는 단계예요. 시작하기 전에 아래 두 가지를 확인해주세요.

* 개발팀의 딥링크 구현과 빌드 배포가 모두 완료됐어요.
* 위 표의 값을 개발팀에게 모두 전달받았어요.

전달받은 값은 MMP 콘솔에 그대로 복사해 붙여 넣으면 돼요. 값의 의미를 이해할 필요는 없고, 형식이 맞는지만 확인해주세요.

사용하는 MMP의 탭을 선택해 안내를 따라 주세요.

{% tabs %}
{% tab title="AppsFlyer" %}
공식 가이드는 [원링크 템플릿 만들기](https://support.appsflyer.com/hc/ko/articles/207032246-%EC%9B%90%EB%A7%81%ED%81%AC-%ED%85%9C%ED%94%8C%EB%A6%BF-%EB%A7%8C%EB%93%A4%EA%B8%B0)를 참고해주세요.

**1. 콘솔에서 딥링크 정보 반영**

**AppsFlyer > Engage** 또는 **Experiences & Deep Linking > OneLink management**에 접속한 뒤, 원링크 템플릿 편집 화면을 열어요. 개발팀에게 전달받은 앱 스킴, Team ID/App ID Prefix, Bundle ID, SHA256 fingerprint를 모두 반영하고 저장해요.

**2. 원링크 생성**

원링크 커스텀 링크를 생성해요. 이때 deep link destination 또는 deep\_link\_value 값에 전달받은 딥링크 값을 파라미터 값으로 설정해요.

링크를 구성할 때 `pid`, `advertising_id`, `click_id`, `af_c_id`, `af_ad_id` 파라미터는 반드시 포함해야 해요. 그 외 `af_siteid`, `af_adset`, `af_ad`, `c` 파라미터는 포함을 권장해요.
{% endtab %}

{% tab title="Adjust" %}
공식 가이드는 [Set up universal links](https://help.adjust.com/en/article/set-up-universal-links)를 참고해주세요.

**1. 콘솔에서 딥링크 정보 반영**

**Adjust > AppView > App 선택 > Platforms**에 접속한 뒤, 개발팀에게 전달받은 항목을 모두 반영하고 저장해요.

1. AppView에서 대상 앱 선택
2. Platforms 탭 진입
3. iOS Universal Linking 활성화
4. iOS Bundle ID, App ID Prefix, 앱 스킴 입력
5. Android App Links 활성화
6. SHA256 fingerprint 및 앱 스킴 입력

**2. 트래킹 링크 생성**

Campaign Lab 탭에 접속해 트래킹 링크를 생성해요.

{% hint style="warning" %}
기존에 `xxx.adj.st` 도메인을 쓰고 있었다면 제거하지 말고, 자사 브랜디드 도메인(`brand.go.link`)과 함께 유지하도록 개발팀에 전달해주세요. (Adjust 공식 권장)
{% endhint %}
{% endtab %}

{% tab title="Airbridge" %}
공식 가이드는 [Retargeting with deep links](https://help.airbridge.io/en/guides/retargeting-with-deep-links)를 참고해주세요.

**1. 콘솔에서 딥링크 정보 반영**

**Airbridge > Tracking Link > Deep Links**에 접속한 뒤, 개발팀에게 전달받은 항목을 반영하고 저장해요.

1. Tracking Link > Deep Links 이동
2. iOS / Android URL Scheme 입력
3. iOS App ID 입력
4. Android Package Name 및 SHA256 입력

**2. 트래킹 링크 생성**

Link Generation 탭에서 링크를 생성해요. 이때 **Redirection > Destination**에서 App (Deep Link)을 선택하고, 전달받은 Deep Link(예: `brandapp://event/123`)를 입력해 트래킹 링크를 생성해요.

**3. Host 수동 변경 (중요)**

Airbridge는 생성한 트래킹 링크의 host를 수정한 링크로 최종 전달해야 해요. `abr.ge` 호스트를 `brandname.abr.ge` 호스트로 변경해주세요.

* 트래킹 링크 원본 `https://abr.ge/@brandname/~~`
* 수정한 트래킹 링크 `https://brandname.abr.ge/@brandname/~~`
{% endtab %}

{% tab title="Branch" %}
공식 가이드는 [Link routing rules](https://help.branch.io/docs/link-routing-rules-new)를 참고해주세요.

**1. 콘솔에서 딥링크 정보 반영**

**Branch > Configuration > Link Controls > Link Routing Rules**에 접속한 뒤, 개발팀에게 전달받은 항목을 반영하고 저장해요.

1. **Link Controls > Link Routing Rules** 이동
2. Android URI Scheme 입력
3. iOS URI Scheme 입력
4. iOS Enable Universal Links 활성화
5. Bundle Identifier, Apple App Prefix 입력
6. Android Enable App Links 활성화
7. Android Package Name, SHA256 입력

**2. 트래킹 링크 생성**

1. App Links / Short Links 생성
2. deep link data 또는 `$deeplink_path` 설정
3. 링크 생성 완료
{% endtab %}

{% tab title="Singular" %}
공식 가이드는 [Singular Links Prerequisites](https://support.singular.net/hc/en-us/articles/360031371451)를 참고해주세요.

**1. 콘솔에서 딥링크 정보 반영**

**Singular > Settings > Apps** 또는 Apps Configuration에 접속한 뒤, 개발팀에게 전달받은 항목을 반영하고 저장해요.

1. Settings > Apps에서 대상 앱 선택
2. 앱 스킴 입력
3. Link Management에서 Singular link subdomain 생성 (예: `brand.sng.link`)
4. iOS Team ID 입력
5. Android SHA256 fingerprint 입력

**2. 트래킹 링크 생성**

Build Tracking Link / Create Link로 이동해 딥링크를 반영한 트래킹 링크를 생성해요.

1. Build Tracking Link / Create Link 이동
2. deep link destination 설정 — 공통 `_dl` / iOS 전용 `_ios_dl` / Android 전용 `_android_dl`
3. 앱 미설치 fallback 설정 — iOS `_ios_redirect` / Android `_android_redirect`
4. 링크 생성 완료
{% endtab %}

{% tab title="DFINERY" %}
공식 가이드는 [DFINERY 도움말](https://help.dfinery.io)의 Ad Landing Settings, Tracking Link 발급 문서를 참고해주세요.

**1. 콘솔에서 딥링크 정보 반영**

**DFINERY > Attribution > Ad Landing Settings**에 접속한 뒤, 개발팀에게 전달받은 항목을 반영하고 저장해요.

1. Attribution > Ad Landing Settings 이동
2. Android Default URL 입력
3. Android Deep Link Scheme 입력 (예: `brandapp`)
4. Package Name 입력
5. iOS Default URL 입력
6. iOS Deep Link Scheme 입력 (예: `brandapp`)
7. App Store ID 입력
8. iOS Universal Links 영역에 Team ID + Bundle ID 입력
9. Android App Links 영역에 SHA256 fingerprint 입력

{% hint style="info" %}
`Deep Link Scheme`에는 `brandapp://event/123` 전체가 아니라 스킴 값(`brandapp`)만 입력해요.
{% endhint %}

**2. 트래킹 링크 생성**

**Attribution > Ad Campaign > Tracking Link**로 이동해 딥링크를 반영한 트래킹 링크를 생성해요.

1. Ad Campaign > Tracking Link에서 Download + Deeplink 선택
2. 설치 유저용 Deep Linking 옵션 On
3. Static 또는 Dynamic path 설정
4. tracking link 발급 후 테스트
5. 링크 생성 완료
{% endtab %}
{% endtabs %}

## 트래킹 링크 테스트하기

생성한 트래킹 링크는 아래 순서로 테스트해요.

1. 테스트 기기에 광고주 앱을 설치해요.
2. 테스트 링크를 메모장 앱 등에 붙여 넣어요. 카카오톡 등 일부 앱에서는 Universal Link가 정상 동작하지 않을 수 있으니, 외부 브라우저에서 해당 링크가 열릴 수 있도록 준비해주세요.
3. 링크를 눌러요.
4. 앱이 중간 브라우저 화면 없이 바로 열리는지 확인해요.

{% hint style="info" %}
Airbridge의 경우, 생성한 트래킹 링크의 host를 수정한 링크로 클릭해야 정상 작동을 확인할 수 있어요.\
· 링크 원본 `https://abr.ge/@brandname/~~`\
· 테스트 링크 `https://brandname.abr.ge/@brandname/~~`
{% endhint %}

테스트에 실패했다면 아래 내용을 확인해주세요.

| 증상              | 확인할 내용                                                |
| --------------- | ----------------------------------------------------- |
| 브라우저가 먼저 열려요    | Universal Link가 아닌 일반 URL이나 fallback으로 동작하고 있을 수 있어요. |
| 앱이 열리지 않아요      | 해당 domain이 앱의 Associated Domains에 등록되어 있는지 확인해주세요.    |
| 특정 링크만 실패해요     | 해당 domain의 AASA 설정 또는 MMP domain 연결 여부를 확인해주세요.       |
| 카카오톡에서는 실패해요    | 메모장, Mail, Safari 검색 결과 등 다른 앱에서 다시 테스트해주세요.          |
| 설정을 바꾼 뒤에도 실패해요 | 앱을 삭제하고 다시 설치한 뒤 테스트해주세요.                             |

정상 작동을 확인했다면 앱 스킴과 최종 트래킹 링크를 파라미터가 보이는 원본(롱 링크)으로 준비해주세요. 소재를 등록할 때 함께 제출해요. 제출 규칙은 [앱 설치 소재 가이드](creative.md)에서 안내하고 있어요.
