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
  anchors:
    visible: true
---

# URL 설정 가이드

앱 설치 유도하기 광고에는 앱 스킴을 설정한 MMP 트래킹 링크 1개가 필요해요. 이 가이드는 앱을 설치한 유저는 앱으로, 설치하지 않은 유저는 스토어로 보내는 트래킹 링크를 만들고 테스트하는 방법을 순서대로 안내해요.

{% hint style="info" %}
**앱 스킴 적용은 필수, 유니버설 링크(iOS)·앱 링크(Android) 적용은 권장이에요.**

토스애즈의 앱 실행 요건은 앱 스킴을 설정한 트래킹 링크를 준비하는 거예요. 광고 성과 측정에 필요한 필수 항목도 포함해야 해요. 사용하는 MMP의 기능에 따라 앱 식별 정보나 도메인 연결 등 추가 사전 설정이 필요할 수 있어요. 유니버설 링크(iOS)·앱 링크(Android) 설정 방법은 이 페이지 맨 아래 '(권장) 유니버설 링크·앱 링크 설정하기'에서 안내해요.
{% endhint %}

{% hint style="info" %}
* 앱 설치 유도하기 광고는 소재 검수 과정에서 트래킹 링크와 앱 스킴이 정상적으로 동작하는지 함께 확인하기 때문에, 검수 시간이 더 소요될 수 있어요.\
  검수 시 앱 미설치 상태에서 스토어로 바로 이동하지 않거나, 기설치 상태에서 앱이 바로 열리지 않는 등 링크나 앱 스킴이 정상 동작하지 않으면 소재 심사 승인이 불가해요.\
  라이브 전에 아래 [트래킹 링크 테스트하기](link-guide.md#undefined-6)를 참고해 정상 동작 여부를 꼭 확인해 주세요.
* 소재 규격과 링크 제출 규칙은 [앱 설치 소재 가이드](creative.md)에서 안내하고 있어요.
{% endhint %}

{% hint style="info" %}
소재 규격과 링크 제출 규칙은 [앱 설치 유도하기 소재 가이드](creative.md)에서 안내하고 있어요.
{% endhint %}



## 이 가이드에서 쓰는 용어 <a href="#terms" id="terms"></a>

이 가이드에서는 링크를 눌렀을 때 앱 안에서 보여 줄 화면을 '앱에서 열 화면'이라고 불러요.

앱 스킴 이름, 앱 실행 주소, 딥링크 주소, 화면 경로가 각각 무엇인지는 아래 표를 참고해 주세요.

| 용어      | 뜻                      | iOS 예시                  | Android 예시                  |
| ------- | ---------------------- | ----------------------- | --------------------------- |
| 앱 스킴 이름 | 앱에 등록한 스킴 이름           | `sampleios`             | `sampleandroid`             |
| 앱 실행 주소 | 앱을 실행만 하는 주소           | `sampleios://`          | `sampleandroid://`          |
| 딥링크 주소  | 앱에서 열 화면까지 가리키는 전체 주소  | `sampleios://event/123` | `sampleandroid://event/123` |
| 화면 경로   | 딥링크 주소에서 앱 실행 주소를 뺀 부분 | `event/123`             | `event/123`                 |

예시 값은 입력 형식을 보여 주는 값이에요. 개발팀이 전달한 실제 값을 써 주세요.



## 한눈에 보기 <a href="#overview" id="overview"></a>

트래킹 링크는 개발팀과 마케팅팀이 아래 순서로 함께 준비해요.

| 단계                  | 담당        | 할 일                                                        |
| ------------------- | --------- | ---------------------------------------------------------- |
| 1. 앱에 앱 스킴 구현하기     | 개발팀       | 앱 스킴을 등록하고, 링크를 받으면 앱에서 열 화면으로 이동하도록 구현한 뒤 앱을 배포해요.        |
| 2. 설정값 전달하기         | 개발팀       | 앱 스킴 이름, 앱 실행 주소, OS별 딥링크 주소, 앱 식별 정보, 스토어 주소를 마케팅팀에 전달해요. |
| 3. MMP에서 트래킹 링크 만들기 | 마케팅팀      | 사용하는 MMP에 앱 스킴, 앱에서 열 화면, 스토어 주소를 설정하고 클릭용 트래킹 링크를 만들어요.   |
| 4. 트래킹 링크 테스트하기     | 마케팅팀과 개발팀 | 앱을 설치한 기기와 설치하지 않은 기기에서 각각 확인해요.                           |

개발 담당자는 1단계부터, 마케팅 담당자는 2단계에서 설정값을 받은 뒤 3단계부터 진행해요. 한쪽 OS만 광고한다면 그 OS를 기준으로 준비하고 테스트해요.



## 1. 앱에 앱 스킴 구현하기 <a href="#step1-app-scheme" id="step1-app-scheme"></a>

개발팀이 진행하는 단계예요. 유저가 트래킹 링크를 누르면 휴대폰은 링크에 연결된 딥링크 주소(예: iOS `sampleios://event/123`, Android `sampleandroid://event/123`)로 광고주 앱을 실행하고, 그 주소를 앱에 넘겨줘요. 앱이 이 주소를 받아 해당 화면을 열 수 있도록 아래 세 가지를 구현한 뒤 앱을 배포해 주세요.

1. **앱 스킴 등록**: 앱 설정에 앱 스킴 이름(예: iOS `sampleios`, Android `sampleandroid`)을 등록해요. 두 OS의 앱 스킴 이름은 서로 달라도 돼요.
2. **주소에 맞는 화면 열기**: 넘겨받은 주소를 읽어 해당 화면을 열어요. 앱이 꺼져 있다가 링크로 실행된 경우와 이미 켜져 있던 경우를 모두 처리해요.
3. **MMP SDK의 딥링크 처리 연결**: 사용하는 SDK의 공식 가이드에 따라 URL 수신과 딥링크 콜백을 연결해요. 광고 유입 측정과 화면 이동에 필요한 데이터를 앱이 처리하도록 구현해요.

{% tabs %}
{% tab title="iOS" %}
Xcode의 **Target → Info → URL Types** 또는 `Info.plist`에 앱 스킴 이름을 등록해요.

```xml
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLSchemes</key>
    <array><string>sampleios</string></array>
  </dict>
</array>
```

앱 구조에 맞는 URL 수신 지점에서 허용한 host·path를 확인하고, 화면 이동과 MMP SDK 처리를 연결해요. SwiftUI 앱은 `onOpenURL`에서 링크 주소를 받을 수 있어요. 자세한 내용은 [Apple 공식 가이드](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app)를 참고해 주세요.
{% endtab %}

{% tab title="Android" %}
링크를 받을 Activity에 앱 스킴용 `intent-filter`를 등록해요.

```xml
<activity android:name=".MainActivity" android:exported="true">
  <intent-filter>
    <action android:name="android.intent.action.VIEW" />
    <category android:name="android.intent.category.DEFAULT" />
    <category android:name="android.intent.category.BROWSABLE" />
    <data android:scheme="sampleandroid" />
  </intent-filter>
</activity>
```

앱 구조와 Activity 실행 방식에 맞춰 `onCreate`와 `onNewIntent`에서 전달받은 Intent의 URL을 처리해요. 처음 실행될 때와 실행 중 새 링크를 받을 때를 모두 확인해 주세요. 예를 들어 `sampleandroid://event/123`은 Scheme이 `sampleandroid`, host가 `event`, path가 `/123`이에요. 허용한 주소인지 확인한 뒤 앱에서 열 화면으로 연결하고 MMP SDK의 딥링크 처리를 적용해요. 자세한 내용은 [Android 공식 가이드](https://developer.android.com/training/app-links/deep-linking)를 참고해 주세요.
{% endtab %}
{% endtabs %}



## 2. 설정값 전달하기 <a href="#step2-share-values" id="step2-share-values"></a>

개발팀은 배포한 앱 기준으로 아래 값을 마케팅팀에 전달해요. 광고를 누른 유저를 앱의 특정 화면(예: 이벤트 화면)으로 보내려면 OS별 딥링크 주소까지 준비해요. 특정 화면 없이 앱을 열기만 하면 된다면 앱 실행 주소(예: `sampleios://`)만 준비하면 돼요.

| 항목                          | 예시                                                               | 확인할 내용                                         |
| --------------------------- | ---------------------------------------------------------------- | ---------------------------------------------- |
| 앱 스킴 이름                     | iOS `sampleios`, Android `sampleandroid`                         | 앱에 등록한 이름이에요. 두 OS가 달라도 돼요.                    |
| 앱 실행 주소                     | iOS `sampleios://`, Android `sampleandroid://`                   | 앱을 실행만 하는 주소예요.                                |
| OS별 딥링크 주소                  | iOS `sampleios://event/123`, Android `sampleandroid://event/123` | 앱에서 열 화면까지 가리키는 주소예요. 앱이 실제로 처리하는 화면 경로를 포함해요. |
| Android Package Name        | `com.brand.app`                                                  | 광고 대상 앱과 일치해야 해요.                              |
| iOS Bundle ID와 App Store ID | 앱별 실제 값                                                          | MMP의 입력 항목에 맞춰 준비해요.                           |
| 스토어 주소                      | Google Play·App Store URL                                        | 앱을 설치하지 않은 유저가 이동할 곳이에요.                       |
| 적용된 앱 버전                    | 배포 버전                                                            | 테스트할 앱에 구현이 반영돼 있어야 해요.                        |

MMP마다 콘솔에 입력하는 값이 달라요. 앱 스킴 이름(예: `sampleios`)을 입력하는 곳도 있고, 앱 실행 주소(예: `sampleios://`)나 딥링크 주소(예: `sampleios://event/123`)를 입력하는 곳도 있어요. 그래서 개발팀은 표의 앱 스킴 이름, 앱 실행 주소, OS별 딥링크 주소를 모두 전달해 주세요. 어떤 값을 어디에 입력하는지는 3단계의 MMP 탭에서 안내해요.



## 3. MMP에서 트래킹 링크 만들기 <a href="#step3-create-link" id="step3-create-link"></a>

마케팅팀이 진행하는 단계예요. 사용하는 MMP 콘솔에서 토스 광고에 쓸 클릭용 트래킹 링크를 만들어요. 이 링크를 누르면 앱을 설치한 유저는 앱에서 열 화면으로, 설치하지 않은 유저는 스토어로 이동해요.

{% hint style="info" %}
이 단계에서는 유저가 광고를 눌렀을 때 거쳐 가는 **클릭용 링크**를 만들어요. MMP에 따라 광고 노출을 기록하는 노출용 링크가 함께 만들어지기도 하지만, 4단계 테스트와 토스 소재 등록에는 클릭용 링크를 써요.
{% endhint %}

### 시작하기 전에 확인하기 <a href="#before-you-start" id="before-you-start"></a>

아래 두 가지가 끝났는지 먼저 확인해요.

* 개발팀이 1단계의 앱 스킴 구현과 앱 배포를 마쳤어요.
* 2단계의 설정값을 개발팀에게 모두 받았어요.

링크에 필수·권장 항목을 넣어도 MMP의 토스 파트너 연동과 앱의 SDK·이벤트 설정이 끝나지 않으면 광고 성과가 측정되지 않아요. 이 설정은 [MMP 연동 가이드](../../tracking/mat/)를 따라 완료해요.

### 링크 만드는 방법 고르기 <a href="#choose-method" id="choose-method"></a>

어느 방법으로 링크를 만들든 앱 스킴은 필수로 설정해요. 이미 유니버설 링크나 앱 링크를 사용하고 있다면 그 설정도 지우지 말고 함께 유지해요. 토스용 링크는 아래 두 방법 중 하나로 만들어요.

#### 방법 1. 토스용 링크 자동으로 만들기(권장) <a href="#method1-auto" id="method1-auto"></a>

MMP 콘솔에서 토스를 고르면 토스용 링크가 자동으로 만들어지는 방법이에요. 자동 생성이 필수 요건은 아니지만 이 방법을 강력히 권장해요.

1. MMP 콘솔에서 토스(Toss)를 광고 파트너 또는 매체로 골라요.
2. MMP가 제공하는 클릭용 트래킹 링크를 자동으로 만들어요.
3. 만든 최종 링크에 2단계에서 받은 아래 값이 적용됐는지 확인해요.
   * 앱 실행 주소 (예: `sampleios://`)
   * OS별 딥링크 주소 (예: iOS `sampleios://event/123`, Android `sampleandroid://event/123`)
   * 앱을 설치하지 않은 유저가 갈 스토어 주소

#### 방법 2. Custom link나 수동 설정으로 직접 만들기 <a href="#method2-manual" id="method2-manual"></a>

자동 생성 기능을 쓸 수 없거나 필요한 설정을 반영하기 어려우면, MMP가 지원하는 Custom link나 수동 설정 방식으로 직접 만들 수 있어요.

1. 토스 매체 식별값과 기존 캠페인 파라미터가 들어 있는 기본 링크를 준비해요.
2. 아래 MMP별 탭의 표를 보고 필수 항목과 값을 넣어요. 권장 항목도 함께 넣어요. 광고 ID 항목은 OS와 MMP가 지원하는 방식에 맞춰 넣어요.
3. OS별 딥링크 주소를 MMP의 입력란이나 파라미터에 설정해요. URL 안에 주소를 넣을 때는 그 값에 필요한 인코딩을 적용해요.
4. 앱을 설치하지 않은 유저가 갈 스토어 주소를 확인하고, 최종 클릭용 링크를 복사해요.

{% hint style="info" %}
**직접 만들어도 매체는 토스로 유지해요.**

Custom link의 의미와 지원 범위는 MMP마다 달라요. 매체를 `newsletter` 같은 자사 채널이나 임의의 Custom Source로 바꾸지 말고, 토스 매체 식별값과 필수 측정값을 유지할 수 있는 방식으로 만들어 주세요.
{% endhint %}

### 방법 1·2 공통 <a href="#method-common" id="method-common"></a>

**매크로와 파라미터를 넣을 때 주의할 점**

* **매크로는 그대로 둬요.** `{TOSS_TK_CLICK_ID}`처럼 중괄호로 감싼 값은 광고가 노출되거나 클릭될 때 실제 값으로 바뀌는 자리예요. 테스트 ID 같은 실제 값으로 바꾸지 말고, 대소문자와 중괄호도 가이드 그대로 유지해요.
* **같은 파라미터를 두 번 넣지 않아요.** 이미 링크에 있는 파라미터라면 기존 값이 맞는지 확인해요.

**필수·권장 항목 확인하기**

링크를 만들었으면 최종 링크에 필요한 값이 빠짐없이 들어 있는지 확인해요. 자동으로 만든 링크와 직접 만든 링크 모두 확인해요.

토스용 링크에는 두 종류의 값이 모두 있어야 해요. 하나는 앱을 열고 화면을 정하는 목적지 값이고, 다른 하나는 광고 성과를 재는 측정값이에요. 둘은 역할이 달라서 하나만 있으면 안 돼요.

1. [MMP로 광고 성과 측정하기](../../tracking/mat/)에서 사용하는 MMP의 **전환 추적 링크 필수·권장 항목**을 확인해요. 같은 내용을 아래 MMP별 탭의 **'③ 필수·권장 항목 확인하기'** 표에도 옮겨 두었어요.
2. 최종 링크를 이 항목과 대조해서 빠진 값이 없는지 확인해요. **필수 항목은 모두 넣고, 권장 항목도 함께 넣어 주세요.**

링크에 넣는 필수·권장 항목은 이벤트 포스트백(MMP가 설치·구매 같은 전환 결과를 토스애즈로 보내는 데이터)에 넣는 파라미터와 다르니 구분해 주세요.

### MMP별 트래킹 링크 만들기 <a href="#mmp-tracking-link" id="mmp-tracking-link"></a>

사용하는 MMP 탭을 골라 ①\~③ 순서대로 진행해요.

* ① 링크를 만들기 전에 콘솔에 앱 정보를 등록해요.
* ② 토스용 클릭 링크를 만들어요.
* ③ 최종 링크에 필수·권장 항목이 모두 있는지 확인해요.

{% hint style="info" %}
탭의 이미지는 참고 화면이에요. 예시 값을 그대로 복사하지 말고 2단계에서 받은 실제 값을 입력해요. 메뉴 이름은 영문 기준이라 콘솔 언어나 업데이트에 따라 다르게 보일 수 있어요.
{% endhint %}

{% tabs %}
{% tab title="AppsFlyer" %}
**① 링크 만들기 전 설정하기**

1.  **Engage → OneLink management** 위쪽에서 **OneLink template**을 골라요.

    템플릿을 고칠 때는 템플릿 영역 오른쪽의 **⋮** 메뉴를 쓰고, 이 템플릿에 Custom link를 추가할 때는 **Active links → Add link**를 눌러요.<br>

    <figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FU0J21VYcwODwlPTE2wy8%2Fimage.png?alt=media&#x26;token=73454363-434f-45c9-b06a-5fe68c192de3" alt=""><figcaption><p>AppsFlyer 원링크 관리(OneLink management) 화면 (출처: AppsFlyer 콘솔 캡처)</p></figcaption></figure>
2.  템플릿이 없다면 **Add OneLink template**에서 새로 만들어요. 이름, Subdomain, iOS·Android 앱, 앱을 설치하지 않은 유저가 갈 스토어 주소를 설정해요.

    템플릿 이름·Subdomain·iOS/Android 앱 선택 화면이에요. 현재 콘솔과 UI가 다를 수 있어요. [원본 보기](https://support.appsflyer.com/hc/article_attachments/360009665478)<br>

    <figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FhxuOi6wRgP6sJPVmSYif%2Fimage.png?alt=media&#x26;token=f0b79dfe-8921-4690-8002-33554cf61f31" alt=""><figcaption><p>AppsFlyer OneLink 템플릿 추가 화면 (출처: <a href="https://support.appsflyer.com/hc/en-us/articles/207032246-Create-a-OneLink-template">AppsFlyer - Create a OneLink template</a>)</p></figcaption></figure>
3. **⋮ → Edit OneLink template → When app is installed**로 이동해요.
4. 화면 아래쪽 **Android and iOS fallback**에서 **Add URI scheme to launch the app → Launch the app using URI scheme**을 골라요.
5.  앱에 구현된 앱 실행 주소(예: `sampleios://`)를 입력하고 **Save changes → Update OneLink template**으로 저장해요.

    앱 스킴은 하단 Android and iOS fallback에서 설정해요. 상단 유니버설 링크·앱 링크 설정은 맨 아래 '(권장) 유니버설 링크·앱 링크 설정하기'에서 안내해요. [원본 보기](https://support.appsflyer.com/hc/article_attachments/18363965490833)\
    <br>

    <figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FBIUO6k6LfOnv2WDGx0aH%2Fimage.png?alt=media&#x26;token=204d678a-bf8c-4536-b42d-442e0b7a02a5" alt=""><figcaption><p>AppsFlyer 앱 설치 상태의 링크 동작(When app is installed) 설정 화면 (출처: <a href="https://support.appsflyer.com/hc/en-us/articles/207032246-Create-a-OneLink-template">AppsFlyer - Create a OneLink template</a>)</p></figcaption></figure>

{% hint style="info" %}
한 템플릿에 iOS와 Android를 함께 연결하면 두 앱에 같은 앱 스킴 이름이 등록돼 있어야 해요. 한쪽 OS만 쓴다면 그 앱에 등록된 앱 스킴 이름으로 앱 실행 주소를 입력해요. 자세한 내용은 [공식 템플릿 가이드](https://support.appsflyer.com/hc/en-us/articles/207032246-Create-a-OneLink-template)를 참고해 주세요.
{% endhint %}

토스 광고용 링크에 넣을 값(토스 매체 식별값, 필수·권장 항목)과 토스용 링크를 자동으로 만드는 메뉴 위치는 아래 ②에서 안내해요.<br>

**② 링크 만들기**

**자동 생성 (권장)**

* 토스용 자동 생성 링크를 먼저 사용해요. **Active Integrations → Toss → Attribution link**에서 Click attribution link를 확인한 뒤, ①에서 설정한 OneLink 템플릿과 앱 실행 목적지가 최종 링크에 적용됐는지 확인해요. 최종 링크에 `af_dp`(앱 실행 주소)가 있는지도 확인해요. [토스애즈 AppsFlyer 연동·링크 가이드](../../tracking/mat/appsflyer.md)

**수동 설정**

* 자동 생성이 어려워 Custom link로 직접 만들 때는 **Engage → OneLink management → 해당 템플릿 → Add link**에서 아래처럼 설정해요. 이미 채워진 값은 그대로 써도 돼요. 단, 토스용 매체값과 필수 매크로가 맞는지는 확인해요.

| 순서 | 메뉴                                    | 설정할 내용                                                                                             |
| -- | ------------------------------------- | -------------------------------------------------------------------------------------------------- |
| 1  | 용도·Media source                       | 광고 목적에 맞는 링크를 선택하고, 최종 링크에 토스 매체 식별값 `pid=tossa3u_int`가 유지되도록 설정해요.                                |
| 2  | General settings                      | 캠페인 정보를 설정해요. 토스용 캠페인 매크로를 임의의 이름으로 덮어쓰지 않아요. 기존 유저의 재참여 성과도 측정하려면 앱과 링크의 Retargeting 설정을 함께 확인해요. |
| 3  | Deep linking and redirection          | 특정 화면을 연결할 때 개발팀과 정한 화면 식별값을 Deep link value에 입력해요. 앱 실행 주소와 미설치 유저용 스토어 주소도 확인해요.                 |
| 4  | Additional parameters → Add parameter | 아래 필수·권장 측정값과 필요한 딥링크 데이터를 설정해요. 이미 있는 값은 다시 넣지 않아요.                                               |
| 5  | Generate link → Actions → Get URL     | 최종 클릭용 URL을 복사해요. 설정값을 확인할 수 있는 원래의 긴 주소로 준비해요.                                                    |

* 공식 문서의 `newsletter` 같은 자사 채널 값은 입력 형식을 보여 주는 예시예요. 실제 토스용 링크에는 토스 매체·캠페인 값을 써요. 콘솔에서 토스용 매체값을 유지할 수 없다면 그 방식은 쓰지 말고 Toss 파트너 링크 설정을 확인해 주세요. [공식 링크 생성 가이드](https://support.appsflyer.com/hc/en-us/articles/208874366-Create-deep-linking-and-redirection-links-for-your-campaigns-with-OneLink)
*   **앱 실행 주소와 화면 식별값은 따로 넣어요**

    앱 실행 주소와 화면 식별값은 역할이 달라요. 화면 식별값은 앱에서 열 화면을 가리키도록 개발팀과 정한 값이에요. `deep_link_value`에는 앱이 읽도록 구현한 형식 그대로 넣어요. 보통은 화면 식별값을 넣지만, 딥링크 주소 전체를 읽도록 만든 앱도 있으니 개발팀과 정한 값을 써요. 특정 화면으로 이동하려면 SDK와 앱의 화면 이동 처리가 구현돼 있어야 해요. [공식 파라미터 가이드](https://support.appsflyer.com/hc/en-us/articles/207447163-About-link-structure-and-parameters)

| 파라미터               | 입력할 값                                                                                                         |
| ------------------ | ------------------------------------------------------------------------------------------------------------- |
| `af_dp`            | <p>앱 실행 주소. </p><ul><li>iOS <code>sampleios://</code></li><li>Android <code>sampleandroid://</code></li></ul> |
| `deep_link_value`  | 개발팀과 정한 화면 식별값                                                                                                |
| `deep_link_sub1` 등 | 앱이 처리하도록 구현한 추가 딥링크 데이터                                                                                       |

* 토스 광고에 제출하는 링크에는 `af_force_deeplink`를 넣지 않아요. 이 파라미터를 넣으면 앱을 설치하지 않은 유저에게도 앱 실행을 강제로 시도해서 오류 알림이 뜰 수 있어요. 앱이 열리지 않으면 이 파라미터를 추가하지 말고 앱 스킴, SDK, OneLink 템플릿의 목적지(앱 실행 주소·스토어 주소) 설정을 확인해 주세요. 테스트는 토스 앱 5.282.0 이상(iOS·Android)에서 해 주세요.



**③ 필수·권장 항목 확인하기**

자동으로 만든 링크와 직접 만든 링크 모두 아래 항목이 들어 있는지 확인해요.&#x20;

| 구분 | 항목                      | 값                    | 설명              |
| -- | ----------------------- | -------------------- | --------------- |
| 필수 | `pid`                   | `tossa3u_int`        | 토스 매체 식별값       |
| 필수 | `clickid`               | `{TOSS_TK_CLICK_ID}` | 클릭 ID           |
| 필수 | `advertising_id / idfa` | `{USER_ADID}`        | OS에 맞는 광고 ID 항목 |
| 필수 | `af_c_id`               | `{TOSS_CID}`         | 캠페인 ID          |
| 권장 | `af_ad_id`              | `{TOSS_CREATIVE_ID}` | 소재 ID           |
| 권장 | `af_siteid`             | `{SITE_ID}`          | 매체·지면 구분        |
| 권장 | `af_adset`              | `{ADGROUP_NAME}`     | 광고 그룹명          |
| 권장 | `af_ad`                 | `{CREATIVE_NAME}`    | 소재명             |
| 권장 | `c`                     | `{CAMPAIGN_NAME}`    | 캠페인명            |
{% endtab %}

{% tab title="Adjust" %}
**① 링크 만들기 전 설정하기**

배포한 앱에 구현된 OS별 앱 스킴 이름과 딥링크 주소를 개발팀에게 받아요. 앱 스킴은 Adjust에서 새로 만드는 값이 아니에요.

App scheme 입력란은 **AppView → All apps → 대상 앱 → Platforms**의 iOS·Android 화면에 있어요. 여기에는 앱에 등록된 앱 스킴 이름(예: iOS `sampleios`, Android `sampleandroid`)만 입력해요. 링크의 `deep_link`에 넣는 딥링크 주소(예: `sampleios://event/123`)와는 다른 값이에요. [공식 App scheme 설정](https://help.adjust.com/en/article/set-up-universal-links)

이 플랫폼 화면은 유니버설 링크·앱 링크 기능과 연결돼 있어서, 이 기능을 켤 때는 App ID prefix, 인증서, 도메인 연결 같은 플랫폼별 사전 요건도 갖춰야 해요.

아래는 App scheme 입력 위치를 보여 주는 참고 화면이에요. 사용하는 기능에 필요한 플랫폼별 앱 정보와 사전 설정을 함께 확인해요. [공식 플랫폼 설정](https://help.adjust.com/en/article/platforms-ios-android-amazon-microsoft)

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FqULD2N7GF8S2nXoiRqR9%2Fimage.png?alt=media&#x26;token=5b0fd466-c150-4048-8f6b-bb496b96821b" alt=""><figcaption><p>Adjust iOS 플랫폼 설정 화면 (출처: <a href="https://help.adjust.com/en/article/platforms-ios-android-amazon-microsoft">Adjust - Connect your platform</a>)</p></figcaption></figure>

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FcZowzaKySpp8gS1UD6Ry%2Fimage.png?alt=media&#x26;token=82f5e3f1-1f94-47df-ad5e-e6c04a35e3b0" alt=""><figcaption><p>Adjust Android 플랫폼 설정 화면 (출처: <a href="https://help.adjust.com/en/article/platforms-ios-android-amazon-microsoft">Adjust - Connect your platform</a>)</p></figcaption></figure>

{% hint style="info" %}
앱 스킴으로 여는 링크는 아래 ②처럼 기본 트래킹 링크에 `deep_link`를 붙여 만들어요. 유니버설 링크·앱 링크를 켜고 Deep link generator를 함께 쓰려면 맨 아래 '(권장) 유니버설 링크·앱 링크 설정하기'의 Adjust 탭을 따라 주세요.
{% endhint %}

\
**② 링크 만들기**

**1) 토스용 기본 링크 만들기**

* **자동 생성 (권장)**: **Campaign Lab → Partners**에서 Toss 연동을 확인하고, 토스용 기본 클릭 링크를 먼저 만들어요. [토스애즈 Adjust 연동 가이드](../../tracking/mat/adjust.md)
* **수동 설정**: 수동 구성이나 Custom link를 쓰더라도 토스 매체 식별값과 측정값이 남아 있어야 해요.

**2) 기본 링크에 딥링크 주소 붙이기**

어느 방법으로 만든 기본 링크든, 토스용 필수·권장값이 들어 있는 기본 링크에 딥링크 주소를 아래처럼 붙여요.

1. 실제 광고에 사용할 Adjust 기본 트래킹 링크를 준비해요.
2. 2단계에서 받은 OS별 딥링크 주소를 URL 인코딩해요. 딥링크 주소를 다른 URL의 파라미터 값으로 넣기 위해 `:`, `/`, `?`, `&`, `=` 같은 기호를 필요한 형식으로 바꿔요. 예를 들어 `:`는 `%3A`, `/`는 `%2F`예요. 기본 트래킹 링크 전체를 인코딩하지 않아요.
3. 기본 트래킹 링크 맨 끝에 `&deep_link=`를 쓰고, 2번에서 바꾼 주소를 붙여요. 기본 트래킹 링크에 `?`가 없으면 `&` 대신 `?`로 붙여요.
4. 완성한 링크를 복사해요. 원래 링크에 있던 부분은 지우거나 바꾸지 않아요.

예시:

* iOS 딥링크 주소: sampleios://event/123
* iOS 링크에 넣을 값: deep\_link=sampleios%3A%2F%2Fevent%2F123
* Android 딥링크 주소: sampleandroid://event/123
* Android 링크에 넣을 값: deep\_link=sampleandroid%3A%2F%2Fevent%2F123

두 OS의 딥링크 주소가 다르면 OS마다 맞는 링크를 만들고 모두 테스트해요. 기존 스토어 주소는 그대로 둬요. `deep_link`는 다른 리다이렉트 설정보다 먼저 적용되므로 앱을 설치한 상태와 설치하지 않은 상태를 모두 확인해요. 자세한 내용은 [Link parameters](https://help.adjust.com/en/article/link-parameters)와 [앱 스킴 사용 예시](https://help.adjust.com/en/article/reftag)를 참고해 주세요.



**③ 필수·권장 항목 확인하기**

자동으로 만든 링크와 직접 만든 링크 모두 아래 항목이 들어 있는지 확인해요.

| 구분 | 항목                 | 값                    | 설명                   |
| -- | ------------------ | -------------------- | -------------------- |
| 필수 | `toss_click_id`    | `{TOSS_TK_CLICK_ID}` | 클릭 ID                |
| 필수 | `idfa / gps_adid`  | `{IDFA} / {AIFA}`    | 각 항목에 대응하는 OS별 광고 ID |
| 필수 | `toss_campaign_id` | `{TOSS_CID}`         | 캠페인 ID               |
| 권장 | `toss_creative_id` | `{TOSS_CREATIVE_ID}` | 소재 ID                |
| 권장 | `toss_site_id`     | `{SITE_ID}`          | 매체·지면 구분             |
| 권장 | `campaign`         | `{CAMPAIGN_NAME}`    | 캠페인명                 |
| 권장 | `adgroup`          | `{ADGROUP_NAME}`     | 광고 그룹명               |

②에서 인코딩한 `deep_link` 값은 위 표의 파라미터가 들어 있는 기본 링크 끝에 붙여요. 이때 기본 링크에 원래 있던 파라미터와 스토어 주소는 지우거나 바꾸지 않아요.
{% endtab %}

{% tab title="Airbridge" %}
**① 링크 만들기 전 설정하기**

1. **Tracking Link → Deep Links**로 이동해요.
2. **Android URL Scheme / iOS URL Scheme**에 OS별 앱 실행 주소(예: Android `sampleandroid://`, iOS `sampleios://`)를 `://`까지 포함해 입력해요.
3. Android는 자동 입력된 **Android Package Name**을 확인하고, `sha256_cert_fingerprints`에 배포 앱의 SHA256 인증서 지문을 입력해요. 여러 값은 쉼표로 구분해요.
4. iOS는 **iOS App ID**에 `App ID Prefix.Bundle ID` 형식으로 입력해요.
5. 앱에는 Airbridge SDK의 딥링크 처리를 구현해요.

{% hint style="info" %}
이 앱 정보는 토스애즈의 필수 요건과 별개로, Airbridge가 딥링크를 설정할 때 등록하라고 안내하는 값이에요. 이미 등록된 앱 ID와 인증서 값은 그대로 두고, 새로 설정할 때도 실제 배포 앱 기준으로 준비해 주세요. 앱의 도메인 연결은 맨 아래 '(권장) 유니버설 링크·앱 링크 설정하기'의 Airbridge 탭에서 안내해요. [공식 딥링크 사전 설정](https://help.airbridge.io/en/guides/retargeting-with-deep-links)
{% endhint %}

**② 링크 만들기**

**자동 생성 (권장)**

* **Integrations → Integrated Ad Channels → Toss → Tracking Link**에서 제공하는 토스용 클릭 링크를 먼저 사용해요. [토스애즈 Airbridge 연동 가이드](../../tracking/mat/airbridge.md)

**수동 설정**

*   새로 만들거나 수동으로 구성할 때는 토스 매체와 측정값을 유지한 채 아래처럼 목적지를 설정해요.

    1. **Tracking Link → Link Generation → Redirection**으로 이동해요.
    2. **Destination**에서 **App (Deep Link)** 항목을 골라요.

    <figure><img src="https://mintcdn.com/airbridge-help-center/C5DxUFZdlJVt7nU9/asset/image/tracking-link-destination-type-ko.png?w=1650&#x26;fit=max&#x26;auto=format&#x26;n=C5DxUFZdlJVt7nU9&#x26;q=85&#x26;s=5784746ef26accb5ea27262bf2c8395c" alt="출처: Airbridge 딥링크 적용 가이드"><figcaption><p>Airbridge 트래킹 링크의 최종 목적지 선택 화면 (출처: <a href="https://help.airbridge.io/ko/guides/retargeting-with-deep-links">Airbridge - 딥링크와 에어브릿지 매크로 활용하기</a>)</p></figcaption></figure>

    3. **Deep Link** 입력란에 OS별 딥링크 주소를 입력해요. 예: iOS `sampleios://event/123`, Android `sampleandroid://event/123`.

    <figure><img src="https://mintcdn.com/airbridge-help-center/jbQGnhL6LTf4bTuy/asset/image/deep-link-macro-redirect-path-ko.png?w=1650&#x26;fit=max&#x26;auto=format&#x26;n=jbQGnhL6LTf4bTuy&#x26;q=85&#x26;s=cb9fd96148ae56d66a73c3cc47a22583" alt="출처: Airbridge 딥링크·매크로 가이드"><figcaption><p>Airbridge 딥링크 주소 입력 화면 (출처: <a href="https://help.airbridge.io/ko/guides/retargeting-with-deep-links">Airbridge - 딥링크와 에어브릿지 매크로 활용하기</a>)</p></figcaption></figure>

    4. 필요한 광고 정보를 설정하고 화면 오른쪽 **Create tracking link**를 눌러요.
    5. 만든 트래킹 링크를 복사해요.

자세한 내용은 [한국어 공식 가이드](https://help.airbridge.io/ko/guides/retargeting-with-deep-links)를 참고해 주세요.

앱 스킴을 등록할 때는 앱 실행 주소(예: `sampleios://`)를, 링크를 만들 때는 딥링크 주소(예: `sampleios://event/123`)를 넣어요. 앱 스킴 이름에는 영문 소문자, 숫자, `+`만 쓸 수 있어요. 3번 단계 아래 이미지는 상품 ID 매크로를 쓴 예시예요. 정해진 화면 하나로 보내려면 실제 주소를 넣고, 매크로는 그 캠페인이 매크로 치환을 지원할 때만 써요.

앱에는 Airbridge SDK의 딥링크·화면 이동 처리가 구현돼 있어야 해요.



**③ 필수·권장 항목 확인하기**

자동으로 만든 링크와 직접 만든 링크 모두 아래 항목이 들어 있는지 확인해요.

| 구분 | 항목               | 값                    | 설명            |
| -- | ---------------- | -------------------- | ------------- |
| 필수 | `URL 경로`         | `/toss`              | 토스 채널의 경로 식별자 |
| 필수 | `click_id`       | `{TOSS_TK_CLICK_ID}` | 클릭 ID         |
| 필수 | `ad_id`          | `{USER_ADID}`        | 광고 ID         |
| 필수 | `campaign_id`    | `{TOSS_CID}`         | 캠페인 ID        |
| 권장 | `sub_id`         | `{SITE_ID}`          | 지면 구분         |
| 권장 | `ad_creative_id` | `{TOSS_CREATIVE_ID}` | 소재 ID         |
| 권장 | `campaign`       | `{CAMPAIGN_NAME}`    | 캠페인명          |
| 권장 | `ad_group`       | `{ADGROUP_NAME}`     | 광고 그룹명        |
| 권장 | `ad_creative`    | `{CREATIVE_NAME}`    | 소재명           |

표의 `/toss`는 파라미터가 아니라 링크 주소의 경로예요. 토스 채널에서 만든 링크에는 이미 들어 있으니 `path=/toss` 같은 파라미터를 따로 추가하지 않아요. 토스 채널 링크의 경로와 측정값은 그대로 두고, 앱 스킴 목적지만 설정해요.
{% endtab %}

{% tab title="Branch" %}
**① 링크 만들기 전 설정하기**

1. **Configuration → Link Controls → Link Routing Rules → Mobile Routing**으로 이동해요. 구버전 콘솔은 **Configuration → Link Settings**예요.
2. 아래 값을 입력하고 **Save changes**로 저장해요.

| 항목                   | 입력값                            |
| -------------------- | ------------------------------ |
| Android URI Scheme   | 앱 실행 주소. 예: `sampleandroid://` |
| Android URL          | Google Play 주소                 |
| Android Package Name | 대상 앱의 Package Name             |
| iOS URI Scheme       | 앱 실행 주소. 예: `sampleios://`     |
| iOS URL              | App Store 주소                   |

아래 이미지는 구버전 UI 화면이에요. 화면에 보이는 Custom URL 값은 예시이므로, 미설치 유저의 목적지는 실제 App Store 주소로 설정해요. [공식 iOS 가이드](https://help.branch.io/developer-hub/ios-basic-integration)

<figure><img src="https://help.branch.io/img/3997afe-Screenshot_2023-06-02_at_12.21.51_PM-1-.png" alt="Branch iOS URI Scheme 입력 예시"><figcaption><p>Branch iOS URI Scheme과 미설치 유저 목적지 입력 화면 (출처: <a href="https://help.branch.io/developer-hub/ios-basic-integration">Branch - iOS SDK Basic Integration</a>)</p></figcaption></figure>

3. **Advanced settings → URI scheme deep link mode**는 Intelligent로 둬요. Aggressive는 앱이 없는 유저에게 오류 메시지를 띄울 수 있고, Conservative는 앱을 설치한 유저도 스토어로 보낼 수 있어요.
4. 토스 광고 파트너를 활성화해요. Ad Link는 활성화한 파트너로만 만들 수 있어요. SDK와 딥링크 연동도 끝나 있어야 해요.

자세한 내용은 [공식 Routing 설정](https://help.branch.io/account-hub/link-routing-rules-new)을 참고해 주세요.



**② 링크 만들기**

**자동 생성 (권장)**

* 토스 파트너로 Ad Link를 만드는 방법을 먼저 사용해요. [토스애즈 Branch 연동 가이드](../../tracking/mat/branch.md)
  1. **LinkHub → + Create Link → Ad Link**를 눌러요.
  2. **App Only → App Install or Engagement**를 고르고 **Continue**를 눌러요.
  3. **Define → Configure Options**에서 링크 이름을 정하고, 활성화한 광고 파트너를 골라요.
  4. **Link Alias**에서 링크 별칭을 정해요. 한 번 만들면 바꿀 수 없어요.
  5. **Analytics Tags / Redirects**에서 캠페인 분류를 정하고, 앱이 없는 유저가 스토어로 가도록 설정돼 있는지 확인해요.
  6.  **Link Data → +More Data**에서 Key에 `$deeplink_path`를, Value에 개발팀에게 받은 화면 경로를 입력해요. 예: `event/123`. 앱 실행 주소(예: `sampleios://`)는 빼고 화면 경로만 넣어요. 두 OS의 경로가 다르면 Key를 `$android_deeplink_path`와 `$ios_deeplink_path`로 나눠 입력해요.

      아래는 Link Data 단계에서 Key와 Value를 입력하는 참고 화면이에요.

<figure><img src="https://help.branch.io/img/5fa51f4-configure_options-1-.png" alt="Branch Ad Link의 Key와 Value 설정 화면"><figcaption><p>Branch Ad Link의 딥링크 Key·Value 입력 화면 (출처: <a href="https://help.branch.io/marketer-hub/ad-links">Branch - Create Ad Links</a>)</p></figcaption></figure>

7. **Create Link Now → Validate & Share**에서 검증 오류가 있으면 고친 뒤 클릭용 링크를 복사해요. 노출용 링크가 함께 나와도 클릭용 링크를 복사해요.

<figure><img src="https://help.branch.io/img/3b4f754-Validation-1-.png" alt="출처: Branch Ad Links"><figcaption><p>Branch Ad Link 검증(Validation) 결과 화면 (출처: <a href="https://help.branch.io/marketer-hub/ad-links">Branch - Create Ad Links</a>)</p></figcaption></figure>

이 가이드는 **App Only** 형식을 기준으로 해요. Cross-Platform은 앱이 없는 유저를 웹으로 보내는 검색·디스플레이 광고용 형식이에요. 자세한 내용은 [공식 Ad Links 가이드](https://help.branch.io/marketer-hub/ad-links)와 [공식 파라미터 가이드](https://help.branch.io/marketer-hub/deep-link-reference)를 참고해 주세요.

**Validate & Share** 검증을 통과한 뒤에도 실제 기기에서 앱 실행, 앱에서 열 화면으로 이동, 스토어 이동을 확인해요. 입력한 화면 경로가 앱의 화면 이동 처리와 일치해야 해요. 실행 모드와 추가 옵션은 MMP 설정을 기준으로 적용해요.



**수동 설정**

* Custom link나 수동 설정을 쓰더라도 ③의 측정 파라미터와 토스 매체 식별값은 유지해야 해요.



**③ 필수·권장 항목 확인하기**

자동으로 만든 링크와 직접 만든 링크 모두 아래 항목이 들어 있는지 확인해요.

| 구분 | 항목             | 값                    | 설명            |
| -- | -------------- | -------------------- | ------------- |
| 필수 | `$3p`          | `a_toss`             | 토스 매체 식별값     |
| 필수 | `~click_id`    | `{TOSS_TK_CLICK_ID}` | 클릭 ID         |
| 필수 | `~campaign_id` | `{TOSS_CID}`         | 캠페인 ID        |
| 필수 | `$aaid`        | `{aaid}`             | Android 광고 ID |
| 필수 | `$idfa`        | `{idfa}`             | iOS 광고 ID     |
| 권장 | `~creative_id` | `{TOSS_CREATIVE_ID}` | 소재 ID         |
| 권장 | `~channel`     | `{SITE_ID}`          | 매체·지면 구분      |

항목 이름의 `$`와 `~`, 매크로의 대소문자를 그대로 유지해요.
{% endtab %}

{% tab title="Singular" %}
**① 링크 만들기 전 설정하기**

1. **Settings → Apps → 대상 앱**에서 Android·iOS를 펼치고 **Show Advanced Settings**를 눌러요. 콘솔에 따라 **Apps Configuration**으로 보일 수 있어요.
2. Android는 **Android App Scheme**(또는 Android Scheme)에, iOS는 **iOS App Scheme**(또는 App Scheme)에 앱에 구현된 앱 스킴을 입력해요.

<figure><img src="https://support.singular.net/hc/article_attachments/33430831952027" alt="출처: Singular Links Prerequisites"><figcaption><p>Singular Android 앱 스킴 입력 화면 (출처: <a href="https://support.singular.net/hc/en-us/articles/360031371451-Singular-Links-Prerequisites">Singular - Singular Links Prerequisites</a>)</p></figcaption></figure>

<figure><img src="https://support.singular.net/hc/article_attachments/360055239651" alt="출처: Singular Links Prerequisites"><figcaption><p>Singular iOS 앱 스킴 입력 화면 (출처: <a href="https://support.singular.net/hc/en-us/articles/360031371451-Singular-Links-Prerequisites">Singular - Singular Links Prerequisites</a>)</p></figcaption></figure>

3. 앱 링크·유니버설 링크도 쓴다면 Android는 App Links SHA256 fingerprints를, iOS는 Team ID를 추가해요. 자세한 방법은 맨 아래 '(권장) 유니버설 링크·앱 링크 설정하기'의 Singular 탭에서 안내해요.
4. 등록된 링크 도메인이 없으면 **Attribution → Manage Links → Manage Link Domains**에서 Subdomain 이름을 입력하고 **Create → Done** 순서로 만들어요.

{% hint style="info" %}
* 앱 스킴만 쓰더라도 Singular가 요구하는 사전 설정이 있는지 [공식 사전 설정 가이드](https://support.singular.net/hc/en-us/articles/360031371451-Singular-Links-Prerequisites)에서 확인해요.
* 이미 등록된 Team ID와 인증서(SHA256) 값은 지우거나 바꾸지 않아요.
* 콘솔에 앱 스킴을 등록하는 것만으로는 화면 이동이 되지 않아요. 앱에 Singular SDK와 화면 이동 처리가 구현돼 있어야 해요.
{% endhint %}

**(선택) 자주 쓰는 목적지 미리 등록하기**

같은 앱의 **Destinations**에 `sampleios://event/123` 같은 딥링크 주소를 한 줄에 하나씩 추가하고 Save해요. 등록한 주소는 링크를 만들 때 드롭다운에서 고를 수 있어요. 미리 등록하지 않아도 링크 생성 화면에서 직접 입력할 수 있어요. [공식 목적지 설정 안내](https://support.singular.net/hc/en-us/articles/360050910891-How-to-Configure-Deep-Links)

아래는 자주 쓰는 딥링크 주소를 한 줄씩 등록하는 화면이에요. [원본 보기](https://support.singular.net/hc/article_attachments/360072436012)

<figure><img src="https://support.singular.net/hc/article_attachments/360072436012" alt="Singular Destinations 사전 등록 화면"><figcaption><p>Singular 자주 쓰는 목적지(Destinations) 사전 등록 화면 (출처: <a href="https://support.singular.net/hc/en-us/articles/360050910891-How-to-Configure-Deep-Links">Singular - How to Configure Deep Links</a>)</p></figcaption></figure>

**② 링크 만들기**

**자동 생성 (권장)**

* **Attribution → Manage Links → Create Link → Partner**에서 토스 매체를 골라 만드는 방식을 먼저 사용해요. [토스애즈 Singular 연동 가이드](../../tracking/mat/singular.md)
  1. 대상 앱을 고르고 **Create Link**를 눌러요.
  2. 링크 유형은 광고 네트워크용인 **Partner**를 골라요. **Custom Source**는 자사 채널, 이메일, 인플루언서용이에요.
  3. **Source Name**에 토스 매체를, **Tracking Link Name**에 링크 이름을 입력해요.
  4. **Link Settings and Redirects**에서 링크 도메인을 고르고 대상 iOS·Android 플랫폼을 켜요.
  5. OS마다 아래 입력란을 채워요.

| 입력란                                          | 언제 이동하나요          | 입력값                                                                         |
| -------------------------------------------- | ----------------- | --------------------------------------------------------------------------- |
| If the app is not installed…                 | 앱이 없는 상태에서 클릭했을 때 | 해당 OS의 App Store·Google Play 주소                                             |
| If the app is already installed… (deep link) | 앱이 있는 상태에서 클릭했을 때 | 딥링크 주소. 예: iOS `sampleios://event/123`, Android `sampleandroid://event/123` |
| After installation… (deferred deep link)     | 새로 설치하고 처음 실행했을 때 | 설치 후 첫 실행에도 특정 화면으로 보낼 때 쓰는 주소                                              |

<figure><img src="https://support.singular.net/hc/article_attachments/360072435992" alt="출처: Singular 딥링크 설정 가이드"><figcaption><p>Singular 링크 생성 시 설치 상태별 목적지 입력 화면 (출처: <a href="https://support.singular.net/hc/en-us/articles/360050910891-How-to-Configure-Deep-Links">Singular - How to Configure Deep Links</a>)</p></figcaption></figure>

6. **Save**를 누르고 **Link Summary**에서 클릭용 링크(Click-through link)를 복사해요. 주소가 `https://`로 시작하는지 확인해요.

딥링크 입력란이 비활성화돼 있다면 **Settings → Apps → 해당 OS → Show Advanced Settings**에서 **Android Deep Linking / iOS Deep Linking** 설정을 확인해요. 앱에서 열 화면 없이 만든 링크에는 이 기능을 나중에 더할 수 없어서 새 링크를 만들어야 해요. 자세한 내용은 [공식 링크 생성 가이드](https://support.singular.net/hc/en-us/articles/13000445013531-How-to-Build-Tracking-Links)를 참고해 주세요.



**수동 설정**

* Custom link나 수동 설정을 쓰더라도 토스 매체와 ③의 필수·권장값은 유지해요. 매체를 임의의 Custom Source로 바꾸면 안 돼요. 목적지는 아래 파라미터로 설정해요.

| 파라미터          | 입력할 값                  |
| ------------- | ---------------------- |
| `_dl`         | 두 OS에서 공통으로 사용할 딥링크 주소 |
| `_ios_dl`     | iOS 전용 딥링크 주소          |
| `_android_dl` | Android 전용 딥링크 주소      |

`sampleios://event/123`처럼 앱 실행 주소와 화면 경로를 모두 포함한 딥링크 주소를 넣어요. 공통 주소와 OS별 주소를 구분하고, 해당 OS의 딥링크 기능을 켠 링크를 사용해요. 파라미터만 추가한다고 딥링크 기능이 켜지지는 않아요. 발급되는 주소는 `https://[서브도메인].sng.link/...` 형식이에요. [공식 Tracking Links FAQ](https://support.singular.net/hc/en-us/articles/360030934212-Singular-Links-Tracking-Links-FAQ)

Deferred Deep Link는 앱을 설치하지 않은 유저가 링크를 누르고 앱을 설치해 처음 실행했을 때 앱에서 열 화면으로 보내는 기능이에요. 이미 설치된 앱을 여는 일반 딥링크와 같은 딥링크 주소로 설정할 수 있어요. **Deferred Deep Link는 추가 기능**이라 별도 SDK 구현과 지원 조건을 확인해야 해요. 적용했다면 앱이 없는 기기에서 클릭 → 스토어 → 설치·첫 실행 → 앱에서 열 화면까지 추가로 테스트해요. [공식 설정·테스트 안내](https://support.singular.net/hc/en-us/articles/360050910891-How-to-Configure-Deep-Links)

토스 iOS 앱에서 앱 스킴으로 연결할 수 있도록 Singular 트래킹 링크에 `_force_redirect=1`을 추가해 주세요. iOS 앱 스킴을 등록하고, `_dl` 또는 `_ios_dl`에는 그 스킴을 쓰는 딥링크 주소를 설정해 주세요. 앱을 설치한 상태와 설치하지 않은 상태에서 각각 앱 실행과 스토어 연결을 확인해 주세요.



**③ 필수·권장 항목 확인하기**

자동으로 만든 링크와 직접 만든 링크 모두 아래 항목이 들어 있는지 확인해요.

| 구분 | 항목                    | 값                               | 설명               |
| -- | --------------------- | ------------------------------- | ---------------- |
| 필수 | `cl`                  | `{TOSS_TK_CLICK_ID}`            | 클릭 ID            |
| 필수 | `idfa / aifa / ad_id` | `{IDFA} / {AIFA} / {USER_ADID}` | 각 항목에 대응하는 광고 ID |
| 필수 | `pcid`                | `{TOSS_CID}`                    | 캠페인 ID           |
| 권장 | `pcrid`               | `{TOSS_CREATIVE_ID}`            | 소재 ID            |
| 권장 | `site_id`             | `{SITE_ID}`                     | 매체·지면 구분         |
| 권장 | `pcn`                 | `{CAMPAIGN_NAME}`               | 캠페인명             |
| 권장 | `pcrn`                | `{CREATIVE_NAME}`               | 소재명              |
| 권장 | `pscn`                | `{ADGROUP_NAME}`                | 광고 그룹명           |

딥링크를 켠 토스 Partner 링크에는 위 측정값과 `_dl` 또는 OS별 목적지 값이 함께 들어 있어야 해요.
{% endtab %}

{% tab title="DFINERY" %}
**① 링크 만들기 전 설정하기**

1. **Attribution → Ad Landing Settings**로 이동해요.
2. 아래 값을 입력하고 저장해요.

| OS      | 항목               | 입력값                               |
| ------- | ---------------- | --------------------------------- |
| Android | default URL      | 광고 대상 앱의 Google Play 주소           |
| Android | Deep Link Scheme | 앱 스킴 이름만 입력해요. 예: `sampleandroid` |
| Android | Package Name     | 광고 대상 앱의 Package Name             |
| iOS     | default URL      | 광고 대상 앱의 App Store 주소             |
| iOS     | Deep Link Scheme | 앱 스킴 이름만 입력해요. 예: `sampleios`     |
| iOS     | App Store ID     | App Store ID의 숫자 부분               |

<figure><img src="https://help.dfinery.io/hc/article_attachments/36794021440537" alt="출처: DFINERY Ad Landing Settings"><figcaption><p>DFINERY Ad Landing Settings 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360003394433">DFINERY - Ad Landing Settings : 유저의 랜딩지점 설정하기</a>)</p></figcaption></figure>

{% hint style="info" %}
Android, iOS, PC의 **default URL은 필수**이고 `https://`나 `http://`로 시작하는 주소를 넣어요. PC에는 기본 웹 목적지를 넣고, 앱 다운로드 안내 페이지가 따로 있으면 App Download Page에 입력해요. Deep Link Scheme 입력란에는 `://`와 화면 경로를 넣지 않아요.
{% endhint %}

3. **Attribution → Ad partner settings**에서 토스 매체를 골라 활성화해요. 매체별 필수값이 있으면 함께 입력해요.

자세한 내용은 [공식 랜딩 설정 가이드](https://help.dfinery.io/hc/ko/articles/360003394433)와 [공식 매체 활성화 가이드](https://help.dfinery.io/hc/ko/articles/14842338029593)를 참고해 주세요.

**② 링크 만들기**

**자동 생성 (권장)**

*   토스 매체를 캠페인에 연결하고 콘솔이 제공하는 클릭 링크를 만드는 방법을 먼저 사용해요. [토스애즈 DFINERY 연동 가이드](../../tracking/mat/dfinery.md)

    1. **Attribution → Ad Campaign → +create campaign**에서 캠페인 이름을 저장해요.
    2.  캠페인의 **Tracking Link** 탭에서 ①에서 활성화한 매체를 고르고 **Connect with Ad Campaign**으로 연결해요.

        아래는 Tracking Link 탭에서 매체를 고르고 Connect with Ad Campaign으로 연결하는 참고 화면이에요.

    <figure><img src="https://help.dfinery.io/hc/article_attachments/15001194947609" alt="DFINERY 매체와 캠페인 연결 화면"><figcaption><p>DFINERY 캠페인에 매체를 연결하는 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360024465693">DFINERY - Ad Campaign 생성과 Tracking Link 발급</a>)</p></figcaption></figure>

3.  링크 이름을 입력하고, 랜딩 형식은 **Download + Deeplink**를 골라요.

    아래는 링크 이름과 랜딩 형식을 설정하는 화면이에요. [원본 보기](https://help.dfinery.io/hc/article_attachments/15002553933593)

<figure><img src="https://help.dfinery.io/hc/article_attachments/15002553933593" alt="DFINERY 링크명과 Download + Deeplink 선택 화면"><figcaption><p>DFINERY 링크 이름과 랜딩 형식 선택 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360024465693">DFINERY - Ad Campaign 생성과 Tracking Link 발급</a>)</p></figcaption></figure>

4. 새로 나타난 **Deep Linking**에서 대상 OS가 **ON**인지 확인해요. OFF면 앱이 있는 유저도 Ad-Touch Landing으로 이동해요. **Scheme**에는 ①에서 등록한 앱 스킴이 보여요.
5. **Static Path → Path**에 화면 경로만 입력해요. 예를 들어 딥링크 주소가 `sampleandroid://product_id_12345`라면 `product_id_12345`만 넣어요.

<figure><img src="https://help.dfinery.io/hc/article_attachments/15013812418585" alt="DFINERY Deep Linking의 Static Path 설정 화면"><figcaption><p>DFINERY Deep Linking의 고정 경로(Static Path) 입력 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360024465693">DFINERY - Ad Campaign 생성과 Tracking Link 발급</a>)</p></figcaption></figure>

6. **Ad-Touch Landing**은 앱이 없는 유저가 이동할 곳이에요. 기본 설정을 그대로 두면 ①에서 등록한 스토어로 이동해요.
7. 만든 링크 중 클릭용 링크를 복사해요. 노출용 링크가 함께 나와도 클릭용 링크를 복사해요.

<figure><img src="https://help.dfinery.io/hc/article_attachments/15075316676249" alt="출처: DFINERY 링크 생성 가이드"><figcaption><p>DFINERY 클릭용·노출용 트래킹 링크 발급 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360024465693">DFINERY - Ad Campaign 생성과 Tracking Link 발급</a>)</p></figcaption></figure>

**고정 경로와 동적 경로 구분하기**

| 항목                                     | 입력할 값                                                |
| -------------------------------------- | ---------------------------------------------------- |
| Ad Landing Settings → Deep Link Scheme | 앱 스킴 이름. 예: iOS `sampleios`, Android `sampleandroid` |
| Deep Linking → Scheme                  | 등록한 OS별 Scheme을 확인해요.                                |
| Deep Linking → Static Path → Path      | 고정된 화면 경로. 예: `product_id_12345`                     |
| Deep Linking → Dynamic                 | 발급 링크의 `{deeplink_custom_path}` 자리를 실제 화면 경로로 치환해요.  |

Path 입력란에는 딥링크 주소 전체를 넣지 않아요. Dynamic은 경로 치환을 지원하는 캠페인에서만 쓰고, `{deeplink_custom_path}`를 바꾸지 않은 채로 배포하면 안 돼요. Deep Linking은 기본적으로 Ad Landing Settings 값을 쓰고, 여기서 직접 설정하면 그 값을 덮어써요. [공식 Static/Dynamic 설정 안내](https://help.dfinery.io/hc/en-us/articles/360024465693-Create-Ad-Campaign-and-Issue-Tracking-Link)

**앱이 없는 유저의 목적지 확인하기**

앱이 있는 유저가 볼 화면은 Deep Linking에서, 앱이 없는 유저가 갈 목적지는 Ad-Touch Landing에서 설정해요. Android·iOS 기본 설정을 그대로 두면 등록한 스토어로 이동해요. 다른 목적지가 필요할 때만 직접 설정하고, 이때도 앱 설치 광고는 스토어로 이동해야 한다는 요건을 확인해요.

아래는 Android, iOS, Web별로 앱이 없는 유저의 목적지를 확인하는 화면이에요. [원본 보기](https://help.dfinery.io/hc/article_attachments/15050040003097)

<figure><img src="https://help.dfinery.io/hc/article_attachments/15050040003097" alt="DFINERY Ad-Touch Landing 설정 화면"><figcaption><p>DFINERY Ad-Touch Landing 설정 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360024465693">DFINERY - Ad Campaign 생성과 Tracking Link 발급</a>)</p></figcaption></figure>

만든 링크는 **Ad Campaign → 해당 캠페인 → Tracking Link → 연결 매체 → URL Details**에서 다시 찾을 수 있어요. 자세한 내용은 [캠페인·트래킹 링크 가이드](https://help.dfinery.io/hc/en-us/articles/360024465693-Create-Ad-Campaign-and-Issue-Tracking-Link)를 참고해 주세요.

테스트는 앱의 Deeplink 이벤트와 SDK 연동이 끝난 배포 버전으로 해요. 링크는 이메일 등에 넣어 실제 휴대폰에서 눌러 보고, 브라우저 주소창에 직접 입력하지 마세요. 앱이 있는 상태, 없는 상태, 실제 광고 연결 환경을 각각 확인해요.



**수동 설정**

* 수동으로 구성할 때도 토스 매체와 ③의 필수·권장값은 유지해요.



**③ 필수·권장 항목 확인하기**

자동으로 만든 링크와 직접 만든 링크 모두 아래 항목이 들어 있는지 확인해요.

| 구분 | 항목           | 값                    | 설명       |
| -- | ------------ | -------------------- | -------- |
| 필수 | `cb_1`       | `{TOSS_TK_CLICK_ID}` | 클릭 ID    |
| 필수 | `m_adid`     | `{USER_ADID}`        | 광고 ID    |
| 필수 | `m_ad`       | `{TOSS_CID}`         | 캠페인 ID   |
| 권장 | `m_creative` | `{TOSS_CREATIVE_ID}` | 소재 ID    |
| 권장 | `m_campaign` | `{CAMPAIGN_NAME}`    | 캠페인명     |
| 권장 | `cb_2`       | `{SITE_ID}`          | 매체·지면 구분 |
| 권장 | `cb_3`       | `{CREATIVE_NAME}`    | 소재명      |
| 권장 | `m_adgroup`  | `{ADGROUP_NAME}`     | 광고 그룹명   |

측정용 파라미터와 Deep Linking의 Scheme·Path는 서로 다른 값이에요. 두 값을 구분해서 설정하고, 발급된 링크에 있던 매체·측정값은 그대로 둬요.
{% endtab %}
{% endtabs %}



## 4. 트래킹 링크 테스트하기 <a href="#step4-test" id="step4-test"></a>

마케팅팀과 개발팀이 함께 진행하는 단계예요. 3단계에서 복사한 클릭용 트래킹 링크를 실제 휴대폰에서 눌러, 앱을 설치한 유저는 앱으로, 설치하지 않은 유저는 스토어로 이동하는지 확인해요.

{% hint style="info" %}
**반드시 트래킹 링크로 테스트해요.** 딥링크 주소(예: `sampleios://event/123`)를 바로 열면 MMP를 거치지 않아요. 그래서 앱이 열려도 MMP 설정이 맞는지는 알 수 없어요.
{% endhint %}

### 테스트 전에 링크 점검하기 <a href="#pre-test-check" id="pre-test-check"></a>

자동 생성과 Custom link 중 어떤 방법을 썼든, 최종 링크를 해당 MMP의 필수·권장 항목과 대조해요. 아래 내용을 확인한 뒤 바로 그 링크로 테스트해요.

* 필수값이 빠지지 않았는지
* 매체 식별값이 바뀌지 않았는지
* 매크로에 오타가 없는지
* 같은 파라미터가 두 번 들어가지 않았는지
* 인코딩과 `?`·`&` 위치가 맞는지

### 휴대폰에서 링크 눌러 보기 <a href="#test-on-device" id="test-on-device"></a>

1. 링크를 이메일이나 메모 앱에 넣고 실제 휴대폰에서 눌러요. 카카오톡·인스타그램 같은 앱에서는 앱 안 브라우저로 열려 앱 스킴이 동작하지 않을 수 있어요. 브라우저 주소창에 직접 붙여 넣는 방식만으로 판단하지 않아요.
2. 대상 OS마다 앱을 설치한 기기와 설치하지 않은 기기에서 각각 눌러 봐요. 설치하지 않은 기기가 없으면 테스트 기기에서 앱을 지운 뒤 눌러요.
3. 결과가 아래 표와 같은지 확인해요. 특정 화면을 설정했다면 그 화면까지, 앱 실행만 설정했다면 앱이 정상적으로 실행되는지 확인해요.

| 환경            | 기대 결과                        |
| ------------- | ---------------------------- |
| Android 앱 설치  | 앱이 열리고, 설정한 화면으로 이동해요.       |
| Android 앱 미설치 | 해당 앱의 Google Play 페이지로 이동해요. |
| iOS 앱 설치      | 앱이 열리고, 설정한 화면으로 이동해요.       |
| iOS 앱 미설치     | 해당 앱의 App Store 페이지로 이동해요.   |

{% hint style="info" %}
앱 스킴은 실행 환경에 따라 확인창이나 브라우저 전환이 나타날 수 있어요. 중간 화면의 유무만으로 성공·실패를 판단하지 말고 최종 앱·스토어 도달 여부를 확인해요.
{% endhint %}

### 토스 앱에서도 확인하기 <a href="#test-in-toss" id="test-in-toss"></a>

토스 앱에서도 광고 링크가 제대로 이동하는지 확인해요. 토스 앱은 iOS와 Android 모두 5.282.0 이상에서 테스트해 주세요.&#x20;

토스 iOS 앱에서 앱을 설치하지 않은 상태로 링크를 누르면 토스 안의 App Store 상품 화면이나 App Store로 연결되는데, 둘 다 정상 결과예요. 브라우저에서 테스트한 결과만으로 토스 앱 안에서의 동작을 판단하지 않아요.

AppsFlyer 링크를 iOS에서 테스트할 때 토스 앱이 5.282.0보다 낮은 버전이면, 앱이 설치돼 있어도 App Store로 이동할 수 있어요. 이때는 토스 앱을 5.282.0 이상으로 업데이트한 뒤 다시 테스트해 주세요.

### MMP별 추가 항목 확인하기 <a href="#mmp-extra-checks" id="mmp-extra-checks"></a>

Branch, Singular, DFINERY를 쓴다면 아래 내용도 확인해요.

| MMP      | 함께 확인할 것                                                                                                     |
| -------- | ------------------------------------------------------------------------------------------------------------ |
| Branch   | **Validate & Share**에서 검증 오류를 확인하고 고쳐요. 검증을 통과한 뒤에도 휴대폰에서 링크를 직접 눌러 앱 실행, 앱에서 열 화면으로 이동, 미설치 시 스토어 이동을 확인해요. |
| Singular | Deferred Deep Link를 적용했다면 앱을 설치하지 않은 기기에서 클릭 → 스토어 → 설치·첫 실행 → 설정한 화면까지 확인해요.                                |
| DFINERY  | 테스트 후 MMP에서 클릭 기록과 앱의 딥링크 이벤트 수신을 각각 확인해요. 기록이 없으면 배포 앱의 DFINERY SDK와 딥링크 이벤트 연동을 확인해요.                      |

### 문제 해결하기 <a href="#troubleshooting" id="troubleshooting"></a>

결과가 기대 결과와 다르면 아래 표에서 같은 증상을 찾아 오른쪽 내용을 확인해요.

| 증상                   | 확인할 내용                                                                                                                                                                                                                                                                 |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 앱을 설치했는데 스토어로 이동해요.  | <p>앱 스킴 구현, MMP에 등록한 앱 스킴, OS별 딥링크 주소를 확인하고, 토스 앱 5.282.0 이상에서 다시 테스트해요.</p><ul><li>AppsFlyer: 최종 링크에 <code>af_dp</code>가 있는지, <code>af_force_deeplink</code>는 없는지 확인해요.</li><li>Branch (iOS·Android 공통): URI scheme deep link mode가 Conservative가 아닌지 확인해요.</li></ul> |
| 앱은 열리지만 다른 화면이에요.    | MMP에 넣은 딥링크 주소나 화면 경로가 앱이 처리하도록 만든 것과 같은지 확인해요.                                                                                                                                                                                                                        |
| 한쪽 OS에서만 실패해요.       | OS별 앱 스킴 이름, OS별 딥링크 주소, 앱 식별 정보를 확인해요.                                                                                                                                                                                                                                |
| 앱을 설치하지 않은 상태에서 멈춰요. | 스토어 주소와 강제 실행 옵션을 확인해요.                                                                                                                                                                                                                                                |
| 링크를 고친 뒤 실패해요.       | 주소의 `?`와 `&` 위치, `%3A`처럼 바꿔 넣은 기호, 빠지거나 두 번 들어간 값이 없는지 확인해요.                                                                                                                                                                                                           |
| 앱은 열리지만 측정되지 않아요.    | 앱의 MMP SDK 연동, MMP 콘솔의 토스애즈 연동 설정, 링크에 붙은 측정값을 확인해요.                                                                                                                                                                                                                   |

### 최종 링크 준비하기 <a href="#final-link" id="final-link"></a>

정상 작동을 확인했다면 최종 트래킹 링크를 설정값이 모두 보이는 원래의 긴 주소(롱 링크)로 준비해요. 이 링크는 소재를 등록할 때 제출해요. 제출 규칙은 [앱 설치 유도하기 소재 가이드](creative.md)에서 안내해요.



## (권장) 유니버설 링크·앱 링크 설정하기 <a href="#universal-link" id="universal-link"></a>

앱 설치 유도하기 광고에서 앱을 실행하는 데 필요한 필수 요건은 앱 스킴을 적용한 MMP 트래킹 링크예요. 여기에 유니버설 링크(iOS)와 앱 링크(Android)도 설정하는 것을 권장해요. 지원되는 환경에서는 HTTPS 링크로 앱에 바로 연결할 수 있어요.

{% hint style="info" %}
**앱 스킴 설정은 지우지 말고 그대로 둬요.**

유니버설 링크·앱 링크가 동작하지 않는 환경에서는 앱 스킴으로 앱을 열어요. 어떤 방식으로 열리는지는 OS, 브라우저, 앱 상태, MMP 설정에 따라 달라요. 모든 환경에서 같은 방식으로 열리거나 확인창 없이 바로 열린다고 보장되지는 않아요.

유니버설 링크·앱 링크 설정과 앱 배포를 마치면 최종 링크로 꼭 테스트해 주세요.
{% endhint %}

### 설정 순서 알아보기 <a href="#ul-setup-flow" id="ul-setup-flow"></a>

유니버설 링크·앱 링크는 트래킹 링크의 `https://` 주소(예: AppsFlyer의 `brand.onelink.me`)를 눌렀을 때 앱을 바로 열어 주는 기능이에요. 휴대폰은 아래 두 곳의 정보가 서로 맞을 때만 앱을 열어요.

* **링크 쪽**:
  * 링크 도메인(예: `brand.onelink.me`)에 있는 확인 파일에 앱 정보가 들어 있어야 해요. 이 파일을 iOS에서는 AASA(apple-app-site-association) 파일, Android에서는 `assetlinks.json` 파일이라고 불러요.
  * 링크 도메인은 앱 전용 도메인이어야 해요. `app.appsflyer.com`, `abr.ge`처럼 여러 앱이 함께 쓰는 주소로는 앱을 바로 열 수 없어요.
  * 마케팅팀이 MMP 콘솔에 앱 정보를 입력하면 MMP가 이 파일을 제공해요.
  * MMP 도메인이 아닌 별도 도메인을 쓴다면 그 도메인에 필요한 파일 제공·연결 요건도 확인해요.
* **앱 쪽**:
  * 앱에 링크 도메인이 등록돼 있어야 해요.
  * 개발팀이 앱에서 등록해요. iOS는 Associated Domains에, Android는 `AndroidManifest.xml`의 앱 링크용 `<intent-filter>`에 도메인을 등록해요.
  * Android는 1단계에서 만든 앱 스킴용 `<intent-filter>` 블록은 그대로 두고, 앱 링크용 `<intent-filter>` 블록을 따로 하나 더 추가해요. [Android 공식 가이드](https://developer.android.com/training/app-links/add-applinks)

마케팅팀은 개발팀에게 앱 정보를, 개발팀은 마케팅팀에게 링크 도메인을 받아야 설정할 수 있어요. 그래서 두 팀이 아래 순서로 값을 주고받으며 진행해요.

1. **개발팀 → 마케팅팀**: 앱 정보를 전달해요. 전달할 값은 아래 '개발팀이 전달할 값 확인하기'에서 안내해요.
2. **마케팅팀**: 받은 앱 정보를 MMP 콘솔에 입력해요.
3. **마케팅팀 → 개발팀**: MMP 콘솔에 보이는 링크 도메인을 전달해요.
4. **개발팀**: 그 도메인을 앱에 등록하고 앱을 배포해요.
5. **마케팅팀**: 배포가 끝나면 '4. 트래킹 링크 테스트하기'를 다시 해요.

MMP마다 무엇을 어디에 입력하는지는 아래 'MMP별 유니버설 링크·앱 링크 설정하기'에서 안내해요.

{% hint style="info" %}
**앱 스킴 설정은 그대로 유지해요.** 실제 연결 방식과 앱 스킴 fallback 동작은 OS, 브라우저, 앱 상태, MMP 설정에 따라 달라져요. 모든 환경에서 같은 순서로 실행되거나 확인창 없이 열린다고 보장되지 않으니, 최종 링크로 꼭 테스트해 주세요.
{% endhint %}

### 개발팀이 전달할 값 확인하기 <a href="#ul-app-info" id="ul-app-info"></a>

Bundle ID와 Package Name은 앱 코드에서 확인할 수 있어요. App ID Prefix(또는 Team ID)와 SHA256 값은 Apple 개발자 계정이나 Google Play Console 권한이 있는 담당자가 확인해요.

| 값                              | 확인하는 곳                                                                                                   |
| ------------------------------ | -------------------------------------------------------------------------------------------------------- |
| iOS Bundle ID                  | Xcode 프로젝트 설정 또는 App Store Connect의 앱 정보                                                                 |
| App ID Prefix(MMP에 따라 Team ID) | Apple 개발자 계정의 Membership 화면(Team ID), Identifiers에서 이 앱을 고른 화면(App ID Prefix)                            |
| Android Package Name           | 앱 `build.gradle`의 `applicationId` 또는 Google Play Console                                                 |
| SHA256 Certificate Fingerprint | 배포 앱의 서명 인증서 SHA256 값. Play App Signing을 사용한다면 Google Play Console의 App signing key certificate 값을 확인해요. |

* **App ID Prefix와 Team ID**: 둘 다 영문·숫자 10자리 값이에요. 대부분 두 값이 같지만 서로 다른 앱도 있어요. 광고할 앱의 App ID Prefix와 Team ID를 각각 확인해 전달해요.
* **Android SHA256 값**: 실제 사용자에게 배포되는 앱의 서명 인증서를 기준으로 확인해요. Play App Signing을 사용하면 로컬 Upload key의 지문과 다를 수 있어요. [Android 공식 인증서 설정 가이드](https://developer.android.com/training/app-links/configure-assetlinks)

### MMP별 유니버설 링크·앱 링크 설정하기 <a href="#ul-mmp-setup" id="ul-mmp-setup"></a>

사용하는 MMP 탭을 골라 ①\~④ 순서대로 진행해요.

* **① 개발팀에게 앱 정보 받기**
* **② MMP 콘솔에 앱 정보 입력하기**
* **③ 개발팀에 도메인 전달하기**
* **④ 링크 만들고 테스트하기**

{% tabs %}
{% tab title="AppsFlyer" %}
**① 개발팀에게 앱 정보 받기**

개발팀에게 아래 값을 받아요. 각 값은 위 '개발팀이 전달할 값 확인하기' 표를 참고해요.

* iOS: Team ID. 아직 출시하지 않은 앱이면 Bundle ID도 받아요.
* Android: SHA256 Certificate Fingerprint

**② MMP 콘솔에 앱 정보 입력하기**

'3. MMP에서 트래킹 링크 만들기'의 AppsFlyer 탭 ①에서 쓰던 OneLink 템플릿에 유니버설 링크·앱 링크를 켜요.

1. **Edit OneLink template → When app is installed** 화면을 열어요.
2. 화면 위쪽 iOS·Android 항목을 아래처럼 바꿔요.

| OS      | 선택할 설정                                                                                    | 입력값                                       |
| ------- | ----------------------------------------------------------------------------------------- | ----------------------------------------- |
| iOS     | **Change to launch the app using Universal Links → Launch the app using Universal Links** | Team ID. 출시 전 앱은 Bundle Identifier도 입력해요. |
| Android | **Change to launch the app using App Links → Launch the app using App Links**             | SHA256 fingerprint                        |

3. 화면 아래쪽 앱 스킴 설정은 그대로 두고 템플릿을 저장해요. 저장하면 AppsFlyer가 링크 도메인의 확인 파일을 만들어 제공해요. 반영되기까지 최대 1시간이 걸릴 수 있어요.

**③ 개발팀에 도메인 전달하기**

* iOS 개발팀: OneLink Subdomain(예: `brand.onelink.me`)을 전달해요.
* Android 개발팀: AppsFlyer가 만들어 준 `intent-filter`를 전달해요.

개발팀은 이 값을 앱에 등록하고 앱을 배포해요.

**④ 링크 만들고 테스트하기**

1. ②에서 저장한 OneLink 템플릿으로 링크를 만들어요. 만드는 방법은 '3. MMP에서 트래킹 링크 만들기'의 AppsFlyer 탭 '② 링크 만들기'와 같아요.
2. 이때 `deep_link_value`에 넣은 화면 식별값은 그대로 두고 `https://` 주소로 바꾸지 않아요.
3. 개발팀이 배포한 앱으로 '4. 트래킹 링크 테스트하기'를 다시 해요.

자세한 내용은 [공식 설정 가이드](https://support.appsflyer.com/hc/en-us/articles/207032246-Create-a-OneLink-template)를 참고해 주세요.
{% endtab %}

{% tab title="Adjust" %}
{% hint style="info" %}
**Deep link generator를 쓰기 전에 확인하기**

* **권한**: Admin, Editor, Custom Editor 중 하나의 권한과 등록된 앱이 필요해요. 단, ②에서 Android App Links를 설정하려면 Admin 권한이 있어야 해요. [Android 앱 링크 설정 공식 가이드](https://help.adjust.com/en/article/set-up-android-app-links)
* **사전 요건**: 대상 OS의 iOS Universal Links 또는 Android App Links와 Branded domain 설정이 필요해요. 두 OS를 함께 쓰면 양쪽 설정과 공통 Branded domain을 준비해 주세요. [공식 사전 요건](https://help.adjust.com/en/article/deep-link-generator)
* **진행 순서**: 플랫폼 설정 → 토스용 기본 트래킹 링크 준비 → Deep link generator에서 앱에서 열 화면 연결 순서로 진행해요.
{% endhint %}

**① 개발팀에게 앱 정보 받기**

개발팀에게 아래 값을 받아요. 각 값은 위 '개발팀이 전달할 값 확인하기' 표를 참고해요.

* iOS: App ID Prefix, Bundle ID
* Android: SHA256 Certificate Fingerprint

**② MMP 콘솔에 앱 정보 입력하기**

iOS는 아래 순서로 입력해요.

1. **AppView → All apps → 대상 앱 → Platforms → iOS**로 이동해요.
2. App ID와 Bundle ID가 개발팀에게 받은 값과 같은지 확인해요.
3. **Universal linking → Enable universal linking**을 켜요.
4. **App ID prefix**와 **App scheme**을 입력하고 **Save**해요. App scheme에는 `sampleios`처럼 iOS 앱에 등록된 앱 스킴 이름을 입력해요.

<figure><img src="https://images.ctfassets.net/5s247im0esyq/2yRwE86cgvYaboZwPTvZPJ/e6c2a8999c590e23aed111ed05d35fcf/iOS_app_platform_settings.png" alt="출처: Adjust 플랫폼 설정"><figcaption><p>출처: Adjust 플랫폼 설정</p></figcaption></figure>

Android는 아래 순서로 입력해요.

1. **AppView → All apps → 대상 앱 → Platforms → Android**로 이동해요.
2. **Enable deep links for Android App Links**를 켜요.
3. **SHA-256 certificate fingerprints**와 **App scheme**을 입력하고 **Save**해요. App scheme은 앱에 등록된 스킴 이름을 사용해요.

<figure><img src="https://images.ctfassets.net/5s247im0esyq/2Hly4WfXq8AopyFX7lIWIn/d3f250f7c57f52a9cee1bb948b8dfa22/Android_g_app_platform_settings.png" alt="출처: Adjust 플랫폼 설정"><figcaption><p>출처: Adjust 플랫폼 설정</p></figcaption></figure>

**③ 개발팀에 도메인 전달하기**

Branded domain을 개발팀에 전달해요. 두 OS를 함께 설정한다면 같은 Branded domain을 써요.

* iOS: 개발팀이 이 도메인을 Associated Domains에 등록해요. 이미 `xxx.adj.st`를 등록해 뒀다면 지우지 않고 함께 둬요.
* Android: 개발팀이 이 도메인과 SDK의 앱 링크 처리를 앱에 반영해요.

**④ 링크 만들고 테스트하기**

유니버설 링크·앱 링크를 설정했다면, '3. MMP에서 트래킹 링크 만들기'의 Adjust 탭 '② 링크 만들기'에서 쓴 `deep_link` 방법 대신 **New deep link**(Deep link generator)로 링크를 만들 수도 있어요.

1. **Campaign Lab → Partners**에서 토스 광고에 쓸 Network-level 링크를 고르고 **New deep link**를 열어요.
2. 앱과 기본 링크, 캠페인 값을 확인해요.
3. **Define a deep link → In-app screen**에 개발팀과 정한 앱에서 열 화면을 설정해요.
4. **Add a redirect → App stores**에서 앱을 설치하지 않은 유저가 이동할 스토어 주소를 확인해요.
5. **Generate & view link**로 만든 링크(full Click URL)를 복사해요.
6. 개발팀이 배포한 앱으로 '4. 트래킹 링크 테스트하기'를 다시 해요.

토스 광고에는 토스 파트너에서 만든 Partner 링크를 먼저 사용해요. 자사 채널용 Custom link와 광고 네트워크용 Partner 링크는 구분해 주세요. Custom link나 수동 구성이 필요하다면, 토스 매체 식별값과 '3. MMP에서 트래킹 링크 만들기'의 필수·권장 항목을 유지할 수 있는 방식인지 확인해요. 자세한 내용은 [Deep link generator 공식 가이드](https://help.adjust.com/en/article/deep-link-generator)를 참고해 주세요.

콘솔에 App scheme을 등록한 뒤, 실제 배포 앱에서 링크를 눌러 앱에서 열 화면까지 이동하는지 확인해요. 화면 이동은 콘솔 설정만으로 되지 않고 앱에도 구현돼 있어야 해요. 앱 쪽 설정은 [iOS 도메인 연결](https://help.adjust.com/en/article/set-up-universal-links)과 [Android App Links 설정](https://help.adjust.com/en/article/set-up-android-app-links)을 참고해요.
{% endtab %}

{% tab title="Airbridge" %}
**① 개발팀에게 앱 정보 받기**

개발팀에게 아래 값을 받아요. 각 값은 위 '개발팀이 전달할 값 확인하기' 표를 참고해요.

* iOS: App ID Prefix, Bundle ID
* Android: Package Name, SHA256 Certificate Fingerprint

**② MMP 콘솔에 앱 정보 입력하기**

'3. MMP에서 트래킹 링크 만들기'의 Airbridge 탭 ①에서 앱 정보를 등록한 **Tracking Link → Deep Links** 화면에서 아래 값이 맞는지 확인해요. 앱 스킴은 그대로 둬요.

| OS      | 항목                         | 입력값                          |
| ------- | -------------------------- | ---------------------------- |
| iOS     | iOS App ID                 | `App ID Prefix.Bundle ID` 형식 |
| Android | Android Package Name       | 대상 앱의 Package Name           |
| Android | `sha256_cert_fingerprints` | SHA256 값. 여러 개면 쉼표로 구분해요.    |

**③ 개발팀에 도메인 전달하기**

* **마케팅팀**: **Settings → App Settings**에서 App Name을 확인해 개발팀에 전달해요.
* **개발팀**: App Name으로 만든 아래 두 도메인을 앱에 등록해요. `YOUR_APP_NAME` 자리에는 전달받은 App Name을 넣어요.
  * iOS: Associated Domains에 `applinks:YOUR_APP_NAME.airbridge.io`와 `applinks:YOUR_APP_NAME.abr.ge`를 등록해요.
  * Android: 두 도메인에 앱 링크용 `intent-filter`를 만들고, SDK가 넘겨준 앱 스킴 주소로 화면을 열어요.

개발팀이 도메인을 등록하고 화면을 여는 방법은 사용하는 Airbridge SDK 버전에 따라 달라요. [iOS SDK 가이드](https://help.airbridge.io/en/developers/ios-sdk-v4) · [Android SDK 가이드](https://help.airbridge.io/en/developers/android-sdk-v4)

**④ 링크 만들고 테스트하기**

1. 링크를 만들어요. 만드는 방법은 '3. MMP에서 트래킹 링크 만들기'의 Airbridge 탭 '② 링크 만들기'와 같아요.
2. 이때 **Deep Link** 입력란에는 계속 `sampleios://event/123` 같은 딥링크 주소를 넣어요. 유니버설 링크·앱 링크로 열지 앱 스킴으로 열지는 Airbridge가 휴대폰 환경에 맞춰 골라요.
3. 개발팀이 배포한 앱으로 '4. 트래킹 링크 테스트하기'를 다시 해요.

자세한 내용은 [공식 딥링크 정보 안내](https://help.airbridge.io/en/guides/retargeting-with-deep-links)를 참고해 주세요.
{% endtab %}

{% tab title="Branch" %}
**① 개발팀에게 앱 정보 받기**

개발팀에게 아래 값을 받아요. 각 값은 위 '개발팀이 전달할 값 확인하기' 표를 참고해요.

* iOS: Bundle ID, App ID Prefix
* Android: Package Name, SHA256 Certificate Fingerprint

**② MMP 콘솔에 앱 정보 입력하기**

'3. MMP에서 트래킹 링크 만들기'의 Branch 탭 ①에서 앱 스킴과 스토어 주소를 입력한 **Configuration → Link Controls → Link Routing Rules → Mobile Routing** 화면에서 아래 항목을 켜고 값을 입력해요. 앱 스킴과 스토어 주소는 그대로 둬요.

| OS      | 켤 항목                   | 입력값                                                   |
| ------- | ---------------------- | ----------------------------------------------------- |
| iOS     | Enable Universal Links | Bundle Identifiers, Apple App Prefix                  |
| Android | Enable App Links       | Android Package Name, SHA256 Certificate Fingerprints |

SHA256 값이 여러 개면 **Add another SHA256 fingerprint**로 추가해요.

**③ 개발팀에 도메인 전달하기**

**Link Appearance → Link Domains**에 있는 도메인을 개발팀에 전달해요. 개발팀은 기본 도메인과 `-alternate` 도메인을 iOS Associated Domains와 Android 앱 링크용 `intent-filter`에 모두 등록해요. Custom domain이나 테스트 키를 쓴다면 그 도메인도 함께 등록해요.

각 도메인을 연결하는 조건은 [Branch iOS 도메인 설정](https://help.branch.io/developer-hub/ios-basic-integration)에서 확인해요.

**④ 링크 만들고 테스트하기**

1. 링크를 만들어요. 만드는 방법은 '3. MMP에서 트래킹 링크 만들기'의 Branch 탭 '② 링크 만들기'의 Ad Link 순서와 같아요.
2. 이때 앱에서 열 화면 정보는 그대로 둬요. 유니버설 링크·앱 링크를 추가했다고 강제 실행 옵션(Aggressive)으로 바꾸지 않아요.
3. 개발팀이 배포한 앱으로 '4. 트래킹 링크 테스트하기'를 다시 해요.

자세한 내용은 [공식 Routing 설정](https://help.branch.io/account-hub/link-routing-rules-new)을 참고해 주세요.
{% endtab %}

{% tab title="Singular" %}
**① 개발팀에게 앱 정보 받기**

개발팀에게 아래 값을 받아요. 각 값은 위 '개발팀이 전달할 값 확인하기' 표를 참고해요.

* iOS: Team ID
* Android: SHA256 Certificate Fingerprint

**② MMP 콘솔에 앱 정보 입력하기**

* iOS: **Apps Configuration → 대상 앱 → iOS App site → Show Advanced Settings**에서 **Team ID**를 입력해요. App Scheme은 그대로 둬요.
* Android: **Settings → Apps → 대상 앱 → Android App site → Show Advanced Settings**에서 **App Links SHA256 fingerprints**에 SHA256 값을 입력해요. Android Scheme은 그대로 둬요.

**③ 개발팀에 도메인 전달하기**

Singular 링크 도메인(예: `brand.sng.link`)을 개발팀에 전달해요.

* iOS: 개발팀이 Associated Domains를 켜고 이 도메인을 등록해요.
* Android: 개발팀이 이 도메인에 앱 링크용 `intent-filter`와 SDK 처리를 구현해요. 실제 트래킹 링크의 경로가 `intent-filter`에 포함되는지도 확인해요.

**④ 링크 만들고 테스트하기**

1. 링크를 만들어요. 만드는 방법은 '3. MMP에서 트래킹 링크 만들기'의 Singular 탭 '② 링크 만들기'와 같아요.
2. 이때 딥링크 입력란(If the app is already installed…)에 넣은 `sampleios://event/123` 같은 딥링크 주소는 그대로 두고 `https://` 주소로 바꾸지 않아요.
3. 개발팀이 배포한 앱으로 '4. 트래킹 링크 테스트하기'를 다시 해요.

함께 확인할 점이에요.

* 유니버설 링크를 설정해도 토스 iOS 앱에서는 앱 스킴으로 열어야 해요. '3. MMP에서 트래킹 링크 만들기'의 Singular 탭 '② 링크 만들기'에서 넣은 `_force_redirect=1`은 지우지 않고 그대로 둬요.
* 기존 링크 전환에 대한 공식 예시에는 `/A`, `/B`, `/E`, `/F` 경로가 나와요. 예시를 그대로 복사하지 말고, 실제로 쓰는 링크의 경로가 앱의 처리 범위에 포함되는지 확인해요.
* `_dl`, `_ios_dl`, `_android_dl`을 HTTPS 주소로 한꺼번에 바꾸지 않아요. [공식 Tracking Links FAQ](https://support.singular.net/hc/en-us/articles/360030934212-Singular-Links-Tracking-Links-FAQ)

자세한 내용은 [공식 사전 설정](https://support.singular.net/hc/en-us/articles/360031371451-Singular-Links-Prerequisites)을 참고해 주세요.
{% endtab %}

{% tab title="DFINERY" %}
**① 개발팀에게 앱 정보 받기**

개발팀에게 아래 값을 받아요. 각 값은 위 '개발팀이 전달할 값 확인하기' 표를 참고해요.

* iOS: Team ID, Bundle ID
* Android: SHA256 Certificate Fingerprint

**② MMP 콘솔에 앱 정보 입력하기**

'3. MMP에서 트래킹 링크 만들기'의 DFINERY 탭 ①에서 앱 스킴과 스토어 주소를 입력한 **Attribution → Ad Landing Settings**에 아래 값을 추가해요. 앱 스킴과 스토어 설정은 그대로 둬요.

| OS      | 영역              | 입력값                      |
| ------- | --------------- | ------------------------ |
| iOS     | Universal Links | `Team ID.Bundle ID` 형식   |
| Android | App Links       | SHA256 Cert Fingerprints |

플랫폼별 입력 형식은 [Ad Landing Settings 공식 안내](https://help.dfinery.io/hc/en-us/articles/360003394433-Ad-Landing-Settings-Setting-the-user-s-landing-point)에서 확인해요.

**③ 개발팀에 도메인 전달하기**

DFINERY 트래킹 링크의 도메인을 개발팀에 전달해요. 개발팀은 이 도메인을 iOS Associated Domains와 Android 앱 링크용 `intent-filter`에 등록하고, SDK로 화면을 여는 처리를 구현해요.

**④ 링크 만들고 테스트하기**

1. 링크를 **Download + Deeplink** 형식으로 만들어요. 만드는 방법은 '3. MMP에서 트래킹 링크 만들기'의 DFINERY 탭 '② 링크 만들기'와 같아요.
2. 이때 앱 스킴과 앱에서 열 화면 경로는 그대로 둬요.
3. 개발팀이 배포한 앱으로 '4. 트래킹 링크 테스트하기'를 다시 해요.

자세한 내용은 [공식 딥링크 연결 안내](https://help.dfinery.io/hc/en-us/articles/360039757433-Deep-Link-Understanding-and-Differentiating-URI-Scheme-Universal-Link-and-App-Link)를 참고해 주세요.
{% endtab %}
{% endtabs %}

### 테스트할 때 함께 확인하기 <a href="#ul-test-checks" id="ul-test-checks"></a>

각 MMP 탭의 ④에서 테스트할 때 아래 내용도 함께 확인해요.

* 확인창이나 브라우저가 나타났다는 이유만으로 설정 오류라고 판단하지 않아요. 최종적으로 앱이나 스토어에 도착하는지 확인해요.
* 기대한 대로 이동하지 않으면 MMP 콘솔과 앱에 등록한 도메인, 앱 식별 정보, 배포 인증서가 서로 일치하는지 확인해요.
