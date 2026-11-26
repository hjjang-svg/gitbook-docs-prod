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

앱 설치 유도하기 광고에는 광고 성과 측정에 필요한 값이 포함된 MMP 트래킹 링크가 필요해요.

앱 스킴, 유니버설 링크(iOS), 앱 링크(Android)를 구현하지 않아도 광고를 집행할 수 있어요. 다만 앱으로 바로 연결되지 않으면 이미 앱을 설치한 유저도 스토어에서 ‘열기’를 눌러야 해요.

유저가 더 편리하게 앱에 도착할 수 있도록 앱 스킴과 유니버설 링크·앱 링크 설정을 강력히 권장해요. 이 가이드에서는 MMP 트래킹 링크를 준비하고, 앱 연결 방식을 설정한 뒤 실제 동작을 확인하는 방법을 안내해요.

{% hint style="info" %}
**광고 성과 측정과 앱 연결 설정은 구분해요.**

MMP 트래킹 링크와 필수 측정값은 반드시 준비해요. 앱 직접 연결은 권장 설정이에요. 앱이 정상적으로 열려도 필수 측정값이 누락되거나 잘못 설정돼 있으면 수정해야 해요.
{% endhint %}

소재 규격과 링크 제출 규칙은 [앱 설치 유도하기 소재 가이드](creative.md)를 참고해 주세요.

## 이 가이드에서 쓰는 용어 <a href="#terms" id="terms"></a>

| 용어           | 뜻                                     | 예시                                     |
| ------------ | ------------------------------------- | -------------------------------------- |
| MMP 트래킹 링크   | 광고 클릭과 전환 측정에 사용하는 링크                 | MMP에서 발급한 토스용 클릭 URL                   |
| 앱 스킴 이름      | 앱에 등록한 스킴 이름                          | sampleios, sampleandroid               |
| 앱 실행 주소      | 앱 스킴으로 앱을 실행하는 주소                     | sampleios://                           |
| 딥링크 주소       | 앱에서 열 화면을 가리키는 주소. 아래 예시는 앱 스킴 방식이에요. | sampleios://event/123                  |
| 화면 경로        | 위 예시에서 앱 실행 주소 뒤에 붙는 경로               | event/123                              |
| 유니버설 링크·앱 링크 | 앱과 연결된 HTTPS 주소로 앱을 여는 방식             | iOS Universal Links, Android App Links |
| 스토어 목적지      | 광고 대상 앱의 다운로드·열기 화면                   | App Store·Google Play의 광고 대상 앱 페이지     |

