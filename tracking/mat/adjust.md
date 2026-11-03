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

# 애드저스트

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

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FUk9PAffikEAX8FhRtzd0%2F%E1%84%83%E1%85%A9%E1%86%BC%E1%84%8B%E1%85%B4%20%E1%84%86%E1%85%B5%E1%86%BE%20%E1%84%8F%E1%85%A9%E1%84%83%E1%85%B3%20%E1%84%89%E1%85%A2%E1%86%BC%E1%84%89%E1%85%A5%E1%86%BC-5.png?alt=media&#x26;token=2efc8004-925c-498c-90ab-5f3431979c94" alt=""><figcaption></figcaption></figure>

전환 및 추적 연동 사용에 동의한 뒤\
코드명, 연동 방식, 업체를 선택해 코드를 생성해요.
{% endstep %}

{% step %}
**생성 여부 확인**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2F1PCuHozoWyi8m7mDS8NV%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202026-02-20%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.20.00%205.png?alt=media&#x26;token=a727140f-da08-495f-95b6-d6188fd88026" alt=""><figcaption></figcaption></figure>

설정한 정보에 맞게 생성된 전환 추적 코드의 ID를 복사하여 연동할 수 있어요.
{% endstep %}
{% endstepper %}

***

### 애드저스트 연동하기 <a href="#connect-adjust" id="connect-adjust"></a>

{% stepper %}
{% step %}
**애드저스트 연동 경로**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FlDToj6CWxyGFAJc4pwFr%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202024-09-13%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.13.12.png?alt=media&#x26;token=3e8d4bc5-0d47-4873-8b98-233af7f56540" alt=""><figcaption></figcaption></figure>

애드저스트 연동 링크 생성은 아래 경로에서 가능해요.

Campaign Lab → Partners 선택
{% endstep %}

{% step %}
**연동 앱 선택**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2Fvul0kCUgyowP77WZKYed%2Ftoss-ads-01.png?alt=media&#x26;token=482c8c51-b722-456a-bab6-c1ae881cfe6b" alt=""><figcaption></figcaption></figure>

우측 상단 New Partner 버튼 선택 → \[Toss]앱 검색
{% endstep %}

{% step %}
**연동 활성화**

<figure><img src="https://1103230780-files.gitbook.io/~/files/v0/b/gitbook-x-prod.appspot.com/o/spaces%2F6C6VnjnrKC0ixISOKw0d%2Fuploads%2FRphZGleDWoHIvZGIlvU6%2F%E1%84%89%E1%85%B3%E1%84%8F%E1%85%B3%E1%84%85%E1%85%B5%E1%86%AB%E1%84%89%E1%85%A3%E1%86%BA%202024-09-13%20%E1%84%8B%E1%85%A9%E1%84%92%E1%85%AE%202.13.53.png?alt=media&#x26;token=25dd72ea-7c7e-4fd4-8cf0-30e60e64d0ac" alt=""><figcaption></figcaption></figure>

