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

# 토스픽셀 TCID 보존 가이드

이 가이드는 토스 픽셀을 설치한 사이트에서 `tcid`를 유지하는 방법을 안내해요.

`tcid`는 토스 광고를 클릭한 사용자를 식별하는 값이에요.

토스 픽셀은 `tcid`를 이용해 광고 클릭과 구매, 회원가입, 상담 신청 같은 전환을 연결해요.

픽셀이 실행되기 전에 `tcid`가 사라지면 광고 클릭과 전환을 연결할 수 없어요



### 꼭 확인하세요

* 광고 랜딩 URL의 `tcid`를 삭제하거나 이름을 변경하지 마세요.
* CDN, WAF, 서버 리다이렉트, 프론트엔드 라우터가 쿼리 스트링을 유지하는지 확인해 주세요.
* 픽셀이 처음 실행되는 페이지까지 `tcid`가 유지되어야 해요.
* 결제, 회원가입처럼 페이지가 바뀌는 경우에도 첫 랜딩 페이지에서 픽셀이 먼저 실행되어야 해요.
* 쿼리 파라미터 Allowlist를 사용하는 경우 `tcid`를 포함해 주세요.



## 픽셀이 읽는 키

`tcid`는 URL에 전달된 값을 그대로 사용해요.

값을 새로 만들거나 수정하지 말고 그대로 유지해 주세요.

```
<https://www.example.com/products/123?**tcid=>...**&utm_source=toss
```



값을 변경하거나 일부를 삭제하면 정상적으로 인식하지 못할 수 있어요.

픽셀은 현재 URL에서 `tcid`를 확인하면 브라우저에 저장해요.

이후 같은 브라우저에서 발생한 전환 이벤트에 저장된 값을 함께 전송해요.



#### tcid 저장 방식

픽셀이 실행되기 전에 `tcid`가 제거되면 저장할 수 없어요.

서버나 프론트엔드에서 URL을 변경하는 경우 `tcid`를 유지하도록 설정해 주세요.

조회 우선순위는 다음과 같아요.

1\. 현재 URL 쿼리 스트링

2\. 브라우저 쿠키

3\. 브라우저 localStorage

