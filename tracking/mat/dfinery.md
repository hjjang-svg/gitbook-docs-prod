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

# 디파이너리

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

<figure><img src="../../.gitbook/assets/동의 및 코드 생성-2.png" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성하고 전환 추적 코드의 ID를 복사해주세요.
{% endstep %}
{% endstepper %}

***

### 디파이너리 연동하기

{% stepper %}
{% step %}
**디파이너리 연동 경로**

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption></figcaption></figure>

디파이너리 연동 링크 생성은 아래 경로에서 가능해요.

Attributions 메뉴 → Ad Partner Settings 선택 \[Toss]앱 검색
{% endstep %}

{% step %}
**연동 활성화**

Ad Partner Information 탭의 Tracking Code에 토스 플랫폼에서 발급받은 전환추적코드 ID를 넣어주세요.

상세한 가이드는 [Dfinery 연동 가이드](https://help.dfinery.io/hc/ko/articles/14842338029593-Ad-partner-settings-%EA%B4%91%EA%B3%A0-%ED%8C%8C%ED%8A%B8%EB%84%88-%EB%A7%A4%EC%B2%B4-%EC%A0%95%EC%9D%98-%EB%B0%8F-%ED%99%9C%EC%84%B1%ED%99%94-%ED%95%98%EA%B8%B0)를 참고해주세요.
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th width="173.80902099609375">이벤트 이름</th><th>Toss Ads 이벤트 라벨</th><th>Dfinery 이벤트 라벨</th></tr></thead><tbody><tr><td>설치</td><td>INSTALL</td><td>0 / 1 / abx:new_install</td></tr><tr><td>딥링크 앱 오픈</td><td>APP_DEEPLINK_OPEN</td><td>2 / abx:deeplink_open</td></tr><tr><td>앱 오픈</td><td>APP_OPEN</td><td>abx:daily_first_open / abx:firstopen</td></tr><tr><td>회원가입</td><td>SIGNUP</td><td>abx:sign_up</td></tr><tr><td>로그인</td><td>SIGNIN</td><td>abx:login</td></tr><tr><td>결제</td><td>PURCHASE</td><td>abx:purchase</td></tr><tr><td>상품 조회</td><td>PRODUCT_VIEW</td><td>abx:product_view</td></tr><tr><td>장바구니 추가</td><td>ADD_TO_CART</td><td>abx:add_to_cart</td></tr><tr><td>검색</td><td>SEARCH</td><td>abx:search</td></tr><tr><td>결제 시작</td><td>INITIATE_CHECKOUT</td><td>abx:review_order</td></tr><tr><td>위시리스트 추가</td><td>ADD_TO_WISHLIST</td><td>abx:add_to_wishlist</td></tr><tr><td>홈 조회</td><td>VIEW_HOME</td><td>abx:view_home</td></tr></tbody></table>

{% hint style="success" %}
* 연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야 해요.
  * 랜딩 URL은 전환 추적 템플릿으로 생성한 랜딩 URL로 입력해 주세요.
* Dfinery 이벤트 라벨은 Dfinery에서 사용 중인 기본 명칭으로 기재되었어요. 자사 서비스에서 발생하는 이벤트를 기준으로 [토스애즈의 표준이벤트](../tag/tracked-events.md)와 가장 적절한 이벤트에 매핑해 주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목

토스애즈에서 **디파이너리**를 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 포함해 주세요.

필수 항목이 누락되면 **어떤 광고에서 전환이 발생했는지 확인하기 어렵고 디파이너리 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

| 항목      | 값                     | 설명          |
| ------- | --------------------- | ----------- |
| cb\_1   | {TOSS\_TK\_CLICK\_ID} | 클릭 ID       |
| m\_adid | {USER\_ADID}          | ADID / IDFA |
| m\_ad   | {TOSS\_CID}           | 캠페인 ID      |

#### 권장 항목

아래 항목들은 랜딩 URL에 함께 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **캠페인/광고그룹/소재 단위 성과를 세부적으로 확인하기 어렵고 디파이너리 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| 항목          | 값                    | 설명     |
| ----------- | -------------------- | ------ |
| m\_creative | {TOSS\_CREATIVE\_ID} | 소재 ID  |
| m\_campaign | {CAMPAIGN\_NAME}     | 캠페인명   |
| cb\_2       | {SITE\_ID}           | 매체 ID  |
| cb\_3       | {CREATIVE\_NAME}     | 광고 소재명 |
| m\_adgroup  | {ADGROUP\_NAME}      | 광고 그룹명 |

### 링크 구성 예시

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> https://adbrix.io/link?<mark style="color:red;">**cb\_1={TOSS\_TK\_CLICK\_ID}\&m\_adid={USER\_ADID}\&m\_ad={TOSS\_CID}**</mark>&<mark style="color:blue;">**m\_creative={TOSS\_CREATIVE\_ID}\&m\_campaign={CAMPAIGN\_NAME}\&cb\_2={SITE\_ID}\&cb\_3={CREATIVE\_NAME}\&m\_adgroup={ADGROUP\_NAME}**</mark>

{% hint style="success" %}
**링크 설정 Tip**

* 디파이너리 콘솔에서 제공하는 click attribution link를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.
  * 자세한 설정 방법은 [디파이너리 트래킹 링크 생성 가이드](https://help.dfinery.io/hc/ko/articles/360024465693-Ad-Campaign-%EC%83%9D%EC%84%B1%EA%B3%BC-Tracking-Link-%EB%B0%9C%EA%B8%89)를 참고해 주세요.
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 필수 항목의 구조를 꼭 확인해 주세요.
* Tracking URL에서 수정이 필요한 항목은 캠페인 설정 시 **소재 URL** 섹션에서 다시 확인할 수 있습니다.
{% endhint %}
