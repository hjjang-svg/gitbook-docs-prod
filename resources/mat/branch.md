# 브랜치

### 전환 추적 코드 생성하기&#x20;

{% stepper %}
{% step %}
#### 전환 및 추적 연동

<figure><img src="../../.gitbook/assets/Group 335 (3).png" alt=""><figcaption></figcaption></figure>

전환 및 추적 연동 설정은 아래 경로에서 가능해요.

광고 계정 접속 → 광고 도구 \[전환 및 추적 연동] 선택
{% endstep %}

{% step %}
#### 전환 추적 코드 생성

<figure><img src="../../.gitbook/assets/동의 및 코드 생성-4.png" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성하고 전환 추적 코드의 ID를 복사해주세요.&#x20;
{% endstep %}
{% endstepper %}

***

### 브랜치 연동하기

{% stepper %}
{% step %}
#### 브랜치 연동하기&#x20;

<figure><img src="../../.gitbook/assets/스크린샷 2025-05-08 오후 6.51.49.png" alt=""><figcaption></figcaption></figure>

브랜치 연동 링크 생성은 아래 경로에서 가능해요.

Ad Partners → \[Toss]앱 검색  → Account Settings 탭 → 활성화
{% endstep %}

{% step %}
#### 전환 추적 코드 입력 &#x20;

토스애즈에서 생성하여 복사해둔 전환 추적 코드 ID를 Tracking Code 항목에 입력해주세요
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th width="127">이벤트 이름</th><th width="204.6953125">Toss Ads 이벤트 라벨</th><th width="351.6484375">Branch 이벤트 라벨</th></tr></thead><tbody><tr><td>설치</td><td>INSTALL</td><td>install<br>reinstall</td></tr><tr><td>앱 오픈</td><td>APP_OPEN</td><td>open<br>pageview</td></tr><tr><td>결제</td><td>PURCHASE</td><td>purchase</td></tr><tr><td>상품 조회</td><td>PRODUCT_VIEW</td><td>view_item</td></tr><tr><td>장바구니 추가</td><td>ADD_TO_CART</td><td>add_to_cart</td></tr></tbody></table>

{% hint style="success" %}
* 연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야해요.
  * 랜딩URL은 전환 추적 탬플릿으로 생성한 랜딩 URL로 입력해주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목 <a href="#undefined-11" id="undefined-11"></a>

토스애즈에서 브랜치를 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 들어가야 해요.

필수 항목이 누락되는 경우 **어떤 광고에서 전환이 일어났는지 알 수 없고** **브랜치 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

| 항목             | 값                     | 설명                               |
| -------------- | --------------------- | -------------------------------- |
| $3p            | a\_toss               | Toss Ads 고유 매체 식별자               |
| \~click\_id    | {TOSS\_TK\_CLICK\_ID} | 클릭 발생 시 부여되는 고유 클릭 ID            |
| \~campaign\_id | {TOSS\_CID}           | 캠페인 ID                           |
| $aaid          | {aaid}                | 유저의 ADID (광고 식별자) \* Android에 사용 |
| $idfa          | {idfa}                | 유저의 ADID (광고 식별자) \* iOS에 사용     |

#### 권장 항목

아래 항목은 MMP에서 제공하는 캠페인 운영에 필요한 권장 값이예요. 아래 항목 외에 MMP에서 제공하는 파라미터를 트래킹 링크에 포함하여 구성할 수 있어요.

권장 항목이 빠지거나 잘못 설정되면 **소재별 전환 데이터를 정확하게 추적하기 어려워지고 브랜치 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| \~creative\_id | {TOSS\_CREATIVE\_ID} | 소재 ID |
| -------------- | -------------------- | ----- |
| \~channel      | {SITE\_ID}           | 매체 ID |

#### &#x20;링크 구성 예시

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> https://sample.app.link/sampletest?<mark style="color:red;">**3p=a\_toss\&toss\_click\_id={TOSS\_TK\_CLICK\_ID}\&toss\_campaign\_id={TOSS\_CID}\&aaid={aaid}\&idfa={idfa}**</mark>&<mark style="color:blue;">**toss\_creative\_id={TOSS\_CREATIVE\_ID}\&toss\_channel={SITE\_ID}**</mark>

{% hint style="success" %}
#### **링크 설정 Tip**

* 브랜치 콘솔에서 제공하는 click attribution link를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.
* 토스애즈 가이드에 있는 표준 이벤트와 파라미터가 들어 있는 링크 템플릿을 사용하는 걸 권장해요.
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 표준 키와 구조를 꼭 확인해 주세요.
{% endhint %}
