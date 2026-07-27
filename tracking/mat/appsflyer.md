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

# 앱스플라이어

### 전환 추적 코드 생성하기

{% stepper %}
{% step %}
**전환 및 추적 연동**

<figure><img src="../../.gitbook/assets/Group 335.png" alt=""><figcaption></figcaption></figure>

전환 및 추적 연동 설정은 아래 경로에서 가능해요.

광고 계정 접속 → 광고 도구 \[전환 및 추적 연동] 선택
{% endstep %}

{% step %}
**전환 추적 코드 생성**

<figure><img src="../../.gitbook/assets/동의 및 코드 생성 (2).png" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성하고 생성한 전환 추적 코드 ID를 복사해주세요.
{% endstep %}
{% endstepper %}

***

### 앱스플라이어 연동하기

{% stepper %}
{% step %}
**앱스플라이어 연동 경로**

<figure><img src="../../.gitbook/assets/스크린샷 2024-04-16 오전 11.50.47.png" alt=""><figcaption></figcaption></figure>

앱스플라이어 연동 링크 생성은 아래 경로에서 가능해요.

Partner Marketplace → \[Toss] 앱 검색 → Set up intergration 선택
{% endstep %}

{% step %}
**연동 활성화**

<figure><img src="../../.gitbook/assets/스크린샷 2024-04-16 오전 11.51.45.png" alt=""><figcaption></figcaption></figure>

Active partner 의 스위치 버튼을 클릭하여 파트너 연동을 활성화 하고 Integration 탭에서 토스 플랫폼에서 발급받은 전환 추적 코드의 ID 값을 복사하여 cvr\_id 항목에 입력해주세요.

<figure><img src="../../.gitbook/assets/image (262).png" alt=""><figcaption></figcaption></figure>

* IOS 세팅을 하시는 경우, Advanced Privacy 모드가 'OFF'로 되어 있는지 확인해 주세요.
  * 해당 설정을 꺼두셔야 데이터 익명화 처리를 방지하고, 토스 애즈와 AppsFlyer 간의 데이터 정합성을 확보할 수 있어요.
{% endstep %}

{% step %}
**이벤트 연동**

<figure><img src="../../.gitbook/assets/스크린샷 2024-07-17 오후 3.47.29.png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/스크린샷 2024-07-17 오후 3.48.40.png" alt=""><figcaption></figcaption></figure>

