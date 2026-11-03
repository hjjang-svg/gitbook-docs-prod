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

# 에어브릿지

### 전환 추적 코드 생성하기 <a href="#create-conversion-code" id="create-conversion-code"></a>

{% stepper %}
{% step %}
**전환 및 추적 연동**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FokITefTS9bsZJon0reTo%2FGroup%20335.png?alt=media&#x26;token=15cffb8e-1a21-42b8-9f77-5a954e6a7e52" alt=""><figcaption></figcaption></figure>

전환 및 추적 연동 설정은 아래 경로에서 가능해요.

광고계정 접속 → 광고 도구 \[전환 및 추적 연동] 선택
{% endstep %}

{% step %}
**전환 추적 코드 생성**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FmXFxvyrjjKEhrpaOCgxH%2F%E1%84%83%E1%85%A9%E1%86%BC%E1%84%8B%E1%85%B4%20%E1%84%86%E1%85%B5%E1%86%BE%20%E1%84%8F%E1%85%A9%E1%84%83%E1%85%B3%20%E1%84%89%E1%85%A2%E1%86%BC%E1%84%89%E1%85%A5%E1%86%BC-1.png?alt=media&#x26;token=afbe341d-883d-4dba-864b-ecf26715c8bd" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성해주세요.
{% endstep %}

{% step %}
**생성 여부 확인**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2Fy8WlFaarmlvzGmkEhvmI%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202026-02-20%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.20.00%202.png?alt=media&#x26;token=e280e08e-ad0b-4d2e-862a-e6233ab97f2c" alt=""><figcaption></figcaption></figure>

설정한 정보에 맞게 생성된 전환 추적 코드의 ID를 복사하여 연동할 수 있어요.
{% endstep %}
{% endstepper %}

***

### 에어브릿지 연동하기 <a href="#connect-airbridge" id="connect-airbridge"></a>

{% stepper %}
{% step %}
**에어브릿지 연동 경로**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2Fvul0kCUgyowP77WZKYed%2Ftoss-ads-01.png?alt=media&#x26;token=482c8c51-b722-456a-bab6-c1ae881cfe6b" alt=""><figcaption></figcaption></figure>

에어브릿지 연동 링크 생성은 아래 경로에서 가능해요.

Integrations → Intergrated Ad Channels 선택 → \[Toss]앱 검색
{% endstep %}

{% step %}
**연동 활성화**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2F1SLdbjHovrCDf0cncnEY%2Fimage.png?alt=media&#x26;token=176455bc-0daf-4084-8980-4f047c2771cd" alt=""><figcaption></figcaption></figure>

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FxRNNrdZ4wJ2ENGgKDYnp%2Fimage.png?alt=media&#x26;token=7814b292-3cb2-43eb-95c7-c610c202e699" alt=""><figcaption></figcaption></figure>

* 포스트백 전송 토글을 ON으로 변경하고 인증 정보 관리 버튼을 클릭하여 토스 플랫폼에서 발급받은 전환 추적 코드의 ID 값을 복사하여 cvr\_id 항목에 입력하여 파트너 연동을 활성화 해주세요.
  * 전환 추적 코드 ID 수정이 필요하다면 포스트백 전송을 중지한 이후 수정 해주세요.
