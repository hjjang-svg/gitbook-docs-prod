---
hidden: true
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

# 토스 픽셀 TCID 보존 가이드

## tcid 보존 가이드

#### tcid란?

이 가이드는 토스 픽셀을 설치한 사이트에서 `tcid`를 유지하는 방법을 안내해요.

`tcid`는 토스 광고를 클릭한 사용자를 식별하는 값이에요. 사용자가 토스 광고를 클릭하면 랜딩 URL에 `tcid`가 함께 전달돼요.

토스 픽셀은 `tcid`를 이용해 광고 클릭과 구매, 회원가입, 상담 신청 같은 전환을 연결해요.

픽셀이 실행되기 전에 `tcid`가 사라지면 광고 클릭과 전환을 연결할 수 없어요.

***

#### 꼭 확인해 주세요

* 광고 랜딩 URL의 `tcid`를 삭제하거나 이름을 변경하지 마세요.
* CDN, WAF, 서버 리다이렉트, 프론트엔드 라우터가 쿼리 스트링을 유지하는지 확인해 주세요.
* 픽셀이 처음 실행되는 페이지까지 `tcid`가 유지되어야 해요.
* 결제, 회원가입처럼 페이지가 바뀌는 경우에도 첫 랜딩 페이지에서 픽셀이 먼저 실행되어야 해요.
* 쿼리 파라미터 Allowlist를 사용하는 경우 `tcid`를 포함해 주세요.

***

#### 픽셀이 읽는 값

픽셀은 URL의 쿼리 스트링에서 `tcid`를 확인해요.

예시:&#x20;

```
<https://www.example.com/products/123?**tcid=>...**&utm_source=toss
```

`tcid`는 URL에 전달된 값을 그대로 사용해요.

값을 새로 만들거나 수정하지 말고 그대로 유지해 주세요. 값을 변경하거나 일부를 삭제하면 정상적으로 인식하지 못할 수 있어요.

***

#### tcid 저장 방식

픽셀은 현재 URL에서 `tcid`를 확인하면 브라우저에 저장해요.

이후 같은 브라우저에서 발생한 전환 이벤트에 저장된 값을 함께 전송해요.

조회 순서는 아래와 같아요.

1. 현재 URL의 쿼리 스트링
2. 브라우저 쿠키
3. 브라우저 localStorage

픽셀이 실행되기 전에 `tcid`가 제거되면 저장할 수 없어요.

서버나 프론트엔드에서 URL을 변경하는 경우 `tcid`를 유지하도록 설정해 주세요.

***

## tcid 보존 원칙

{% stepper %}
{% step %}
#### 첫 랜딩 URL의 tcid를 유지해 주세요.

좋은 예시

```
요청 URL: <https://www.example.com/?tcid=abc...&utm_source=toss>
브라우저 최종 URL: <https://www.example.com/?tcid=abc...&utm_source=toss>
```

좋지 않은 예시:&#x20;

```
요청 URL: <https://www.example.com/?tcid=abc...&utm_source=toss>
브라우저 최종 URL: <https://www.example.com/>
```
{% endstep %}

{% step %}
#### URL을 변경해야 한다면 픽셀 실행 후에 진행해 주세요.

사이트 정책상 URL을 정리해야 하는 경우에는 픽셀이 먼저 실행되어 `tcid`를 저장한 뒤 URL을 변경해 주세요.

예시:

```jsx
const pixel = new TossPixel('YOUR_CONVERSION_ID');
pixel.pageView();

// 픽셀 실행 후 필요한 경우에만 주소창 정리
const url = new URL(window.location.href);
url.searchParams.delete('utm_source');
url.searchParams.delete('utm_medium');
window.history.replaceState({}, '', url);
```

`tcid`는 가능한 한 삭제하지 않는 것을 권장해요. 부득이하게 삭제해야 하는 경우에는 픽셀이 먼저 실행되는지 확인해 주세요.
{% endstep %}

{% step %}
#### 가능하면 쿼리 스트링 전체를 유지해 주세요.

리다이렉트나 라우팅 과정에서는 기존 쿼리 스트링 전체를 유지하는 것을 권장해요.

좋은 예시:

```
/landing?tcid=...&utm_source=toss
→ /products?tcid=...&utm_source=toss
```

