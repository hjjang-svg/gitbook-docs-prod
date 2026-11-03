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

# 브랜치

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

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FjliZuvRCeNoB5ww4u3uH%2F%E1%84%83%E1%85%A9%E1%86%BC%E1%84%8B%E1%85%B4%20%E1%84%86%E1%85%B5%E1%86%BE%20%E1%84%8F%E1%85%A9%E1%84%83%E1%85%B3%20%E1%84%89%E1%85%A2%E1%86%BC%E1%84%89%E1%85%A5%E1%86%BC-4.png?alt=media&#x26;token=9e99033d-b5d9-4f73-a239-9afe144d7a1c" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성하고 전환 추적 코드의 ID를 복사해주세요.
{% endstep %}
{% endstepper %}

***

### 브랜치 연동하기 <a href="#connect-branch" id="connect-branch"></a>

{% stepper %}
{% step %}
**브랜치 연동 경로**

브랜치 연동 링크 생성은 아래 경로에서 가능해요.

Ad Partners → \[Toss]앱 검색 → Account Settings 탭
{% endstep %}

{% step %}
**전환 추적 코드 입력**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2Fl7wYJh4z9CssyAZ2DBlN%2F%EC%8A%A4%ED%81%AC%EB%A6%B0%EC%83%B7%202025-05-08%20%EC%98%A4%ED%9B%84%206.51.49.png?alt=media&#x26;token=079ccadc-0a21-4af4-baf2-6d56530f3039" alt=""><figcaption></figcaption></figure>

Ad Account Information > Tracking Code에 토스 플랫폼에서 발급받은 전환 추적 코드 ID를 넣어주세요.

상세한 가이드는 [Branch 연동 가이드](https://help.branch.io/marketer-hub/docs/ad-partner-integration-guide)를 참고해주세요.
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기 <a href="#event-mapping" id="event-mapping"></a>

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th>토스애즈 이벤트 라벨</th><th>Branch 이벤트 라벨</th><th width="159.05645751953125">이벤트명</th></tr></thead><tbody><tr><td>AD_IMPRESSION</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>인앱 광고 노출</td></tr><tr><td>ADD_TO_CART</td><td>ADD_TO_CART</td><td>장바구니 추가</td></tr><tr><td>ADD_TO_WISHLIST</td><td>ADD_TO_WISHLIST</td><td>위시리스트 추가</td></tr><tr><td>APP_DEEPLINK_OPEN</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>딥링크 열기</td></tr><tr><td>APP_OPEN</td><td>open / pageview</td><td>앱 오픈</td></tr><tr><td>APPLY_SCREENING</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>가심사 조회</td></tr><tr><td>FIRST_PURCHASE</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>첫 구매</td></tr><tr><td>GET_OFFER</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>쿠폰 다운로드</td></tr><tr><td>INITIATE_CHECKOUT</td><td>INITIATE_PURCHASE</td><td>결제 시작</td></tr><tr><td>INSTALL</td><td>install / reinstall</td><td>설치</td></tr><tr><td>LEAD_COLLECTION</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>잠재 고객</td></tr><tr><td>LEVEL_ACHIEVED</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>레벨 달성</td></tr><tr><td>PAGE_VIEW</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>페이지 조회</td></tr><tr><td>PRE_REGISTER</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>사전 예약</td></tr><tr><td>PRODUCT_VIEW</td><td>VIEW_ITEM</td><td>상품 조회</td></tr><tr><td>PURCHASE</td><td>PURCHASE</td><td>결제</td></tr><tr><td>SEARCH</td><td>SEARCH</td><td>검색</td></tr><tr><td>SIGNIN</td><td>LOGIN</td><td>로그인</td></tr><tr><td>SIGNUP</td><td>COMPLETE_REGISTRATION</td><td>회원가입</td></tr><tr><td>SUBSCRIBE</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>구독</td></tr><tr><td>TUTORIAL</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>튜토리얼</td></tr><tr><td>VIEW_HOME</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>홈 조회</td></tr><tr><td>VIEW_LIMIT</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>한도 조회</td></tr></tbody></table>

{% hint style="warning" %}
**일부 이벤트는 담당 AM에게 별도로 요청해야 해요.**

표에서 '담당 AM과 상의'로 적힌 이벤트는 Branch 설정과 별개로 토스애즈에서 추가 작업이 필요해요. 게임 이벤트 `TUTORIAL`, `LEVEL_ACHIEVED`도 여기에 해당해요. 커스텀 이벤트의 포스트백 설정과 매핑 방법은 담당 AM과 상의해 주세요.
{% endhint %}

{% hint style="success" %}
연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야 해요.

* 랜딩 URL은 전환 추적 템플릿으로 생성한 랜딩 URL로 입력해 주세요.

Branch 이벤트 라벨은 Branch에서 사용 중인 기본 명칭으로 기재되었어요. 자사 서비스에서 발생하는 이벤트를 기준으로 [토스애즈의 표준이벤트](../tag/tracked-events.md)와 가장 적절한 이벤트에 매핑해 주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목 <a href="#branch-link-parameters" id="branch-link-parameters"></a>

토스애즈에서 **브랜치**를 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목 <a href="#required-parameters" id="required-parameters"></a>

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 포함해 주세요.

필수 항목이 누락되면 **어떤 광고에서 전환이 발생했는지 확인하기 어렵고 브랜치 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

| 항목             | 값                     | 설명                               |
| -------------- | --------------------- | -------------------------------- |
| $3p            | a\_toss               | 토스애즈 고유 매체 식별자                   |
| \~click\_id    | {TOSS\_TK\_CLICK\_ID} | 클릭 발생 시 부여되는 고유 클릭 ID            |
| \~campaign\_id | {TOSS\_CID}           | 캠페인 ID                           |
| $aaid          | {aaid}                | 유저의 ADID (광고 식별자) \* Android에 사용 |
| $idfa          | {idfa}                | 유저의 ADID (광고 식별자) \* iOS에 사용     |

#### 권장 항목 <a href="#recommended-parameters" id="recommended-parameters"></a>

아래 항목들은 랜딩 URL에 함께 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **소재 단위 성과를 세부적으로 확인하기 어렵고 브랜치 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| 항목             | 값                    | 설명    |
| -------------- | -------------------- | ----- |
| \~channel      | {SITE\_ID}           | 매체 ID |
| \~creative\_id | {TOSS\_CREATIVE\_ID} | 소재 ID |

#### 링크 구성 예시 <a href="#link-example" id="link-example"></a>

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> [https://app.link/abc](https://app.link/abc)?<mark style="color:red;">**$3p=a\_toss&\~click\_id={TOSS\_TK\_CLICK\_ID}&$idfa={idfa}&$aaid={aaid}&\~campaign\_id={TOSS\_CID}&**</mark><mark style="color:blue;">**\~channel={SITE\_ID}**</mark><mark style="color:blue;">&</mark><mark style="color:blue;">**\~creative\_id={TOSS\_CREATIVE\_ID}**</mark>

{% hint style="success" %}
**링크 설정 Tip**

* 브랜치 콘솔에서 제공하는 click attribution link를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.
  * 자세한 설정 방법은 [브랜치 트래킹 링크 생성 가이드](../../a-d/app-install/link-guide.md#branch)를 참고해 주세요.
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 필수 항목의 구조를 꼭 확인해 주세요.
* Tracking URL에서 수정이 필요한 항목은 캠페인을 설정할 때 **소재 URL** 섹션에서 다시 확인할 수 있어요.
{% endhint %}
