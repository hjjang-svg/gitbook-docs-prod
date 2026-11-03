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

# 앱스플라이어

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

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FggG0J7LVtF3yJVPiIjX7%2F%E1%84%83%E1%85%A9%E1%86%BC%E1%84%8B%E1%85%B4%20%E1%84%86%E1%85%B5%E1%86%BE%20%E1%84%8F%E1%85%A9%E1%84%83%E1%85%B3%20%E1%84%89%E1%85%A2%E1%86%BC%E1%84%89%E1%85%A5%E1%86%BC.png?alt=media&#x26;token=7db55eeb-d2aa-4aa8-8973-5f6c70069b58" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성하고 생성한 전환 추적 코드 ID를 복사해주세요.
{% endstep %}
{% endstepper %}

***

### 앱스플라이어 연동하기 <a href="#connect-appsflyer" id="connect-appsflyer"></a>

{% stepper %}
{% step %}
**앱스플라이어 연동 경로**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FTb7LjsD74e6tMzNNmlrr%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202024-04-16%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2011.50.47.png?alt=media&#x26;token=fe00f48f-9ac5-402e-a677-6f5f73d7a960" alt=""><figcaption></figcaption></figure>

앱스플라이어 연동 링크 생성은 아래 경로에서 가능해요.

Partner Marketplace → \[Toss] 앱 검색 → Set up intergration 선택
{% endstep %}

{% step %}
**연동 활성화**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FpWUORarv3A4zh5KT1OW5%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202024-04-16%20%E1%84%8B%E1%85%A9%E1%84%8C%E1%85%A5%E1%86%AB%2011.51.45.png?alt=media&#x26;token=5612ad13-b706-4dee-bf4c-6da506116fce" alt=""><figcaption></figcaption></figure>

Active partner 의 스위치 버튼을 클릭하여 파트너 연동을 활성화 하고 Integration 탭에서 토스 플랫폼에서 발급받은 전환 추적 코드의 ID 값을 복사하여 cvr\_id 항목에 입력해주세요.

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FgJGpYpqVDulXlysfRRz8%2Fimage.png?alt=media&#x26;token=d365f5cd-6009-48ee-84da-34c2d8548f44" alt=""><figcaption></figcaption></figure>

* IOS 세팅을 하시는 경우, Advanced Privacy 모드가 'OFF'로 되어 있는지 확인해 주세요.
  * 해당 설정을 꺼두셔야 데이터 익명화 처리를 방지하고, 토스애즈와 AppsFlyer 간의 데이터 정합성을 확보할 수 있어요.
{% endstep %}

{% step %}
**이벤트 연동**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2F5wS8xZUwtAOyGeqGTQBL%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202024-07-17%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.47.29.png?alt=media&#x26;token=2dd4dd7f-64a6-41d5-84ef-a99bf489dca5" alt=""><figcaption></figcaption></figure>

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2Ffj6cQZ5W2rGDN7trDrZ7%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202024-07-17%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%203.48.40.png?alt=media&#x26;token=a99d6f5f-2bcb-4a67-8504-300ba16004c4" alt=""><figcaption></figcaption></figure>