&#x20;좋지 않은 예시:

```
/landing?tcid=...&utm_source=toss
→ /products?utm_source=toss
```
{% endstep %}
{% endstepper %}

***

## 유실 원인별 대응 방법&#x20;

#### CDN 또는 Edge Rewrite

#### 확인해 주세요

* Rewrite 후에도 쿼리 스트링이 유지되는지
* 캐시 최적화 과정에서 브라우저 URL이 변경되지 않는지
* Edge Function에서 기존 `search` 값을 함께 전달하는지

#### 권장해요

* 리다이렉트 대상 URL에 기존 쿼리 스트링을 유지해 주세요.
* Query Allowlist를 사용하는 경우 `tcid`를 포함해 주세요.
* 캐시 최적화를 하더라도 브라우저 URL에서는 `tcid`를 유지해 주세요.

***

#### 서버 리다이렉트

#### 확인해 주세요

HTTP 응답의 `Location` 헤더로 다른 페이지에 보내는 과정에서 query string이 빠질 수 있습니다. 예를 들어 비로그인 사용자를 로그인 페이지로 보내거나, 모바일 경로로 보내거나, trailing slash를 붙이는 리다이렉트가 여기에 해당합니다.

위험한 예:

```
GET /promo?tcid=...&utm_source=toss
302 Location: /products
```

좋은 예:

```
GET /promo?tcid=...&utm_source=toss
302 Location: /products?tcid=...&utm_source=toss
```

권장 설정:

* 리다이렉트 대상 URL을 만들 때 기존 query string을 복사합니다.
* canonical URL로 이동시키는 리다이렉트에서도 query string을 유지합니다.
* 로그인, 회원가입, 장바구니, 결제 시작 페이지로 이동할 때도 `tcid`를 보존합니다.

***

#### 클라이언트 URL 변경



프론트엔드 코드에서 `history.replaceState`, `router.replace`, `router.push` 등으로 URL을 정리하면서 query string이 사라질 수 있습니다.

위험한 예:

```jsx
window.history.replaceState({}, '', window.location.pathname);
```

좋은 예:

```jsx
const currentUrl = new URL(window.location.href);
window.history.replaceState({}, '', currentUrl.pathname + currentUrl.search + currentUrl.hash);
```

권장 설정:

* 페이지 초기화 직후 실행되는 URL 정리 코드가 있는지 확인합니다.
* 라우터 전환 시 `query`, `searchParams`, `location.search`를 유지합니다.
* URL을 정리해야 한다면 픽셀 초기화와 `pageView()` 호출 이후에 실행합니다.

***

#### SPA 라우팅

*   &#x20;Single Page Application에서는 첫 진입 이후 페이지 이동이 브라우저 새로고침 없이 일어납니다. 첫 진입 URL의 `tcid`가 유지되면 픽셀이 저장할 수 있지만, 초기 라우터가 query string을 제거하면 값이 유실됩니다.

    권장 설정:

    * 앱 bootstrap 시점에 query string을 보존합니다.
    * 첫 `pageView()` 호출 전에 라우터가 `tcid`를 제거하지 않게 합니다.
    * 내부 페이지 이동에서 URL을 재구성할 때 기존 query string을 무조건 버리는 공통 유틸을 사용하지 않습니다.

***

#### 도메인 또는 서브도메인 이동

광고 랜딩은 `www.example.com`이고 결제 완료는 `order.example.com` 또는 외부 결제 도메인에서 일어날 수 있습니다.

픽셀은 브라우저 쿠키와 localStorage를 활용해 식별자를 보존합니다. 같은 루트 도메인의 서브도메인 이동은 쿠키로 이어질 수 있지만, localStorage는 브라우저 origin 단위로 분리됩니다(localStorage는 쿠키가 없는 경우에만 사용됩니다). 첫 랜딩 페이지에서 픽셀이 실행되지 않았거나, 전혀 다른 도메인으로 바로 이동하면 저장 기회가 없을 수 있습니다.

권장 설정:

* 광고 랜딩 페이지에서 픽셀이 먼저 실행되는지 확인합니다.
* 결제, 회원가입, 예약 같은 전환 완료 페이지에도 픽셀을 설치합니다.
* 외부 도메인을 거쳐 돌아오는 흐름에서는 복귀 URL에 `tcid`를 계속 붙일 수 있는지 결제사 또는 플랫폼 설정을 확인합니다.

