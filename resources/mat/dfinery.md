# 디파이너리

### 전환 추적 코드 생성하기&#x20;

{% stepper %}
{% step %}
#### 전환 및 추적 연동&#x20;

<figure><img src="../../.gitbook/assets/Group 335 (4).png" alt=""><figcaption></figcaption></figure>

전환 및 추적 연동 설정은 아래 경로에서 가능해요.

광고 계정 접속 → 광고 도구 \[전환 및 추적 연동] 선택
{% endstep %}

{% step %}
#### 전환 추적 코드 생성

<figure><img src="../../.gitbook/assets/동의 및 코드 생성-2.png" alt=""><figcaption></figcaption></figure>

코드 명과 연동 방식, 연동 업체를 선택하여 코드를 생성하고 전환 추적 코드의 ID를 복사해주세요.&#x20;
{% endstep %}
{% endstepper %}

***

### 디파이너리 연동하기

{% stepper %}
{% step %}
#### 디파이너리 연동하기&#x20;

디파이너리 연동 링크 생성은 아래 경로에서 가능해요.

Attributions 메뉴 → Ad Partner Settings 선택 \[Toss]앱 검색
{% endstep %}

{% step %}
#### 연동 앱 선택&#x20;

생성한 전환 추적 코드의 ID 값을 복사하여 cvr\_id 항목에 입력해주세요.
{% endstep %}
{% endstepper %}

***

### 전환 이벤트 연동하기

토스애즈에서 수집하는 전환 이벤트 항목은 아래와 같아요.

<table><thead><tr><th width="152.69140625">이벤트 이름</th><th width="277.05859375">Toss Ads 이벤트 라벨</th><th width="525.234375">Dfinery 이벤트 파라미터</th></tr></thead><tbody><tr><td>설치</td><td>INSTALL</td><td>0<br>1</td></tr><tr><td>딥링크 앱 오픈</td><td>APP_DEEPLINK_OPEN</td><td>2</td></tr><tr><td>앱 오픈</td><td>APP_OPEN</td><td>abx:daily_first_open</td></tr><tr><td>회원가입</td><td>SIGNUP</td><td>abx:sign_up</td></tr><tr><td>로그인</td><td>SIGNIN</td><td>abx:login</td></tr><tr><td>결제</td><td>PURCHASE</td><td>abx:purchase</td></tr><tr><td>상품 조회</td><td>PRODUCT_VIEW</td><td>abx:product_view</td></tr><tr><td>장바구니 추가</td><td>ADD_TO_CART</td><td>abx:add_to_cart</td></tr><tr><td>홈 조회</td><td>VIEW_HOME</td><td>abx:view_home</td></tr></tbody></table>

{% hint style="success" %}
* 연동 후 전환 추적을 위해서는 소재를 새롭게 세팅해야해요.
  * 랜딩URL은 전환 추적 탬플릿으로 생성한 랜딩 URL로 입력해주세요.
{% endhint %}

***

### 전환 추적 링크 필수/권장 항목

토스애즈에서 **디파이너리**를 통해 광고 성과를 추적할 때 전환 추적에 필요한 **필수 항목**과 **권장 항목**을 올바르게 설정해야 정확한 데이터를 확인할 수 있어요.

#### 필수 항목

아래 항목들은 서로 짝을 지어 꼭 랜딩 URL에 들어가야 해요.

필수 항목이 누락되는 경우 **어떤 광고에서 전환이 일어났는지 알 수 없고** **디파이너리 대시보드에서도 데이터가 정확하게 집계되지 않을 수 있어요.**

| 항목      | 값                         | 설명                    |
| ------- | ------------------------- | --------------------- |
| cb\_1   | **{TOSS\_TK\_CLICK\_ID}** | 클릭 발생 시 부여되는 고유 클릭 ID |
| m\_ad   | **{TOSS\_CID}**           | 캠페인 ID                |
| m\_adid | **{USER\_ADID}**          | 유저의 ADID (광고 식별자)     |

#### 권장 항목

아래 항목들은 랜딩 URL에 넣는 것을 권장해요.

권장 항목이 빠지거나 잘못 설정되면 **소재별 전환 데이터를 정확하게 추적하기 어려워지고 디파이너리 표준 키와 맞지 않아 트래킹이 누락되거나 잘못 동작할 수 있어요.**

| 항목          | 값                    | 설명    |
| ----------- | -------------------- | ----- |
| m\_creative | {TOSS\_CREATIVE\_ID} | 소재 ID |

### &#x20;링크 구성 예시

모든 <mark style="color:red;">**필수**</mark>**/**<mark style="color:blue;">**권장**</mark> 항목이 포함된 예시 링크

> https://exampleKey.ap1.adtouch.dfinery.io/api/v1/click/example?<mark style="color:red;">**cb\_1={TOSS\_TK\_CLICK\_ID}\&m\_ad={TOSS\_CID}\&m\_adid={USER\_ADID}**</mark>&<mark style="color:blue;">**m\_creative={TOSS\_CREATIVE\_ID}**</mark>

{% hint style="success" %}
#### **링크 설정 Tip**

* 디파이너리 콘솔에서 제공하는 트래킹 링크를 그대로 활용하면 필수/권장 항목을 놓치지 않을 수 있어요.
* 토스애즈 가이드에 있는 표준 이벤트와 파라미터가 들어 있는 링크 템플릿을 사용하는 걸 권장해요.
* 이벤트 매핑이 잘못되면 실제 전환 데이터가 빠질 수 있으니 표준 키와 구조를 꼭 확인해 주세요.
{% endhint %}