* 연동 페이지로 들어가 토스 플랫폼에서 발급받은 전환 추적 코드 ID를 넣어주세요.
* 전송 규칙은 Data from all attribution sources로 설정해주세요.
* 상세한 가이드는 [Adjust 연동 가이드](https://help.adjust.com/ko/partner-setup/toss)를 참고해주세요.
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기 <a href="#event-mapping" id="event-mapping"></a>

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th>토스애즈 이벤트 라벨</th><th>Adjust 이벤트 라벨</th><th width="178.70050048828125">이벤트명</th></tr></thead><tbody><tr><td>AD_IMPRESSION</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>인앱 광고 노출</td></tr><tr><td>ADD_TO_CART</td><td>Add to basket</td><td>장바구니 추가</td></tr><tr><td>ADD_TO_WISHLIST</td><td>Add to wishlist</td><td>위시리스트 추가</td></tr><tr><td>APP_DEEPLINK_OPEN</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>딥링크 열기</td></tr><tr><td>APP_OPEN</td><td>session</td><td>앱 오픈</td></tr><tr><td>APPLY_SCREENING</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>가심사 조회</td></tr><tr><td>FIRST_PURCHASE</td><td>First sale</td><td>첫 구매</td></tr><tr><td>GET_OFFER</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>쿠폰 다운로드</td></tr><tr><td>INITIATE_CHECKOUT</td><td>Sale / checkout</td><td>결제 시작</td></tr><tr><td>INSTALL</td><td>install / reinstall</td><td>설치</td></tr><tr><td>LEAD_COLLECTION</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>잠재 고객</td></tr><tr><td>LEVEL_ACHIEVED</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>레벨 달성</td></tr><tr><td>PAGE_VIEW</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>페이지 조회</td></tr><tr><td>PRE_REGISTER</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>사전 예약</td></tr><tr><td>PRODUCT_VIEW</td><td>View product</td><td>상품 조회</td></tr><tr><td>PURCHASE</td><td>Gadget purchase / In-app purchase</td><td>결제</td></tr><tr><td>SEARCH</td><td>Search product / Search (Travel)</td><td>검색</td></tr><tr><td>SIGNIN</td><td>Login</td><td>로그인</td></tr><tr><td>SIGNUP</td><td>Sign up / Registration</td><td>회원가입</td></tr><tr><td>SUBSCRIBE</td><td>Buy 1/3/6-month subscription</td><td>구독</td></tr><tr><td>TUTORIAL</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>튜토리얼</td></tr><tr><td>VIEW_HOME</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>홈 조회</td></tr><tr><td>VIEW_LIMIT</td><td>담당 AM과 상의 (아래 안내 참고)</td><td>한도 조회</td></tr></tbody></table>

{% hint style="warning" %}
**일부 이벤트는 담당 AM에게 별도로 요청해야 해요.**

표에서 '담당 AM과 상의'로 적힌 이벤트는 Adjust 설정과 별개로 토스애즈에서 추가 작업이 필요해요. 게임 이벤트 `TUTORIAL`, `LEVEL_ACHIEVED`도 여기에 해당해요. 커스텀 이벤트 설정과 매핑 방법은 담당 AM과 상의해 주세요.
{% endhint %}

{% hint style="success" %}
연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야 해요.

* 랜딩 URL은 전환 추적 템플릿으로 생성한 랜딩 URL로 입력해 주세요.

Adjust 이벤트 라벨은 Adjust에서 사용 중인 기본 명칭으로 기재되었어요. 자사 서비스에서 발생하는 이벤트를 기준으로 [토스애즈의 표준이벤트](../tag/tracked-events.md)와 가장 적절한 이벤트에 매핑해 주세요.

**구매 유도하기(카탈로그 연동)**&#xB97C; 운영한다면 상품 정보(product)를 받기 위해 토스애즈와 따로 연동해야 해요. 구매 이벤트에서 product\_id로 쓰는 파라미터를 미리 확인해 담당 AM에게 알려 주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목 <a href="#adjust-link-parameters" id="adjust-link-parameters"></a>

토스애즈에서 **애드저스트**로 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목 <a href="#required-parameters" id="required-parameters"></a>

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 포함해 주세요.

필수 항목이 누락되면 **어떤 광고에서 전환이 발생했는지 확인하기 어렵고 애드저스트 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

| 항목                 | 값                     | 설명                    |
| ------------------ | --------------------- | --------------------- |
| toss\_click\_id    | {TOSS\_TK\_CLICK\_ID} | 클릭 발생 시 부여되는 고유 클릭 ID |
| idfa / gps\_adid   | {IDFA} / {AIFA}       | 디바이스 광고 ID            |
| toss\_campaign\_id | {TOSS\_CID}           | 캠페인 ID                |

#### 권장 항목 <a href="#recommended-parameters" id="recommended-parameters"></a>

아래 항목들은 랜딩 URL에 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **캠페인/광고그룹/소재 단위 성과를 세부적으로 확인하기 어렵고 애드저스트 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| 항목                 | 값                    | 설명     |
| ------------------ | -------------------- | ------ |
| toss\_creative\_id | {TOSS\_CREATIVE\_ID} | 소재 ID  |
| toss\_site\_id     | {SITE\_ID}           | 매체 ID  |
| campaign           | {CAMPAIGN\_NAME}     | 캠페인명   |
| adgroup            | {ADGROUP\_NAME}      | 광고 그룹명 |

#### **링크 구성 예시** <a href="#link-example" id="link-example"></a>

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> https://app.adjust.com/abc?<mark style="color:red;">**toss\_click\_id={TOSS\_TK\_CLICK\_ID}\&idfa={IDFA}\&gps\_adid={AIFA}\&toss\_campaign\_id={TOSS\_CID}**</mark>&<mark style="color:blue;">**toss\_creative\_id={TOSS\_CREATIVE\_ID}\&toss\_site\_id={SITE\_ID}\&campaign={CAMPAIGN\_NAME}\&adgroup={ADGROUP\_NAME}**</mark>

{% hint style="success" %}
**링크 설정 Tip**

* 애드저스트 콘솔에서 제공하는 click attribution link를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.
  * 자세한 설정 방법은 [애드저스트 트래킹 링크 생성 가이드](https://ior.ad/ado1)를 참고해 주세요.
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 필수 항목의 구조를 꼭 확인해 주세요.
* Tracking URL에서 고쳐야 할 항목은 캠페인을 설정할 때 **소재 URL** 섹션에서 다시 확인할 수 있어요.
{% endhint %}