***

#### 마케팅 링크 단축과 추적 링크

* 실제 광고 클릭과 동일한 방식으로 `tcid`가 최종 URL까지 전달되는지 확인해 주세요.
*   중간 추적 링크가 기존 쿼리 스트링을 삭제하지 않도록 설정해 주세요.&#x20;

    광고 클릭 URL 앞단에 링크 단축기, 내부 트래킹 링크, 캠페인 라우터가 있으면 중간 단계에서 query string이 바뀔 수 있습니다.

    권장 설정:

    * 최종 랜딩 URL까지 `tcid` 가 전달되는지 실제 광고 클릭과 같은 방식으로 테스트합니다.
    * 중간 추적 링크가 자체 파라미터만 남기고 원래 파라미터를 삭제하지 않게 합니다.
    *   링크 단축 서비스의 "query parameter forwarding" 또는 유사 설정을 켭니다.

        &#x20; &#x20;

***

#### 캐시 와 정적 페이지 생성&#x20;

* 브라우저 최종 URL에서는 `tcid`를 유지해 주세요.
* Canonical Redirect가 `tcid`를 삭제하지 않는지 확인해 주세요.
* 캐시된 페이지에서도 현재 URL의 `tcid`를 읽을 수 있는지 확인해 주세요.

***

## QA 체크리스트

사이트 배포 전후 아래 항목을 확인해 주세요.

1. 테스트용 랜딩 URL을 열어주세요.

```
<https://www.example.com/?tcid=aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa-00000000000000000000000000000000&utm_source=toss>
```

1. 페이지가 완전히 로드된 뒤 주소창에 `tcid`가 남아 있는지 확인해주세요.
2. 주소창에서 `tcid`가 사라진다면, 사라지는 시점이 서버 리다이렉트인지 프론트엔드 URL 정리인지 확인해주세요.
3. 브라우저 개발자 도구의 Network 탭에서 픽셀 이벤트 요청을 찾아주새요.&#x20;

```
<https://lex.toss.im/api/lex/event/v2>
```

1. 요청 본문에 `tcid`가 포함되어 있는지 확인해주세요.&#x20;
2. 구매, 회원가입, 상담 신청 같은 실제 전환 완료 페이지에서도 이벤트 요청이 발생하고 `tcid`가 포함되는지 확인해주세요.&#x20;
3. CDN, WAF, 서버, 프론트엔드 라우터 설정 변경 후 같은 테스트를 반복해주세요.&#x20;

***

## 개발팀 확인 사항

아래 항목을 개발팀 또는 인프라 담당자에게 전달해 주세요.

* 광고 랜딩 URL의 query string을 삭제하지 않아요.
* 서버 리다이렉트의 Location URL에 기존 query string을 유지해요.
* CDN/Edge rewrite에서 기존 query string을 목적지 URL에 전달해요.
* WAF 또는 보안 프록시의 query allowlist에 tcid를 포함해요.
* 프론트엔드 URL 정규화 로직이 픽셀 실행 전에 tcid 삭제되지 않도록 설정해요.
* 전환 완료 페이지에도 픽셀이 설치되어 있고 정상적으로 이벤트를 전송하는지 확인해요.

***

## 전환 누락이 의심된다면

아래 순서대로 확인해 주세요.

1. 광고 클릭 URL에 `tcid`가 포함되어 있는지 확인해요.
2. 최종 랜딩 URL까지 `tcid`가 유지되는지 확인해요.
3. 픽셀 이벤트 요청에 `tcid`가 포함되어 있는지 확인해요.
4. 전환 완료 페이지에서 이벤트가 정상적으로 전송되는지 확인해요.
5. 최근 CDN, WAF, 리다이렉트, 라우터 설정이 변경된 것은 없는지 확인해요.

최종 랜딩 URL에는 `tcid`가 있지만 이벤트 요청에는 없다면 픽셀 설치 또는 실행 순서를 확인해 주세요.

반대로 최종 랜딩 URL에서 `tcid`가 이미 사라졌다면 픽셀 문제가 아니라 URL 전달 과정에서 값이 유실된 것이에요.