예시 값 대신 실제 앱에 구현된 값을 넣어 주세요. MMP 콘솔마다 앱 스킴 이름(예: sampleios)을 넣는 입력란도 있고, 전체 주소(예: sampleios://, sampleios://event/123)를 넣는 입력란도 있어요. 입력란 설명을 보고 맞는 형식으로 넣어 주세요.

## 한눈에 보기 <a href="#overview" id="overview"></a>

| 단계                   | 담당       | 할 일                                    |
| -------------------- | -------- | -------------------------------------- |
| 1. MMP에서 트래킹 링크 만들기  | 마케팅팀     | 토스용 클릭 링크를 만들고 필수 측정값과 목적지를 확인해요.      |
| 2. (권장) 앱 직접 연결 설정하기 | 개발팀·마케팅팀 | 앱 스킴, 유니버설 링크·앱 링크를 구현하고 MMP 링크에 적용해요. |
| 3. 최종 링크 테스트하기       | 마케팅팀·개발팀 | 설치 전후의 앱·스토어 도착과 측정 설정을 각각 확인해요.       |

이미 앱 직접 연결 설정을 사용하고 있다면 정상 동작하는 설정을 유지해요. 새로 구현한다면 2단계를 진행한 뒤 1단계에서 만든 링크에 반영하고 테스트해요. 한쪽 OS만 광고한다면 광고할 OS의 값만 준비하면 돼요.

## 1. MMP에서 트래킹 링크 만들기 <a href="#step1-create-link" id="step1-create-link"></a>

사용하는 MMP에서 토스를 광고 파트너 또는 매체로 선택하고 **클릭용 트래킹 링크**를 만들어요. 노출용 링크가 함께 발급되더라도 소재 등록과 클릭 테스트에는 클릭용 링크를 사용해요.

### 시작하기 전에 <a href="#before-you-start" id="before-you-start"></a>

* MMP의 토스 파트너 연동을 완료해요.
* 앱의 MMP SDK와 필요한 이벤트 설정을 완료해요.
* 광고 대상 앱과 OS별 스토어 주소를 확인해요. MMP가 요구하는 Package Name·Bundle ID·App Store ID가 실제 광고 대상 앱과 일치하는지도 확인해요.
* 앱 직접 연결을 사용한다면 구현이 반영된 배포 앱과 설정값을 준비해요.

링크에 파라미터를 넣는 것만으로 SDK·이벤트 연동이 완료되지는 않아요. [MMP 연동 가이드](../../tracking/mat/)를 함께 확인해 주세요.

### 링크 생성 방법 <a href="#create-link-method" id="create-link-method"></a>

**MMP의 토스용 링크 생성 기능을 사용하는 방법을 권장해요.**

1. MMP 콘솔에서 토스(Toss)를 광고 파트너 또는 매체로 선택해요.
2. 광고 대상 앱과 스토어 목적지를 확인하고 클릭용 링크를 만들어요.
3. 아래 MMP별 측정값 표와 최종 링크를 대조해요.
4. 앱 직접 연결을 사용한다면 앱 스킴·유니버설 링크 설정이 최종 링크에 반영됐는지도 확인해요.

자동 생성으로 필요한 설정을 반영하기 어렵다면 MMP가 지원하는 수동 설정을 사용할 수 있어요. 수동으로 설정할 때도 토스 매체 식별값과 필수 측정값은 유지해야 해요. 자사 채널용 Custom Source나 newsletter 같은 예시 매체값으로 바꾸지 않아요.

### 매크로와 파라미터 확인하기 <a href="#macros-and-parameters" id="macros-and-parameters"></a>

* 중괄호로 감싼 매크로는 실제 광고 노출·클릭 시 값이 들어갈 자리예요. 대소문자와 중괄호를 유지하고 임의의 테스트 값으로 바꾸지 않아요.
* 이미 있는 파라미터를 중복으로 추가하지 않아요. 잘못된 값이 있다면 기존 값을 수정해요.
* 다른 URL을 파라미터 값으로 넣을 때는 넣는 URL만 인코딩해요. 트래킹 링크 전체를 인코딩하지 않아요.
* 필수 측정값은 모두 포함하고 권장 측정값도 함께 적용해 주세요.
* 광고 ID는 OS와 MMP가 지원하는 항목·매크로에 맞춰 설정해요. 검수 기기에서 광고 ID 실제 값을 얻지 못하는 경우와 링크의 매체·클릭·캠페인 설정 오류는 구분해요. 광고 ID 템플릿 설정과 실제 집행 시 측정·전환 수신은 별도로 확인해요.
* 아래 표는 링크의 측정값이에요. 설치·구매 결과를 보내는 이벤트 포스트백의 파라미터와 구분해요.

### MMP별 링크 설정 <a href="#mmp-link-setup" id="mmp-link-setup"></a>

아래에서 사용하는 MMP를 선택해요. **기본 링크 생성 → 측정값 점검** 순서로 안내해요. 앱 직접 연결을 사용하지 않는 경우에도 기본 링크와 스토어 목적지, 측정값은 확인해야 해요.

메뉴 이름은 콘솔 언어와 업데이트에 따라 다를 수 있어요. 아래 이미지는 MMP 공식 문서와 콘솔의 참고 화면이에요. 예시 값 대신 실제 앱의 값을 입력하고, 사용하는 기능에 해당하는 설정만 적용해요. 토스의 앱 직접 연결 권장 정책과 별개로, MMP의 특정 기능을 선택하면 MMP가 그 기능에 요구하는 SDK·앱·콘솔 사전 요건을 갖춰야 해요.

{% tabs %}
{% tab title="AppsFlyer" %}
**① 기본 링크 만들기**

1. Active Integrations → Toss → Attribution link에서 Click attribution link를 확인해요.
2. 광고 대상 앱과 스토어 목적지가 맞는지 확인해요.
3. OneLink를 쓴다면 OneLink 템플릿의 앱·스토어 설정도 확인해요.
4. 아래 표와 최종 링크의 측정값을 대조해요.

Custom link로 만드는 경우 **Engage → OneLink management → 사용할 템플릿 → Add link**에서 설정해요. 최종 링크의 토스 매체값 `pid=tossa3u_int`와 캠페인 매크로를 유지해요. 콘솔에서 토스용 값을 유지할 수 없다면 Toss 파트너 링크 설정을 확인해 주세요.

<figure><img src="https://support.appsflyer.com/hc/article_attachments/50900375410065" alt=""><figcaption><p>AppsFlyer Attribution link 파라미터 입력 화면 (다른 매체 360 Ads 예시, 출처: <a href="https://support.appsflyer.com/hc/en-us/articles/360002152957-360-Ads-campaign-configuration">AppsFlyer - 360 Ads campaign configuration</a>)</p></figcaption></figure>

**OneLink를 사용하는 경우의 참고 화면**

아래는 템플릿 관리·추가 화면이에요. OneLink를 사용하는 경우에 참고하고, 앱 스킴 연결은 2단계에서 설정해요.

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2F3JstqDtsM8HPS8EeWFmX%2Furlguide-01.png?alt=media" alt=""><figcaption><p>AppsFlyer 원링크 관리(OneLink management) 화면 (출처: AppsFlyer 콘솔 캡처)</p></figcaption></figure>

<figure><img src="https://support.appsflyer.com/hc/article_attachments/360009665478" alt=""><figcaption><p>AppsFlyer OneLink 템플릿 추가 화면 (출처: <a href="https://support.appsflyer.com/hc/en-us/articles/207032246-Create-a-OneLink-template">AppsFlyer - Create a OneLink template</a>)</p></figcaption></figure>

**② 측정값 확인하기**

| 구분 | 항목                     | 값                     |
| -- | ---------------------- | --------------------- |
| 필수 | pid                    | tossa3u\_int          |
| 필수 | clickid                | {TOSS\_TK\_CLICK\_ID} |
| 필수 | advertising\_id / idfa | {USER\_ADID}          |
| 필수 | af\_c\_id              | {TOSS\_CID}           |
| 권장 | af\_ad\_id             | {TOSS\_CREATIVE\_ID}  |
| 권장 | af\_siteid             | {SITE\_ID}            |
| 권장 | af\_adset              | {ADGROUP\_NAME}       |
| 권장 | af\_ad                 | {CREATIVE\_NAME}      |
| 권장 | c                      | {CAMPAIGN\_NAME}      |

[토스애즈 AppsFlyer 가이드](../../tracking/mat/appsflyer "relative-link") · [OneLink template 설정](https://support.appsflyer.com/hc/en-us/articles/207032246-Create-a-OneLink-template) · [OneLink 링크 생성](https://support.appsflyer.com/hc/en-us/articles/208874366-Create-deep-linking-and-redirection-links-for-your-campaigns-with-OneLink)
{% endtab %}

{% tab title="Adjust" %}
**① 기본 링크 만들기**

Campaign Lab → Partners에서 Toss 연동을 확인하고 토스용 기본 클릭 링크를 만들어요. 광고 대상 앱과 OS별 스토어 목적지를 확인해요. 수동으로 구성하더라도 토스 매체와 측정값을 유지해요.

아래 이미지는 Adjust의 CTV 캠페인 문서에 실린 구형 UI 화면이에요. 구형 UI의 New ad network는 Adjust Toss 설정 절차의 Partners → New partner와 같은 메뉴이고, 여기서 Toss를 선택해요. 진입 메뉴만 참고하고, 이미지 출처 문서의 CTV·Cross-device 설정은 적용하지 않아요.

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FS9j27RUEpuwI4UjH1v7F%2Furlguide-02.png?alt=media" alt=""><figcaption><p>Adjust 구형 Campaign Lab에서 광고 네트워크 설정을 시작하는 화면 (출처: <a href="https://help.adjust.com/en/article/measure-connected-tv-mobile-campaigns">Adjust - Measure CTV campaigns</a> · <a href="https://help.adjust.com/en/partner-setup/toss">Adjust - Toss 설정 절차</a>)</p></figcaption></figure>

**② 측정값 확인하기**

| 구분 | 항목                 | 값                     |
| -- | ------------------ | --------------------- |
| 필수 | toss\_click\_id    | {TOSS\_TK\_CLICK\_ID} |
| 필수 | idfa / gps\_adid   | {IDFA} / {AIFA}       |
| 필수 | toss\_campaign\_id | {TOSS\_CID}           |
| 권장 | toss\_creative\_id | {TOSS\_CREATIVE\_ID}  |
| 권장 | toss\_site\_id     | {SITE\_ID}            |
| 권장 | campaign           | {CAMPAIGN\_NAME}      |
| 권장 | adgroup            | {ADGROUP\_NAME}       |

Adjust의 .[go.link](http://go.link)·.[adj.st](http://adj.st) 발급 결과에 adj\_·adjust\_ 접두어가 있다면 발급된 형식을 유지해요. 표와 달라 보인다는 이유만으로 접두어를 지우거나 같은 값을 추가하지 않아요. URL에 보이지 않는 설정은 원래 링크나 발급 설정에서 확인해요.

[토스애즈 Adjust 가이드](../../tracking/mat/adjust "relative-link") · [Link parameters](https://help.adjust.com/en/article/link-parameters) · [Deep link generator](https://help.adjust.com/en/article/deep-link-generator)
{% endtab %}

{% tab title="Airbridge" %}
**① 기본 링크 만들기**

1. Settings → App Settings → App Info → Platform에서 앱을 선택하거나 스토어 URL을 등록해요.
2. Tracking Link → Link Generation → Integrated Channels에서 Channel을 Toss로 선택해요. 채널에 미리 설정된 측정값은 유지해요.
3. 앱 직접 연결을 사용하지 않는다면 Redirection의 Destination을 **App Store**로 선택해요. iOS는 광고 대상 앱의 App Store, Android는 Google Play로 설정해요.
4. Create tracking link로 생성한 링크 중 Click 링크를 복사하고 토스 채널 경로와 측정값을 점검해요.

[Airbridge 공식 링크 생성 가이드](https://help.airbridge.io/en/guides/creating-tracking-links-on-the-dashboard)

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FQERlpbIIuAuq9OWTT5Fq%2Furlguide-03.png?alt=media" alt=""><figcaption><p>Airbridge 캠페인 파라미터 입력 및 링크 미리보기 화면 (출처: <a href="https://help.airbridge.io/en/guides/creating-tracking-links-on-the-dashboard">Airbridge - Creating tracking links</a>)</p></figcaption></figure>

**② 측정값 확인하기**

| 구분 | 항목               | 값                     |
| -- | ---------------- | --------------------- |
| 필수 | URL 경로           | /toss                 |
| 필수 | click\_id        | {TOSS\_TK\_CLICK\_ID} |
| 필수 | ad\_id           | {USER\_ADID}          |
| 필수 | campaign\_id     | {TOSS\_CID}           |
| 권장 | sub\_id          | {SITE\_ID}            |
| 권장 | ad\_creative\_id | {TOSS\_CREATIVE\_ID}  |
| 권장 | campaign         | {CAMPAIGN\_NAME}      |
| 권장 | ad\_group        | {ADGROUP\_NAME}       |
| 권장 | ad\_creative     | {CREATIVE\_NAME}      |

/toss는 URL 경로예요. path=/toss 같은 별도 파라미터를 추가하지 않아요.

[토스애즈 Airbridge 가이드](../../tracking/mat/airbridge "relative-link") · [딥링크 설정](https://help.airbridge.io/ko/guides/retargeting-with-deep-links)
{% endtab %}

{% tab title="Branch" %}
**① 기본 링크 만들기**

1. 토스 광고 파트너를 활성화해요.
2. LinkHub → Create Link → Ad Link에서 App Only → App Install or Engagement를 선택해요.
3. Define → Configure Options에서 링크 이름과 토스 파트너를 선택해요.
4. Link Alias와 캠페인 정보를 설정하고 Redirects의 스토어 목적지를 확인해요.
5. Create Link Now → Validate & Share에서 오류를 확인한 뒤 클릭용 링크를 복사해요.

아래 두 이미지는 기존 콘솔의 Criteo 예시 화면이에요. 지금 콘솔에서는 2번 단계처럼 LinkHub → Create Link → Ad Link로 들어가고, 파트너는 Criteo 대신 Toss를 선택해요.

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2F2iTYjSuk6uq6suOVXmqI%2Furlguide-04.png?alt=media" alt=""><figcaption><p>Branch 기존 콘솔의 Create Ad Link → App Only → App Install or Engagement 선택 화면 (Criteo 예시, 출처: <a href="https://help.branch.io/marketer-hub/criteo">Branch - Criteo</a>)</p></figcaption></figure>

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FSrq6co4UGuqJkISqcEpZ%2Furlguide-05.png?alt=media" alt=""><figcaption><p>링크 이름·Ad Partner·App Only 형식을 확인하고 Configure Options로 넘어가는 Branch 기존 콘솔의 Define 화면 (Criteo 예시, 출처: <a href="https://help.branch.io/marketer-hub/criteo">Branch - Criteo</a>)</p></figcaption></figure>

**② 측정값 확인하기**

| 구분 | 항목             | 값                     |
| -- | -------------- | --------------------- |
| 필수 | $3p            | a\_toss               |
| 필수 | \~click\_id    | {TOSS\_TK\_CLICK\_ID} |
| 필수 | \~campaign\_id | {TOSS\_CID}           |
| 필수 | $aaid          | {aaid}                |
| 필수 | $idfa          | {idfa}                |
| 권장 | \~creative\_id | {TOSS\_CREATIVE\_ID}  |
| 권장 | \~channel      | {SITE\_ID}            |

항목 이름의 $·\~와 매크로 대소문자를 유지해요. Validate & Share 통과 후에도 실제 기기에서 테스트해요.

[토스애즈 Branch 가이드](../../tracking/mat/branch "relative-link") · [Ad Links](https://help.branch.io/marketer-hub/ad-links) · [Routing 설정](https://help.branch.io/account-hub/link-routing-rules-new)
{% endtab %}

{% tab title="Singular" %}
**① 기본 링크 만들기**

1. Attribution → Manage Links → Create Link에서 대상 앱을 선택해요.
2. 광고 네트워크용 Partner를 선택하고 Source Name에 토스 매체를 설정해요.
3. Tracking Link Name과 링크 도메인, 대상 OS를 설정해요.
4. OS별 App Store·Google Play 목적지를 확인해요.
5. Save 후 Link Summary에서 Click-through link를 복사해요.

토스 광고 링크를 자사 채널용 Custom Source로 만들지 않아요. 스토어로만 연결하려면 딥링크 목적지를 설정하지 않은 상태로 링크를 생성해요. [공식 FAQ](https://support.singular.net/hc/en-us/articles/360030934212-Singular-Links-Tracking-Links-FAQ)

아래 이미지는 다른 매체(Adikteev) 예시예요. 이미지의 매체명과 re-engagement 설정은 그대로 따라 하지 않아요.

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FL70jrfZm5x64TjssLIcd%2Furlguide-06.png?alt=media" alt=""><figcaption><p>Singular Create Link에서 Link Type, Source Name, Tracking Link Name을 입력하는 화면 (Adikteev 예시, 출처: <a href="https://support.singular.net/hc/en-us/articles/22706866069787-Adikteev-Attribution-Integration">Singular - Adikteev Attribution Integration</a>)</p></figcaption></figure>

**② 측정값 확인하기**

| 구분 | 항목                   | 값                              |
| -- | -------------------- | ------------------------------ |
| 필수 | cl                   | {TOSS\_TK\_CLICK\_ID}          |
| 필수 | idfa / aifa / ad\_id | {IDFA} / {AIFA} / {USER\_ADID} |
| 필수 | pcid                 | {TOSS\_CID}                    |
| 권장 | pcrid                | {TOSS\_CREATIVE\_ID}           |
| 권장 | site\_id             | {SITE\_ID}                     |
| 권장 | pcn                  | {CAMPAIGN\_NAME}               |
| 권장 | pcrn                 | {CREATIVE\_NAME}               |
| 권장 | pscn                 | {ADGROUP\_NAME}                |

[토스애즈 Singular 가이드](../../tracking/mat/singular "relative-link") · [Tracking Links 생성](https://support.singular.net/hc/en-us/articles/13000445013531-How-to-Build-Tracking-Links) · [딥링크 설정](https://support.singular.net/hc/en-us/articles/360050910891-How-to-Configure-Deep-Links)
{% endtab %}

{% tab title="DFINERY" %}
**① 기본 링크 만들기**

1. Attribution → Ad Landing Settings에서 광고 대상 앱의 OS별 default URL과 앱 식별 정보를 확인해요.
2. Attribution → Ad partner settings에서 토스 매체를 활성화해요.
3. Attribution → Ad Campaign에서 캠페인을 만들어요.
4. Tracking Link 탭에서 토스 매체를 선택하고 Connect with Ad Campaign으로 연결해요.
5. 딥링크를 사용하지 않으면 랜딩 형식에서 **Download**를 선택해요. 설치 여부와 관계없이 스토어로 이동하는 형식이에요.
6. Ad-Touch Landing의 목적지가 광고 대상 앱의 스토어인지 확인한 뒤 클릭용 링크를 복사해요.

앱 직접 연결을 사용하지 않더라도 스토어 목적지는 필요해요. 콘솔이 요구하는 PC default URL 등 추가 항목은 DFINERY 설정 기준을 따라요.

<figure><img src="https://help.dfinery.io/hc/article_attachments/14979511559705" alt=""><figcaption><p>DFINERY Ad Campaign 생성 절차 화면(GIF) (출처: <a href="https://help.dfinery.io/hc/en-us/articles/360024465693-Create-Ad-Campaign-and-Issue-Tracking-Link">DFINERY - Create Ad Campaign and Issue Tracking Link</a>)</p></figcaption></figure>

<figure><img src="https://help.dfinery.io/hc/article_attachments/4411974403609" alt=""><figcaption><p>DFINERY 랜딩 형식에서 Download를 선택하는 화면 (출처: <a href="https://help.dfinery.io/hc/en-us/articles/360024465693-Create-Ad-Campaign-and-Issue-Tracking-Link">DFINERY - Create Ad Campaign and Issue Tracking Link</a>)</p></figcaption></figure>

**매체 연결·클릭 링크 발급·스토어 목적지 참고 화면**

앱 직접 연결을 사용하지 않는 경우 Download를 선택하고 스토어 목적지를 확인해요. 아래 목적지 화면의 예시 URL을 그대로 사용하지 않아요.

<figure><img src="https://help.dfinery.io/hc/article_attachments/15001194947609" alt=""><figcaption><p>DFINERY 캠페인에 매체를 연결하는 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360024465693">DFINERY - Ad Campaign 생성과 Tracking Link 발급</a>)</p></figcaption></figure>

<figure><img src="https://help.dfinery.io/hc/article_attachments/15075316676249" alt=""><figcaption><p>DFINERY 클릭용·노출용 트래킹 링크 발급 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360024465693">DFINERY - Ad Campaign 생성과 Tracking Link 발급</a>)</p></figcaption></figure>

<figure><img src="https://help.dfinery.io/hc/article_attachments/15050040003097" alt=""><figcaption><p>DFINERY Ad-Touch Landing 설정 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360024465693">DFINERY - Ad Campaign 생성과 Tracking Link 발급</a>)</p></figcaption></figure>

**② 측정값 확인하기**

| 구분 | 항목          | 값                     |
| -- | ----------- | --------------------- |
| 필수 | cb\_1       | {TOSS\_TK\_CLICK\_ID} |
| 필수 | m\_adid     | {USER\_ADID}          |
| 필수 | m\_ad       | {TOSS\_CID}           |
| 권장 | m\_creative | {TOSS\_CREATIVE\_ID}  |
| 권장 | m\_campaign | {CAMPAIGN\_NAME}      |
| 권장 | cb\_2       | {SITE\_ID}            |
| 권장 | cb\_3       | {CREATIVE\_NAME}      |
| 권장 | m\_adgroup  | {ADGROUP\_NAME}       |

[토스애즈 DFINERY 가이드](../../tracking/mat/dfinery "relative-link") · [Ad Landing Settings](https://help.dfinery.io/hc/ko/articles/360003394433) · [캠페인·Tracking Link 발급](https://help.dfinery.io/hc/ko/articles/360024465693)
{% endtab %}
{% endtabs %}

## 2. (권장) 앱 직접 연결 설정하기 <a href="#step2-direct-link" id="step2-direct-link"></a>

앱 직접 연결을 설정하면 유저가 스토어를 거치는 단계를 줄일 수 있어요. 앱 스킴과 유니버설 링크·앱 링크를 함께 준비하는 것을 강력히 권장해요.

이미 사용하는 설정은 유지해요. 권장 항목으로 바뀌었다는 이유로 정상 동작하는 앱 스킴이나 도메인 연결을 삭제하지 않아요.

### 앱 직접 연결에 필요한 정보 준비하기 <a href="#direct-link-info" id="direct-link-info"></a>

앱 직접 연결을 사용할 때 개발팀에게 아래 값을 받아요. 이미 구현돼 있다면 실제 배포 버전의 값을 확인해요. 아직 구현하지 않았다면 아래 구현 안내를 진행해요.

| 사용할 기능       | 준비할 정보                     |
| ------------ | -------------------------- |
| 앱 스킴         | OS별 앱 스킴 이름·앱 실행 주소        |
| 특정 화면 연결     | OS별 딥링크 주소·화면 경로 또는 화면 식별값 |
| 유니버설 링크·앱 링크 | 연결 도메인·앱 식별 정보·플랫폼별 인증서 정보 |
| 공통           | 구현이 반영된 배포 앱 버전            |

앱 스킴 주소를 임의로 만들어 입력하지 않아요. 콘솔이 요구하는 이름·주소 형식을 구분해요.

### 앱 스킴 구현하기 <a href="#app-scheme-setup" id="app-scheme-setup"></a>

개발팀이 앱 스킴을 등록하고, 전달받은 주소에 맞는 화면을 열도록 구현해요. 앱이 종료된 상태와 실행 중인 상태를 모두 처리하고 MMP SDK의 URL 수신·딥링크 콜백을 연결해요.

**iOS**

Xcode의 Target → Info → URL Types 또는 Info.plist에 앱 스킴 이름을 등록해요.

```xml
<key>CFBundleURLTypes</key>
<array>
  <dict>
    <key>CFBundleURLSchemes</key>
    <array><string>sampleios</string></array>
  </dict>
</array>
```

앱 구조에 맞는 URL 수신 지점에서 허용한 host·path를 확인하고 화면 이동과 SDK 처리를 연결해요. SwiftUI에서는 onOpenURL 등 앱 구조에 맞는 수신 방식을 사용해요. [Apple 앱 스킴 가이드](https://developer.apple.com/documentation/xcode/defining-a-custom-url-scheme-for-your-app)

**Android**

링크를 받을 Activity에 앱 스킴용 intent-filter를 등록해요. 아래 코드는 구조 예시이며 실제 앱의 Activity와 스킴으로 바꿔요.

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

onCreate와 onNewIntent 등 앱 실행 방식에 맞는 지점에서 주소를 처리해요. 허용한 주소인지 확인한 뒤 화면 이동과 SDK 처리를 연결해요. [Android 딥링크 가이드](https://developer.android.com/training/app-links/deep-linking)

개발팀이 배포를 마치면 마케팅팀에 OS별 앱 스킴 이름·앱 실행 주소·딥링크 주소와 적용 버전을 전달해요. 마케팅팀은 아래 MMP별 앱 연결 설정에 반영해요.

### MMP별 앱 직접 연결 설정 <a href="#mmp-direct-link" id="mmp-direct-link"></a>

앱 구현을 마쳤다면 1단계에서 만든 링크에 아래 설정을 반영해요. 유니버설 링크·앱 링크는 이어지는 도메인 연결 안내도 확인해요.

{% tabs %}
{% tab title="AppsFlyer" %}
앱 스킴으로 연결하려면 OneLink template의 Edit → When app is installed → Android and iOS fallback에서 URI scheme을 설정해요. 입력한 앱 실행 주소가 실제 배포 앱에 등록돼 있어야 해요.

| 항목                  | 적용할 때             | 값              |
| ------------------- | ----------------- | -------------- |
| af\_dp              | 앱 스킴 연결           | 앱 실행 주소        |
| af\_force\_deeplink | 앱 스킴 연결           | true           |
| deep\_link\_value   | 특정 화면 연결          | 개발팀과 정한 화면 식별값 |
| deep\_link\_sub1 등  | 추가 화면 데이터가 필요한 경우 | 앱이 처리하도록 구현한 값 |

af\_dp와 af\_force\_deeplink=true는 앱 스킴 연결에 함께 사용하는 권장 설정이에요. 모든 광고 링크의 공통 제출 필수값은 아니에요. 앱 스킴 연결을 적용한다면 자동 생성 링크도 두 값을 확인하고, 빠진 값은 추가해요. 이미 있는 키를 중복으로 넣지 않아요.

deep\_link\_value는 앱 실행 주소와 역할이 달라요. 앱이 읽도록 구현한 형식을 개발팀과 확인해요. 특정 화면 연결에는 SDK와 앱의 화면 이동 처리도 필요해요.

한 OneLink 템플릿에 iOS·Android 앱 스킴을 함께 설정하는 경우 두 앱의 스킴 이름 등 템플릿 요건을 확인해요. 유니버설 링크·앱 링크의 도메인 설정은 2단계를 참고해요.\
**앱 스킴 fallback 설정 화면**

<figure><img src="https://support.appsflyer.com/hc/article_attachments/18363965490833" alt=""><figcaption><p>AppsFlyer 앱 설치 상태의 링크 동작(When app is installed) 설정 화면 (출처: <a href="https://support.appsflyer.com/hc/en-us/articles/207032246-Create-a-OneLink-template">AppsFlyer - Create a OneLink template</a>)</p></figcaption></figure>
{% endtab %}

{% tab title="Adjust" %}
앱 스킴으로 연결한다면 개발팀이 전달한 OS별 딥링크 주소를 기본 트래킹 링크의 deep\_link에 설정해요.

1. 토스용 측정값이 포함된 기본 트래킹 링크를 준비해요.
2. 딥링크 주소만 URL 인코딩해요.
3. 기본 링크에 deep\_link를 추가해요. 이미 쿼리가 있으면 &를, 없으면 ?를 사용해요.
4. OS별 목적지와 설치 전후 동작을 모두 확인해요.

예: sampleios://event/123 → sampleios%3A%2F%2Fevent%2F123

기존 스토어 목적지와 측정값을 삭제하지 않아요. AppView → All apps → 대상 앱 → Platforms의 App scheme 입력란에는 앱 스킴 이름을 입력하며, deep\_link에 넣는 전체 주소와 구분해요.

Deep link generator를 사용하려면 기존 기본 링크와 권한 외에도 Branded domain, iOS Universal Links 또는 Android App Links 설정이 필요해요. Deep link generator의 플랫폼 설정에는 App scheme도 필요해요. 이 기능의 사전 요건은 2단계와 공식 문서를 확인해요.\
**플랫폼 설정 참고 화면**

유니버설 링크·앱 링크 기능을 사용할 때 입력하는 항목이 함께 보이는 화면이에요. 앱 스킴 없이 기본 트래킹 링크만 만드는 경우의 필수 설정 화면은 아니에요.

<figure><img src="https://images.ctfassets.net/5s247im0esyq/2yRwE86cgvYaboZwPTvZPJ/e6c2a8999c590e23aed111ed05d35fcf/iOS_app_platform_settings.png" alt=""><figcaption><p>Adjust iOS 플랫폼 설정 화면 (출처: <a href="https://help.adjust.com/en/article/platforms-ios-android-amazon-microsoft">Adjust - Connect your platform</a>)</p></figcaption></figure>

<figure><img src="https://images.ctfassets.net/5s247im0esyq/2Hly4WfXq8AopyFX7lIWIn/d3f250f7c57f52a9cee1bb948b8dfa22/Android_g_app_platform_settings.png" alt=""><figcaption><p>Adjust Android 플랫폼 설정 화면 (출처: <a href="https://help.adjust.com/en/article/platforms-ios-android-amazon-microsoft">Adjust - Connect your platform</a>)</p></figcaption></figure>
{% endtab %}

{% tab title="Airbridge" %}
앱 직접 연결을 사용한다면 Tracking Link → Deep Links에서 앱 정보를 등록해요.

* Android URL Scheme / iOS URL Scheme에는 실제 앱 실행 주소를 ://까지 포함해 입력해요.
* Android Package Name과 배포 앱의 SHA256 인증서 지문을 확인해요.
* iOS App ID는 App ID Prefix.Bundle ID 형식으로 입력해요.
* 앱에는 사용하는 Airbridge SDK에 맞는 딥링크·화면 이동 처리를 구현해요.

직접 링크를 구성할 때는 Tracking Link → Link Generation → Redirection에서 App (Deep Link) 목적지를 선택하고 OS별 딥링크 주소를 설정해요. App (Deep Link) 목적지는 앱 직접 연결을 사용할 때만 설정해요.

앱 스킴과 인증서·앱 식별 정보는 Airbridge 딥링크 기능을 쓸 때 필요한 설정이에요. 이미 등록된 값은 유지해요. 앱 직접 연결을 사용하지 않는다면 스토어로 도착하는 기본 클릭 링크를 준비하고 실제 동작을 확인해요.\
**App (Deep Link) 목적지·주소 입력 화면**

아래는 앱 직접 연결을 적용하는 경우의 예시예요. 스토어로만 연결하려면 1단계의 App Store 목적지를 사용해요. 상품 매크로는 캠페인이 상품 매크로를 지원할 때만 사용해요.

<figure><img src="https://mintcdn.com/airbridge-help-center/C5DxUFZdlJVt7nU9/asset/image/tracking-link-destination-type-ko.png?w=1650&#x26;fit=max&#x26;auto=format&#x26;n=C5DxUFZdlJVt7nU9&#x26;q=85&#x26;s=5784746ef26accb5ea27262bf2c8395c" alt=""><figcaption><p>Airbridge 트래킹 링크의 최종 목적지 선택 화면 (출처: <a href="https://help.airbridge.io/ko/guides/retargeting-with-deep-links">Airbridge - 딥링크와 에어브릿지 매크로 활용하기</a>)</p></figcaption></figure>

<figure><img src="https://mintcdn.com/airbridge-help-center/jbQGnhL6LTf4bTuy/asset/image/deep-link-macro-redirect-path-ko.png?w=1650&#x26;fit=max&#x26;auto=format&#x26;n=jbQGnhL6LTf4bTuy&#x26;q=85&#x26;s=cb9fd96148ae56d66a73c3cc47a22583" alt=""><figcaption><p>Airbridge 딥링크 주소 입력 화면 (출처: <a href="https://help.airbridge.io/ko/guides/retargeting-with-deep-links">Airbridge - 딥링크와 에어브릿지 매크로 활용하기</a>)</p></figcaption></figure>
{% endtab %}

{% tab title="Branch" %}
Configuration → Link Controls → Link Routing Rules → Mobile Routing에서 실제 앱의 URI Scheme을 등록해요. 구버전 콘솔은 Configuration → Link Settings로 보일 수 있어요.

| 설정                                  | 내용                                   |
| ----------------------------------- | ------------------------------------ |
| Android URI Scheme / iOS URI Scheme | OS별 앱 실행 주소                          |
| Android URL / iOS URL               | 광고 대상 앱의 스토어 주소                      |
| Android Package Name                | 광고 대상 앱의 Package Name                |
| URI scheme deep link mode           | 앱 스킴 연결을 사용하는 경우 Intelligent 기준으로 확인 |

특정 화면을 연결한다면 Link Data에서 $deeplink\_path에 화면 경로를 넣어요. 두 OS의 경로가 다르면 $android\_deeplink\_path와 $ios\_deeplink\_path를 사용해요. 앱 실행 주소를 포함한 전체 URL과 화면 경로를 구분해요.

앱 직접 연결을 구현하지 않았다면 URI Scheme·화면 경로를 임의로 입력하지 않아요. 스토어 목적지와 측정값은 유지해요. 앱 연결을 사용할 때는 SDK·화면 이동 처리도 구현해야 해요.\
**URI Scheme·화면 경로 입력 화면**

일부 이미지는 구버전 콘솔이에요. Custom URL 등 예시 값 대신 실제 앱의 설정과 스토어 주소를 사용해요.

<figure><img src="https://help.branch.io/img/3997afe-Screenshot_2023-06-02_at_12.21.51_PM-1-.png" alt=""><figcaption><p>Branch iOS URI Scheme과 미설치 유저 목적지 입력 화면 (출처: <a href="https://help.branch.io/developer-hub/ios-basic-integration">Branch - iOS SDK Basic Integration</a>)</p></figcaption></figure>

<figure><img src="https://help.branch.io/img/5fa51f4-configure_options-1-.png" alt=""><figcaption><p>Branch Ad Link의 딥링크 Key·Value 입력 화면 (출처: <a href="https://help.branch.io/marketer-hub/ad-links">Branch - Create Ad Links</a>)</p></figcaption></figure>
{% endtab %}

{% tab title="Singular" %}
Settings → Apps → 대상 앱 → Show Advanced Settings에서 OS별 App Scheme을 등록해요. 링크의 If the app is already installed…에는 실제 앱이 처리하는 딥링크 주소를 설정해요.

| 항목                  | 용도                                 |
| ------------------- | ---------------------------------- |
| \_dl                | 두 OS의 공통 딥링크 주소                    |
| \_ios\_dl           | iOS 딥링크 주소                         |
| \_android\_dl       | Android 딥링크 주소                     |
| \_force\_redirect=1 | 토스 iOS에서 앱 스킴 연결을 적용할 때 함께 확인하는 옵션 |

토스 iOS에서 앱 스킴으로 직접 연결하려면 iOS App Scheme과 App Scheme으로 여는 딥링크 목적지를 설정하고 \_force\_redirect=1을 함께 적용해요. 모든 광고 링크의 공통 제출 필수값은 아니에요. 적용 후 설치 전후에 앱 실행과 스토어 연결을 확인해요.

파라미터만 추가한다고 앱의 딥링크 기능이 구현되지는 않아요. 딥링크를 설정한 링크와 SDK·화면 이동 처리가 필요해요.

After installation…의 Deferred Deep Link는 설치 후 첫 실행에도 특정 화면을 연결하려는 경우의 추가 기능이에요. 별도 구현·지원 조건을 확인하고 클릭 → 스토어 → 설치·첫 실행 → 지정 화면까지 테스트해요. 일반 스토어 경유만으로 특정 화면 이동이 보장되지는 않아요.\
**OS별 앱 스킴·딥링크 목적지 설정 화면**

Destinations 사전 등록은 자주 쓰는 주소를 선택하기 위한 편의 기능이에요. 스토어 전용 링크에는 딥링크 목적지를 설정하지 않아요.

<figure><img src="https://support.singular.net/hc/article_attachments/33430831952027" alt=""><figcaption><p>Singular Android 앱 스킴 입력 화면 (출처: <a href="https://support.singular.net/hc/en-us/articles/360031371451-Singular-Links-Prerequisites">Singular - Singular Links Prerequisites</a>)</p></figcaption></figure>

<figure><img src="https://support.singular.net/hc/article_attachments/360055239651" alt=""><figcaption><p>Singular iOS 앱 스킴 입력 화면 (출처: <a href="https://support.singular.net/hc/en-us/articles/360031371451-Singular-Links-Prerequisites">Singular - Singular Links Prerequisites</a>)</p></figcaption></figure>

<figure><img src="https://support.singular.net/hc/article_attachments/360072436012" alt=""><figcaption><p>Singular 자주 쓰는 목적지(Destinations) 사전 등록 화면 (출처: <a href="https://support.singular.net/hc/en-us/articles/360050910891-How-to-Configure-Deep-Links">Singular - How to Configure Deep Links</a>)</p></figcaption></figure>

<figure><img src="https://support.singular.net/hc/article_attachments/360072435992" alt=""><figcaption><p>Singular 링크 생성 시 설치 상태별 목적지 입력 화면 (출처: <a href="https://support.singular.net/hc/en-us/articles/360050910891-How-to-Configure-Deep-Links">Singular - How to Configure Deep Links</a>)</p></figcaption></figure>
{% endtab %}

{% tab title="DFINERY" %}
앱 스킴을 사용한다면 Ad Landing Settings의 Deep Link Scheme에 앱 스킴 이름을 입력해요. Deep Link Scheme 입력란에는 ://와 화면 경로를 넣지 않아요.

링크 생성 시 Download + Deeplink를 선택하고 Deep Linking에서 대상 OS 설정과 Scheme을 확인해요. 특정 화면을 열려면 Static Path → Path에 화면 경로를 입력해요.

| 구분                 | 입력 예시                              |
| ------------------ | ---------------------------------- |
| Deep Link Scheme   | sampleandroid                      |
| 전체 딥링크 주소          | sampleandroid://product\_id\_12345 |
| Static Path → Path | product\_id\_12345                 |

Dynamic 경로는 캠페인이 경로 치환을 지원할 때만 사용해요. 치환되지 않은 {deeplink\_custom\_path}를 그대로 제출하지 않아요.

Ad-Touch Landing의 스토어 목적지도 확인해요. 앱 직접 연결을 사용하지 않는 경우에는 설치한 유저도 스토어 목적지를 거칠 수 있어요. 앱 직접 연결을 사용하는 경우 SDK의 Deeplink 이벤트와 화면 이동 처리를 구현한 배포 앱으로 테스트해요.\
**앱 스킴·Download + Deeplink·화면 경로 설정 화면**

아래 랜딩 형식 화면은 앱 직접 연결을 적용하는 예시예요. 스토어 전용 링크는 Download를 사용해요.

<figure><img src="https://help.dfinery.io/hc/article_attachments/36794021440537" alt=""><figcaption><p>DFINERY Ad Landing Settings 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360003394433">DFINERY - Ad Landing Settings : 유저의 랜딩지점 설정하기</a>)</p></figcaption></figure>

<figure><img src="https://help.dfinery.io/hc/article_attachments/15002553933593" alt=""><figcaption><p>DFINERY 링크 이름과 랜딩 형식 선택 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360024465693">DFINERY - Ad Campaign 생성과 Tracking Link 발급</a>)</p></figcaption></figure>

<figure><img src="https://help.dfinery.io/hc/article_attachments/15013812418585" alt=""><figcaption><p>DFINERY Deep Linking의 고정 경로(Static Path) 입력 화면 (출처: <a href="https://help.dfinery.io/hc/ko/articles/360024465693">DFINERY - Ad Campaign 생성과 Tracking Link 발급</a>)</p></figcaption></figure>
{% endtab %}
{% endtabs %}

### 유니버설 링크·앱 링크 구현하기 <a href="#universal-link" id="universal-link"></a>

유니버설 링크(iOS)와 앱 링크(Android)는 앱과 연결된 HTTPS 주소로 앱을 여는 기능이에요. 링크 도메인의 연결 정보와 실제 배포 앱의 설정이 일치해야 해요.

1. 개발팀이 앱 식별 정보와 인증서 정보를 마케팅팀에 전달해요.
2. 마케팅팀이 MMP 콘솔에 앱 정보를 등록하고 사용할 링크 도메인을 확인해요.
3. 개발팀이 iOS Associated Domains 또는 Android 앱 링크용 intent-filter에 2번에서 확인한 링크 도메인을 등록해요.
4. SDK와 앱의 화면 이동 처리를 연결하고 앱을 배포해요.
5. 최종 MMP 트래킹 링크로 설치 전후 테스트를 진행해요.

| 플랫폼     | 준비할 정보                                       | 확인할 내용                                                                  |
| ------- | -------------------------------------------- | ----------------------------------------------------------------------- |
| iOS     | Bundle ID, App ID Prefix 또는 Team ID          | MMP가 요구하는 값과 실제 배포 앱을 대조해요. App ID Prefix와 Team ID가 항상 같은 것은 아니에요.      |
| Android | Package Name, SHA256 Certificate Fingerprint | 배포 앱 서명 인증서를 기준으로 해요. Play App Signing 사용 시 Upload key와 구분해요.           |
| 공통      | MMP 링크 도메인                                   | 콘솔과 앱에 등록된 도메인이 일치해야 해요. Custom domain을 쓴다면 Custom domain의 연결 요건도 확인해요. |

MMP가 제공하는 도메인은 콘솔 설정에 따라 AASA 또는 assetlinks.json 같은 연결 파일을 제공해요. 별도 도메인을 사용하면 그 도메인이 연결 파일을 제공하는지와 연결 설정도 확인해요.

**MMP별 설정 위치**

| MMP       | 콘솔에서 확인할 곳                                                              | 앱에 반영할 것                                                                                    |
| --------- | ----------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| AppsFlyer | OneLink template → When app is installed에서 Universal Links·App Links 설정 | OneLink 도메인, iOS Team ID·Android SHA256에 맞는 앱 연결                                            |
| Adjust    | AppView → Platforms에서 Universal linking·Android App Links 설정            | Branded domain과 SDK 처리. Deep link generator는 사전 요건을 확인                                      |
| Airbridge | Tracking Link → Deep Links에서 앱 식별 정보·인증서 설정                             | App Name에 대응하는 [airbridge.io](http://airbridge.io)·[abr.ge](http://abr.ge) 앱 전용 도메인과 SDK 처리 |
| Branch    | Mobile Routing에서 Enable Universal Links·Enable App Links                | Link Domains의 기본·alternate 도메인과 SDK 처리                                                      |
| Singular  | Apps의 Advanced Settings에서 Team ID·App Links SHA256 설정                   | 실제 Singular 링크 도메인과 경로에 맞는 앱 연결                                                             |
| DFINERY   | Ad Landing Settings의 Universal Links·App Links 설정                       | 실제 트래킹 링크 도메인과 SDK 처리                                                                       |

앱 직접 연결 기능을 선택했다면 사용하는 MMP가 요구하는 앱 스킴 등 추가 요건도 확인해요. 토스의 제출 요건이 권장이라는 이유로 MMP 기능에 필요한 설정을 생략하지 않아요.

기존에 앱 스킴을 사용하고 있다면 유지해요. 모든 환경에서 동일한 방식으로 열리거나 확인창 없이 바로 열린다고 보장되지는 않아요. 어떤 경로로 열렸는지는 실제 테스트 결과로 확인해요.

공식 설정 가이드는 아래를 참고해 주세요.

* [AppsFlyer OneLink](https://support.appsflyer.com/hc/en-us/articles/207032246-Create-a-OneLink-template)
* [Adjust iOS](https://help.adjust.com/en/article/set-up-universal-links) · [Adjust Android](https://help.adjust.com/en/article/set-up-android-app-links)
* [Airbridge iOS SDK](https://help.airbridge.io/en/developers/ios-sdk-v4) · [Airbridge Android SDK](https://help.airbridge.io/en/developers/android-sdk-v4)
* [Branch Routing](https://help.branch.io/account-hub/link-routing-rules-new)
* [Singular 사전 설정](https://support.singular.net/hc/en-us/articles/360031371451-Singular-Links-Prerequisites)
* [DFINERY 랜딩 설정](https://help.dfinery.io/hc/en-us/articles/360003394433-Ad-Landing-Settings-Setting-the-user-s-landing-point)

## 3. 최종 링크 테스트하기 <a href="#step3-test" id="step3-test"></a>

**실제 제출할 MMP 클릭용 트래킹 링크로 테스트해요.** 앱 스킴 주소만 직접 실행하면 MMP를 거치지 않으므로 링크 전체가 정상인지 확인할 수 없어요.

### 테스트 전 점검 <a href="#pre-test-check" id="pre-test-check"></a>

* 필수 측정값이 모두 들어 있는지 확인해요.
* 토스 매체 식별값과 캠페인 정보가 맞는지 확인해요.
* 매크로의 대소문자·중괄호, 빈 값, 중복 키를 확인해요.
* URL 인코딩과 ?·& 연결이 맞는지 확인해요.
* 광고 대상 앱의 올바른 스토어 페이지가 설정돼 있는지 확인해요. iOS의 토스 앱 내 테스트에서는 토스 안에서 광고 대상 앱의 App Store 상품 화면이 열리는지도 확인해요.
* 앱 직접 연결을 사용하는 경우 배포 앱과 MMP 설정이 일치하는지 확인해요.

iOS에서 외부 App Store 앱이나 일반 웹으로 이동한 뒤 끝나는 경우를 토스 안의 상품 화면 도착과 같은 결과로 판단하지 않아요.

### 실제 휴대폰에서 확인하기 <a href="#test-on-device" id="test-on-device"></a>

1. 최종 링크를 이메일이나 메모 앱 등에 넣고 실제 휴대폰에서 눌러요. 브라우저 주소창에 붙여 넣은 결과만으로 판단하지 않아요.
2. 대상 OS별로 앱을 설치하지 않은 상태와 설치한 상태를 모두 테스트해요.
3. 토스 앱에서도 같은 최종 링크의 동작을 확인해요. 다른 브라우저에서 성공한 결과만으로 토스 안의 동작을 판단하지 않아요.
4. 도착한 앱·스토어와 실제 이동 경로를 기록해요.

| 앱 상태·설정               | 기대 결과                                              |
| --------------------- | -------------------------------------------------- |
| 앱 미설치                 | 광고 대상 앱의 App Store 또는 Google Play 페이지에 도착해요.       |
| 앱 설치·직접 연결 사용         | 광고주 앱이 열리는지 확인해요. 특정 화면을 설정했다면 설정한 화면이 열리는지도 확인해요. |
| 앱 설치·스토어 경유           | 광고 대상 앱의 스토어 페이지에서 ‘열기’를 누르면 광고주 앱이 실행돼요.          |
| Deferred Deep Link 사용 | 미설치 상태의 클릭부터 설치·첫 실행 후 지정 화면까지 추가 확인해요.            |

앱이 바로 열리지 않고 스토어를 거치더라도 올바른 앱의 ‘열기’로 광고주 앱에 도착할 수 있다면 허용되는 연결 방식이에요. 직접 연결을 설정했는데 스토어를 거친다면 사용자 경험 개선을 위해 연결 설정을 점검해 주세요.

{% hint style="info" %}
**앱 도착과 성과 측정을 따로 확인해요.**

앱이 열려도 필수 측정값의 누락·오류·중복은 수정해야 해요. 반대로 앱 스킴이나 유니버설 링크·앱 링크가 없다는 이유만으로 링크를 오류로 판단하지 않아요.
{% endhint %}

확인창이나 브라우저 전환의 유무만으로 성공·실패를 판단하지 않아요. 최종 도착지를 확인하고, 앱 직접 실행과 스토어 경유를 구분해 기록해요. 일반적인 스토어 경유가 설치 후 특정 화면 이동까지 보장하는 것은 아니에요.

### MMP별 추가 확인 <a href="#mmp-extra-checks" id="mmp-extra-checks"></a>

* Branch: Validate & Share 오류를 확인한 뒤 실제 휴대폰에서도 테스트해요.
* Singular: Deferred Deep Link를 사용한다면 설치·첫 실행 후 화면 이동을 확인해요.
* DFINERY: MMP 클릭 기록을 확인해요. 앱 직접 연결을 사용한다면 앱의 Deeplink 이벤트 수신도 확인해요.

### 문제 해결하기 <a href="#troubleshooting" id="troubleshooting"></a>

| 증상                    | 확인할 내용                                                                                       |
| --------------------- | -------------------------------------------------------------------------------------------- |
| 앱이 설치돼 있는데 스토어로 이동해요. | 직접 연결을 사용하지 않으면 가능한 경로예요. 올바른 앱의 스토어인지, ‘열기’로 앱에 도착하는지 먼저 확인해요. 직접 연결을 설정했다면 앱·MMP 설정을 점검해요. |
| 스토어에서 다른 앱이 보여요.      | 광고 대상 앱 식별 정보와 OS별 스토어 주소를 수정해요.                                                             |
| 앱이 열리지만 다른 화면이에요.     | 특정 화면 연결을 설정했다면 딥링크 주소·화면 식별값과 앱의 처리 로직을 대조해요. 스토어 경유 후 특정 화면은 별도 기능이 필요할 수 있어요.             |
| 한쪽 OS에서만 실패해요.        | 실패한 OS의 스토어 주소와 앱 식별 정보를 확인해요. 직접 연결을 사용한다면 OS별 스킴·도메인·인증서도 확인해요.                            |
| 미설치 상태에서 이동이 멈춰요.     | 스토어 목적지와 앱 강제 실행 옵션을 확인하고 수정한 링크로 설치 전후 재시험해요.                                               |
| 링크 수정 후 실패해요.         | 인코딩, ?·& 위치, 빈 값과 중복 파라미터를 확인해요.                                                             |
| 앱은 열리지만 측정되지 않아요.     | SDK·이벤트 연동, 토스 파트너 설정, 매체 식별값과 측정 파라미터를 각각 확인해요.                                             |

앱 스킴 연결을 사용하는 AppsFlyer 링크는 af\_dp와 af\_force\_deeplink=true를 함께 확인해요. Singular iOS 앱 스킴 연결은 앱 스킴·딥링크 목적지와 \_force\_redirect=1을 함께 확인해요. 옵션만 추가하면 모든 문제가 해결된다고 판단하지 않아요.

### 최종 제출 <a href="#final-link" id="final-link"></a>

테스트한 최종 클릭용 트래킹 링크를 소재 등록에 사용해요. 설정값을 확인할 수 있는 원래의 긴 주소를 준비하고, 제출 형식은 [소재 가이드](creative.md)를 확인해요.

링크나 MMP 설정을 바꾼 경우 변경한 최종 링크로 다시 테스트해요.