* 앱 내에서의 이벤트 연동을 희망하는 경우 In-app event postbacks 토글을 ON으로 변경해주세요.
* 전송되는 이벤트에 대하여 **All media sources, including organic** 항목을 선택, 해당 항목이 없다면 This Partner Only를 선택해주세요.
* Save Integration 를 눌러 연동을 완료해주세요.
* **상세한 가이드는** [**Appsflyer 연동 가이드**](https://support.appsflyer.com/hc/ko/articles/9960361873809-%ED%8C%8C%ED%8A%B8%EB%84%88-%EB%A7%88%EC%BC%93%ED%94%8C%EB%A0%88%EC%9D%B4%EC%8A%A4)**를 참고해주세요.**
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기 <a href="#event-mapping" id="event-mapping"></a>

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th>토스애즈 이벤트 라벨</th><th>AppsFlyer 이벤트 라벨</th><th width="198.25347900390625">이벤트명</th></tr></thead><tbody><tr><td>AD_IMPRESSION</td><td>af_ad_view</td><td>광고 노출</td></tr><tr><td>ADD_TO_CART</td><td>af_add_to_cart</td><td>장바구니 추가</td></tr><tr><td>ADD_TO_WISHLIST</td><td>af_add_to_wishlist</td><td>위시리스트 추가</td></tr><tr><td>APP_DEEPLINK_OPEN</td><td>af_opened_from_push_notification</td><td>딥링크/푸시 실행</td></tr><tr><td>APP_OPEN</td><td>af_app_opened</td><td>앱 오픈</td></tr><tr><td>APPLY_SCREENING</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>가심사 조회</td></tr><tr><td>FIRST_PURCHASE</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>첫 구매</td></tr><tr><td>GET_OFFER</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>쿠폰 다운로드</td></tr><tr><td>INITIATE_CHECKOUT</td><td>af_initiated_checkout</td><td>결제 시작</td></tr><tr><td>INSTALL</td><td>install</td><td>설치</td></tr><tr><td>LEAD_COLLECTION</td><td>lead</td><td>리드</td></tr><tr><td>LEVEL_ACHIEVED</td><td>af_level_achieved</td><td>레벨 달성</td></tr><tr><td>PAGE_VIEW</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>페이지 조회</td></tr><tr><td>PRE_REGISTER</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>사전 예약</td></tr><tr><td>PRODUCT_VIEW</td><td>af_content_view</td><td>상품 조회</td></tr><tr><td>PURCHASE</td><td>af_purchase</td><td>결제</td></tr><tr><td>SEARCH</td><td>af_search</td><td>검색</td></tr><tr><td>SIGNIN</td><td>af_login</td><td>로그인</td></tr><tr><td>SIGNUP</td><td>af_complete_registration</td><td>회원가입</td></tr><tr><td>SUBSCRIBE</td><td>af_subscribe</td><td>구독</td></tr><tr><td>TUTORIAL</td><td>af_tutorial_completion</td><td>튜토리얼</td></tr><tr><td>VIEW_HOME</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>홈 조회</td></tr><tr><td>VIEW_LIMIT</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>한도 조회</td></tr></tbody></table>

{% hint style="warning" %}
**일부 이벤트는 담당 AM에게 별도로 요청해야 해요.**

표에서 '담당 AM과 상의'로 적힌 이벤트는 AppsFlyer 설정과 별개로 토스애즈에서 추가 작업이 필요해요. 이벤트 설정과 매핑 방법은 담당 AM과 상의해 주세요.
{% endhint %}

{% hint style="success" %}
연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야 해요.

* 랜딩URL은 전환 추적 템플릿으로 생성한 랜딩 URL로 입력해주세요.

AppsFlyer 이벤트 라벨은 AppsFlyer에서 사용 중인 기본 명칭으로 기재되었어요. 자사 서비스에서 발생하는 이벤트를 기준으로 [토스애즈의 표준이벤트](../tag/tracked-events.md)와 가장 적절한 이벤트에 매핑해 주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목 <a href="#appsflyer-link-parameters" id="appsflyer-link-parameters"></a>

토스애즈에서 **앱스플라이어(AppsFlyer)**&#xB97C; 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목 <a href="#required-parameters" id="required-parameters"></a>

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 포함해 주세요.

필수 항목이 누락되면 **어떤 광고에서 전환이 발생했는지 확인하기 어렵고 앱스플라이어 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

| 항목                     | 값                     | 설명          |
| ---------------------- | --------------------- | ----------- |
| pid                    | tossa3u\_int          | 고유 매체 식별자   |
| clickid                | {TOSS\_TK\_CLICK\_ID} | 포스트백용 클릭 ID |
| advertising\_id / idfa | {USER\_ADID}          | 디바이스 광고 ID  |
| af\_c\_id              | {TOSS\_CID}           | 캠페인 ID      |

#### 권장 항목 <a href="#recommended-parameters" id="recommended-parameters"></a>

아래 항목들은 랜딩 URL에 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **캠페인/광고그룹/소재 단위 성과를 세부적으로 확인하기 어렵고 앱스플라이어 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| 항목         | 값                    | 설명     |
| ---------- | -------------------- | ------ |
| af\_ad\_id | {TOSS\_CREATIVE\_ID} | 소재 ID  |
| af\_siteid | {SITE\_ID}           | 매체 ID  |
| af\_adset  | {ADGROUP\_NAME}      | 광고 그룹명 |
| af\_ad     | {CREATIVE\_NAME}     | 광고 소재명 |
| c          | {CAMPAIGN\_NAME}     | 캠페인명   |

#### 링크 구성 예시 <a href="#link-example" id="link-example"></a>

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> https://app.appsflyer.com/abc?<mark style="color:red;">**pid=tossa3u\_int\&clickid={TOSS\_TK\_CLICK\_ID}\&advertising\_id={USER\_ADID}\&af\_c\_id={TOSS\_CID}**</mark>&<mark style="color:blue;">**af\_ad\_id={TOSS\_CREATIVE\_ID}\&af\_siteid={SITE\_ID}\&af\_adset={ADGROUP\_NAME}\&af\_ad={CREATIVE\_NAME}\&c={CAMPAIGN\_NAME}**</mark>

{% hint style="success" %}
**링크 설정 Tip**

*   앱스플라이어 콘솔에서 제공하는 click attribution link를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.

    * 자세한 설정 방법은 앱스플라이어 대시보드 내 Active Integrations > Attribution link 탭에서 확인하실 수 있어요.

    <figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FRbPvzlKVXLxYluBuD2ES%2Fimage%20(1).jpeg?alt=media&#x26;token=98e64d70-4d08-46b9-a095-9626b8f9c462" alt="" width="375"><figcaption></figcaption></figure>
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 표준 키와 구조를 꼭 확인해 주세요.
* Tracking URL에서 수정이 필요한 항목은 캠페인 설정 시 **소재 URL** 섹션에서 다시 확인할 수 있습니다.
{% endhint %}