* 이벤트 전송 규칙은 `채널 기여와 상관 없이 모든 이벤트 전송`으로 설정해주세요.
* 상세한 가이드는 [Airbridge 연동 가이드](https://help.airbridge.io/ko/guides/toss-ads)를 참고해주세요.
{% endstep %}
{% endstepper %}

***

### 미디어 파트너 권한 부여하기 <a href="#grant-media-partner" id="grant-media-partner"></a>

{% stepper %}
{% step %}
**미디어 파트너 권한 부여**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FgIbnrY0AiohwzT59lACP%2Fimage.png?alt=media&#x26;token=572bfd8f-fb7c-4fbf-914c-c9abfee145b6" alt=""><figcaption></figcaption></figure>

에어브릿지를 연동한 후 데이터 관리 및 최적화를 위해 toss-ads@toss.im 계정에 미디어 파트너 권한을 부여해주세요.

권한 부여 경로는 아래와 같아요.

에어브릿지 접속 → \[Settings] → \[User Management] 접속
{% endstep %}

{% step %}
**앱 접근 권한 부여**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FLe3gjVsioACSUJlKq4Qu%2Fimage.png?alt=media&#x26;token=363900d5-fa37-4b17-9980-ebd84bedc39c" alt=""><figcaption></figcaption></figure>

\[앱 접근 권한 부여] 버튼을 클릭해주세요.

팝업창에서 toss-ads@toss.im 계정을 입력하고 앱 역할을 "미디어 파트너"로 설정해주세요.

자세한 가이드는 [에어브릿지 > 앱에서 앱 접근 권한 관리하기 가이드](https://help.airbridge.io/ko/guides/app-access-management)를 참고해주세요.
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기 <a href="#event-mapping" id="event-mapping"></a>

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th>토스애즈 이벤트 라벨</th><th>Airbridge 이벤트 라벨</th><th width="185.28466796875">이벤트명</th></tr></thead><tbody><tr><td>AD_IMPRESSION</td><td>airbridge.adImpression</td><td>광고 노출</td></tr><tr><td>ADD_TO_CART</td><td>airbridge.ecommerce.product.addedToCart</td><td>장바구니 추가</td></tr><tr><td>ADD_TO_WISHLIST</td><td>airbridge.addToWishlist</td><td>위시리스트 추가</td></tr><tr><td>APP_DEEPLINK_OPEN</td><td>app_deeplink_open</td><td>딥링크 앱 오픈</td></tr><tr><td>APP_OPEN</td><td>app_open</td><td>앱 오픈</td></tr><tr><td>APPLY_SCREENING</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>가심사 조회</td></tr><tr><td>FIRST_PURCHASE</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>첫 구매</td></tr><tr><td>GET_OFFER</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>쿠폰 다운로드</td></tr><tr><td>INITIATE_CHECKOUT</td><td>airbridge.initiateCheckout</td><td>결제 시작</td></tr><tr><td>INSTALL</td><td>app_install</td><td>설치</td></tr><tr><td>LEAD_COLLECTION</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>잠재 고객</td></tr><tr><td>LEVEL_ACHIEVED</td><td>airbridge.achieveLevel</td><td>레벨 달성</td></tr><tr><td>PAGE_VIEW</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>페이지 조회</td></tr><tr><td>PRE_REGISTER</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>사전 예약</td></tr><tr><td>PRODUCT_VIEW</td><td>airbridge.ecommerce.product.viewed</td><td>상품 조회</td></tr><tr><td>PURCHASE</td><td>airbridge.ecommerce.order.completed</td><td>결제</td></tr><tr><td>SEARCH</td><td>airbridge.ecommerce.searchResults.viewed</td><td>검색</td></tr><tr><td>SIGNIN</td><td>airbridge.user.signin</td><td>로그인</td></tr><tr><td>SIGNUP</td><td>airbridge.user.signup</td><td>회원가입</td></tr><tr><td>SUBSCRIBE</td><td>airbridge.subscribe</td><td>구독</td></tr><tr><td>TUTORIAL</td><td>airbridge.completeTutorial</td><td>튜토리얼</td></tr><tr><td>VIEW_HOME</td><td>airbridge.ecommerce.home.viewed</td><td>홈 조회</td></tr><tr><td>VIEW_LIMIT</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>한도 조회</td></tr></tbody></table>

{% hint style="warning" %}
**일부 이벤트는 담당 AM에게 별도로 요청해야 해요.**

표에서 '담당 AM과 상의'로 적힌 이벤트는 Airbridge 설정과 별개로 토스애즈에서 추가 작업이 필요해요. 이벤트 설정과 매핑 방법은 담당 AM과 상의해 주세요.
{% endhint %}

{% hint style="success" %}
연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야 해요.

* 랜딩 URL은 전환 추적 템플릿으로 생성한 랜딩 URL로 입력해 주세요.

Airbridge 이벤트 라벨은 Airbridge에서 사용 중인 기본 명칭으로 기재되었어요. 자사 서비스에서 발생하는 이벤트를 기준으로 [토스애즈의 표준이벤트](../tag/tracked-events.md)와 가장 적절한 이벤트에 매핑해 주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목 <a href="#airbridge-link-parameters" id="airbridge-link-parameters"></a>

토스애즈에서 **에어브릿지**를 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목 <a href="#required-parameters" id="required-parameters"></a>

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 포함해 주세요.

필수 항목이 누락되면 **어떤 광고에서 전환이 발생했는지 확인하기 어렵고 에어브릿지 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

| 항목           | 값                     | 설명          |
| ------------ | --------------------- | ----------- |
| path         | /toss                 | 경로 식별자      |
| click\_id    | {TOSS\_TK\_CLICK\_ID} | 클릭 ID       |
| ad\_id       | {USER\_ADID}          | ADID / IDFA |
| campaign\_id | {TOSS\_CID}           | 캠페인 ID      |

#### 권장 항목 <a href="#recommended-parameters" id="recommended-parameters"></a>

아래 항목들은 랜딩 URL에 함께 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **캠페인/광고그룹/소재 단위 성과를 세부적으로 확인하기 어렵고 에어브릿지 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| 항목               | 값                    | 설명     |
| ---------------- | -------------------- | ------ |
| sub\_id          | {SITE\_ID}           | 지면 구분  |
| ad\_creative\_id | {TOSS\_CREATIVE\_ID} | 소재 ID  |
| campaign         | {CAMPAIGN\_NAME}     | 캠페인명   |
| ad\_group        | {ADGROUP\_NAME}      | 광고 그룹명 |
| ad\_creative     | {CREATIVE\_NAME}     | 광고 소재명 |

### 링크 구성 예시 <a href="#link-example" id="link-example"></a>

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> https://abr.ge/@tossads/toss?<mark style="color:red;">**click\_id={TOSS\_TK\_CLICK\_ID}\&ad\_id={USER\_ADID}\&campaign\_id={TOSS\_CID}**</mark>&<mark style="color:blue;">**sub\_id={SITE\_ID}\&ad\_creative\_id={TOSS\_CREATIVE\_ID}\&campaign={CAMPAIGN\_NAME}\&ad\_group={ADGROUP\_NAME}\&ad\_creative={CREATIVE\_NAME}**</mark>

{% hint style="warning" %}
**링크 설정 시 확인해 주세요.**

* 에어브릿지 콘솔에서 제공하는 click attribution link를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.
  * 자세한 설정 방법은 에어브릿지 대시보드 내 연동 > 광고 채널 연동 > 토스 >트래킹 링크 탭에서 확인하실 수 있어요.
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 필수 항목의 구조를 꼭 확인해 주세요.
* Tracking URL에서 수정이 필요한 항목은 캠페인 설정 시 **소재 URL** 섹션에서 다시 확인할 수 있습니다.
* 카탈로그 및 앱 설치 유도하기 광고를 운영하는 경우, 토스 광고 상품 내 최적 경험을 위해 트래킹 링크 생성 시 **스탑오버 에어페이지를 OFF(미적용)**&#xD574;주세요. 스탑오버 에어페이지 상세 가이드는 [에어브릿지](https://help.airbridge.io/ko/deeplink-guides/deeplink-option-setting#%EC%8A%A4%ED%83%91%EC%98%A4%EB%B2%84-%EC%97%90%EC%96%B4%ED%8E%98%EC%9D%B4%EC%A7%80-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0)에서 확인하실 수 있습니다.
{% endhint %}
