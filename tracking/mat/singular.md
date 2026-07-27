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

# 싱귤러

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

<figure><img src="../../.gitbook/assets/동의 및 코드 생성-3.png" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성하고 생성한 전환 추적 코드 ID를 복사해주세요.
{% endstep %}
{% endstepper %}

***

### 싱귤러 연동하기

{% stepper %}
{% step %}
**싱귤러 연동 경로**

싱귤러 연동 링크 생성은 아래 경로에서 가능해요.

Attribution → Partner Management 메뉴 선택 → Add a Partner 버튼을 클릭 → \[Toss]앱 검색
{% endstep %}

{% step %}
**연동 활성화**

Partner Configuration > Attribution Postback & Settings > Tracking Code 에 토스 플랫폼에서 발급받은 전환추적코드 ID를 넣어주세요.

상세한 가이드는 [Singular 연동 가이드](https://support.singular.net/hc/en-us/articles/360053018851-How-to-Configure-Partner-Settings-and-Postbacks)를 참고해주세요.
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th width="176.26995849609375">이벤트 이름</th><th>Toss Ads 이벤트 라벨</th><th>Singular 이벤트 라벨</th></tr></thead><tbody><tr><td>설치</td><td>INSTALL</td><td>install</td></tr><tr><td>앱 오픈</td><td>APP_OPEN</td><td>sng_start_trial</td></tr><tr><td>딥링크 앱 오픈</td><td>APP_DEEPLINK_OPEN</td><td>sng_attr_deep_link</td></tr><tr><td>회원가입</td><td>SIGNUP</td><td>sng_complete_registration</td></tr><tr><td>로그인</td><td>SIGNIN</td><td>sng_login</td></tr><tr><td>결제</td><td>PURCHASE</td><td>sng_ecommerce_purchase</td></tr><tr><td>상품 조회</td><td>PRODUCT_VIEW</td><td>sng_content_view</td></tr><tr><td>장바구니 추가</td><td>ADD_TO_CART</td><td>sng_add_to_cart</td></tr><tr><td>검색</td><td>SEARCH</td><td>sng_search</td></tr><tr><td>결제 시작</td><td>INITIATE_CHECKOUT</td><td>sng_checkout_initiated</td></tr><tr><td>위시리스트 추가</td><td>ADD_TO_WISHLIST</td><td>sng_add_to_wishlist</td></tr><tr><td>구독</td><td>SUBSCRIBE</td><td>sng_subscribe</td></tr></tbody></table>

{% hint style="success" %}
* 연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야 해요.
  * 랜딩 URL은 전환 추적 템플릿으로 생성한 랜딩 URL로 입력해 주세요.
* Singular 이벤트 라벨은 Singular에서 사용 중인 기본 명칭으로 기재되었어요. 자사 서비스에서 발생하는 이벤트를 기준으로 [토스애즈의 표준이벤트](../tag/tracked-events.md)와 가장 적절한 이벤트에 매핑해 주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목 안내

토스애즈에서 **싱귤러**를 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 포함해 주세요.

필수 항목이 누락되면 **어떤 광고에서 전환이 발생했는지 확인하기 어렵고 싱귤러 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

<table><thead><tr><th width="187.420166015625">항목</th><th>값</th><th>설명</th></tr></thead><tbody><tr><td>cl</td><td>{TOSS_TK_CLICK_ID}</td><td>클릭 ID</td></tr><tr><td>idfa / aifa / ad_id</td><td>{IDFA} / {AIFA} / {USER_ADID}</td><td>디바이스 광고 ID</td></tr><tr><td>pcid</td><td>{TOSS_CID}</td><td>캠페인 ID</td></tr></tbody></table>

#### 권장 항목

아래 항목들은 랜딩 URL에 함께 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **캠페인/광고그룹/소재 단위 성과를 세부적으로 확인하기 어렵고 싱귤러 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

<table><thead><tr><th width="146.79949951171875">항목</th><th>값</th><th>설명</th></tr></thead><tbody><tr><td>pcrid</td><td>{TOSS_CREATIVE_ID}</td><td>소재 ID</td></tr><tr><td>site_id</td><td>{SITE_ID}</td><td>매체 ID</td></tr><tr><td>pcn</td><td>{CAMPAIGN_NAME}</td><td>캠페인명</td></tr><tr><td>pcrn</td><td>{CREATIVE_NAME}</td><td>광고 소재명</td></tr><tr><td>pscn</td><td>{ADGROUP_NAME}</td><td>광고 그룹명</td></tr></tbody></table>

#### 링크 구성 예시

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> https://sng.link/abc?<mark style="color:red;">**cl={TOSS\_TK\_CLICK\_ID}\&idfa={IDFA}\&aifa={AIFA}\&ad\_id={USER\_ADID}\&pcid={TOSS\_CID}**</mark>&<mark style="color:blue;">**pcrid={TOSS\_CREATIVE\_ID}\&site\_id={SITE\_ID}\&pcn={CAMPAIGN\_NAME}\&pcrn={CREATIVE\_NAME}\&pscn={ADGROUP\_NAME}**</mark>

####

{% hint style="success" %}
**링크 설정 Tip**

* 콘솔에서 제공하는 click attribution link를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.
  * 자세한 설정 방법은 [싱귤러 트래킹 링크 생성 가이드](https://support.singular.net/hc/en-us/articles/360041317471-Creating-Website-Links)를 참고해 주세요.
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 필수 항목의 구조를 꼭 확인해 주세요.
* Tracking URL에서 수정이 필요한 항목은 캠페인 설정 시 **소재 URL** 섹션에서 다시 확인할 수 있습니다.
{% endhint %}