* 앱 내에서의 이벤트 연동을 희망하는 경우 In-app event postbacks 토글을 ON으로 변경해주세요.
* 전송되는 이벤트에 대하여 **All media sources, including organic** 항목을 선택, 해당 항목이 없다면 This Partner Only를 선택해주세요.
* Save Integration 를 눌러 연동을 완료해주세요.
* **상세한 가이드는** [**Appsflyer 연동 가이드**](https://support.appsflyer.com/hc/ko/articles/9960361873809-%ED%8C%8C%ED%8A%B8%EB%84%88-%EB%A7%88%EC%BC%93%ED%94%8C%EB%A0%88%EC%9D%B4%EC%8A%A4)**를 참고해주세요.**
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th width="198.25347900390625">이벤트 이름</th><th>Toss Ads 이벤트 라벨</th><th>AppsFlyer 이벤트 라벨</th></tr></thead><tbody><tr><td>설치</td><td>INSTALL</td><td>install</td></tr><tr><td>앱 오픈</td><td>APP_OPEN</td><td>af_app_opened</td></tr><tr><td>딥링크/푸시 실행</td><td>APP_DEEPLINK_OPEN</td><td>af_opened_from_push_notification</td></tr><tr><td>회원가입</td><td>SIGNUP</td><td>af_complete_registration</td></tr><tr><td>로그인</td><td>SIGNIN</td><td>af_login</td></tr><tr><td>결제</td><td>PURCHASE</td><td>af_purchase</td></tr><tr><td>상품 조회</td><td>PRODUCT_VIEW</td><td>af_content_view</td></tr><tr><td>장바구니 추가</td><td>ADD_TO_CART</td><td>af_add_to_cart</td></tr><tr><td>검색</td><td>SEARCH</td><td>af_search</td></tr><tr><td>결제 시작</td><td>INITIATE_CHECKOUT</td><td>af_initiated_checkout</td></tr><tr><td>위시리스트 추가</td><td>ADD_TO_WISHLIST</td><td>af_add_to_wishlist</td></tr><tr><td>구독</td><td>SUBSCRIBE</td><td>af_subscribe</td></tr><tr><td>광고 노출</td><td>AD_IMPRESSION</td><td>af_ad_view</td></tr><tr><td>리드</td><td>LEAD_COLLECTION</td><td>lead</td></tr></tbody></table>

{% hint style="success" %}
* 연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야해요.
  * 랜딩URL은 전환 추적 탬플릿으로 생성한 랜딩 URL로 입력해주세요.
* AppsFlyer 이벤트 라벨은 AppsFlyer에서 사용 중인 기본 명칭으로 기재되었어요. 자사 서비스에서 발생하는 이벤트를 기준으로 [토스애즈의 표준이벤트](../tag/tracked-events.md)와 가장 적절한 이벤트에 매핑해 주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목

토스애즈에서 **앱스플라이어(AppsFlyer)**&#xB97C; 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 포함해 주세요.

필수 항목이 누락되면 **어떤 광고에서 전환이 발생했는지 확인하기 어렵고 앱스플라이어 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

| 항목                     | 값                     | 설명          |
| ---------------------- | --------------------- | ----------- |
| pid                    | tossa3u\_int          | 고유 매체 식별자   |
| clickid                | {TOSS\_TK\_CLICK\_ID} | 포스트백용 클릭 ID |
| advertising\_id / idfa | {USER\_ADID}          | 디바이스 광고 ID  |
| af\_c\_id              | {TOSS\_CID}           | 캠페인 ID      |

#### 권장 항목

아래 항목들은 랜딩 URL에 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **캠페인/광고그룹/소재 단위 성과를 세부적으로 확인하기 어렵고 앱스플라이어 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| 항목         | 값                    | 설명     |
| ---------- | -------------------- | ------ |
| af\_ad\_id | {TOSS\_CREATIVE\_ID} | 소재 ID  |
| af\_siteid | {SITE\_ID}           | 매체 ID  |
| af\_adset  | {ADGROUP\_NAME}      | 광고 그룹명 |
| af\_ad     | {CREATIVE\_NAME}     | 광고 소재명 |
| c          | {CAMPAIGN\_NAME}     | 캠페인명   |

#### 링크 구성 예시

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> https://app.appsflyer.com/abc?<mark style="color:red;">**pid=tossa3u\_int\&clickid={TOSS\_TK\_CLICK\_ID}\&advertising\_id={USER\_ADID}\&af\_c\_id={TOSS\_CID}\&af\_ad\_id={TOSS\_CREATIVE\_ID**</mark>}&<mark style="color:blue;">**af\_siteid={SITE\_ID}\&af\_adset={ADGROUP\_NAME}\&af\_ad={CREATIVE\_NAME}\&c={CAMPAIGN\_NAME}**</mark>

{% hint style="success" %}
**링크 설정 Tip**

*   앱스플라이어 콘솔에서 제공하는 click attribution link를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.

    * 자세한 설정 방법은 앱스플라이어 대시보드 내 Active Intergrations > Attribution link 탭에서 확인하실 수 있어요.

    <figure><img src="../../.gitbook/assets/image (1).jpeg" alt="" width="375"><figcaption></figcaption></figure>
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 표준 키와 구조를 꼭 확인해 주세요.
* Tracking URL에서 수정이 필요한 항목은 캠페인 설정 시 **소재 URL** 섹션에서 다시 확인할 수 있습니다.
{% endhint %}
