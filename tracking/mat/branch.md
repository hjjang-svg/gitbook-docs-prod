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

# 브랜치

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

<figure><img src="../../.gitbook/assets/동의 및 코드 생성-4.png" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성하고 전환 추적 코드의 ID를 복사해주세요.
{% endstep %}
{% endstepper %}

***

### 브랜치 연동하기

{% stepper %}
{% step %}
**브랜치 연동 경로**

브랜치 연동 링크 생성은 아래 경로에서 가능해요.

Ad Partners → \[Toss]앱 검색 → Account Settings 탭
{% endstep %}

{% step %}
**전환 추적 코드 입력**

<figure><img src="../../.gitbook/assets/스크린샷 2025-05-08 오후 6.51.49.png" alt=""><figcaption></figcaption></figure>

Ad Account Information > Tracking Code에 토스 플랫폼에서 발급받은 전환추적코드 ID를 넣어주세요.

상세한 가이드는 [Branch 연동 가이드](https://help.branch.io/marketer-hub/docs/ad-partner-integration-guide)를 참고해주세요.
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th width="159.05645751953125">이벤트 이름</th><th>Toss Ads 이벤트 라벨</th><th>Branch 이벤트 라벨</th></tr></thead><tbody><tr><td>설치</td><td>INSTALL</td><td>install / reinstall</td></tr><tr><td>앱 오픈</td><td>APP_OPEN</td><td>open / pageview</td></tr><tr><td>회원가입</td><td>SIGNUP</td><td>COMPLETE_REGISTRATION</td></tr><tr><td>로그인</td><td>SIGNIN</td><td>LOGIN</td></tr><tr><td>결제</td><td>PURCHASE</td><td>PURCHASE</td></tr><tr><td>상품 조회</td><td>PRODUCT_VIEW</td><td>VIEW_ITEM</td></tr><tr><td>장바구니 추가</td><td>ADD_TO_CART</td><td>ADD_TO_CART</td></tr><tr><td>검색</td><td>SEARCH</td><td>SEARCH</td></tr><tr><td>결제 시작</td><td>INITIATE_CHECKOUT</td><td>INITIATE_PURCHASE</td></tr><tr><td>위시리스트 추가</td><td>ADD_TO_WISHLIST</td><td>ADD_TO_WISHLIST</td></tr></tbody></table>

{% hint style="success" %}
* 연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야 해요.
  * 랜딩 URL은 전환 추적 템플릿으로 생성한 랜딩 URL로 입력해 주세요.
* Branch 이벤트 라벨은 Branch에서 사용 중인 기본 명칭으로 기재되었어요. 자사 서비스에서 발생하는 이벤트를 기준으로 [토스애즈의 표준이벤트](../tag/tracked-events.md)와 가장 적절한 이벤트에 매핑해 주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목 <a href="#branch-link-parameters" id="branch-link-parameters"></a>

토스애즈에서 **브랜치**를 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 포함해 주세요.

필수 항목이 누락되면 **어떤 광고에서 전환이 발생했는지 확인하기 어렵고 브랜치 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

| 항목             | 값                     | 설명                               |
| -------------- | --------------------- | -------------------------------- |
| $3p            | a\_toss               | Toss Ads 고유 매체 식별자               |
| \~click\_id    | {TOSS\_TK\_CLICK\_ID} | 클릭 발생 시 부여되는 고유 클릭 ID            |
| \~campaign\_id | {TOSS\_CID}           | 캠페인 ID                           |
| $aaid          | {aaid}                | 유저의 ADID (광고 식별자) \* Android에 사용 |
| $idfa          | {idfa}                | 유저의 ADID (광고 식별자) \* iOS에 사용     |

#### 권장 항목

아래 항목들은 랜딩 URL에 함께 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **소재 단위 성과를 세부적으로 확인하기 어렵고 브랜치 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| 항목             | 값                        | 설명    |
| -------------- | ------------------------ | ----- |
| \~creative\_id | **{TOSS\_CREATIVE\_ID}** | 소재 ID |

#### 링크 구성 예시

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> https://app.link/abc?<mark style="color:red;">**$3p=a\_toss&\~click\_id={TOSS\_TK\_CLICK\_ID}&$idfa={idfa}&$aaid={aaid}&\~campaign\_id={TOSS\_CID}&\~channel={SITE\_ID}**</mark>&<mark style="color:blue;">**\~creative\_id={TOSS\_CREATIVE\_ID}**</mark>

{% hint style="success" %}
**링크 설정 Tip**

* 브랜치 콘솔에서 제공하는 click attribution link를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.
  * 자세한 설정 방법은 브랜치 트래킹 링크 생성 가이드를 참고해 주세요.
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 필수 항목의 구조를 꼭 확인해 주세요.
* Tracking URL에서 수정이 필요한 항목은 캠페인 설정 시 **소재 URL** 섹션에서 다시 확인할 수 있습니다.
{% endhint %}
