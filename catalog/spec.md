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

# 카탈로그 연동 스펙

이 문서는 카탈로그에 등록하는 상품 데이터 파일의 규격을 설명해요. 상품마다 필수 상품 정보 여섯 가지를 정확한 형식으로 입력해야 광고에 사용할 수 있어요. 선택 상품 정보를 함께 보내면 할인, 재고, 배송 같은 정보를 더 자세히 전달할 수 있어요. 카탈로그를 만드는 방법과 관리 방법은 [카탈로그 연동 가이드](how-to.md)를 먼저 읽어 주세요. 오류 유형과 해결 방법은 [카탈로그 문제 해결하기](troubleshooting.md)에서 확인할 수 있어요.

## 파일 규격

등록 방식별 파일 준비 방법과 허용 규격을 확인해 주세요.

| 구분       | 자동 등록 (상품 목록 URL)         | 수동 등록 (파일 등록)                                |
| -------- | ------------------------- | -------------------------------------------- |
| 전달 방식    | 상품 데이터베이스 파일이 호스팅되는 URL   | CSV·TSV 파일 직접 등록                             |
| URL 조건   | https://로 시작하는 유효한 URL    | 해당 없음                                        |
| 지원 형식    | CSV·TSV (XML 등 다른 형식 미지원) | CSV·TSV (XML 등 다른 형식 미지원)                    |
| 인코딩 형식   | UTF-8                     | UTF-8                                        |
| 파일 작성 방법 | 첫 행에 영문 컬럼명을 직접 입력        | 이 페이지의 템플릿을 사용하고, 첫 행의 영문 컬럼명을 수정하거나 삭제하지 않음 |
| 최대 크기    | 4GB                       | 100MB                                        |
| 최대 상품 수  | 500만 건                    | 10만 건                                        |

아래 조건을 충족하지 않으면 카탈로그 연동에 실패해요.

* 필수 상품 정보 6가지(`id`, `title`, `brand`, `image_url`, `landing_url`, `price`) 컬럼이 모두 있어야 해요.
* 각 상품에는 필수 상품 정보 6가지의 값이 모두 입력돼 있어야 해요.
* 등록된 상품이 1건 이상이어야 해요.

## 필수 상품 정보 <a href="#required" id="required"></a>

모든 상품에 반드시 입력해야 하는 정보예요. 필수 정보의 값이 비어 있는 상품은 등록되지 않고, 문제 보고서에 기록돼요.

<table data-first-column-sticky><thead><tr><th>상품 정보</th><th>컬럼명</th><th>타입</th><th width="339.83984375">설명</th><th width="339.9296875">입력 규칙</th><th width="299.640625">예시</th></tr></thead><tbody><tr><td>상품 ID</td><td><code>id</code></td><td>string</td><td><ul><li>상품의 고유 ID예요.</li><li>재고 관리에 쓰는 상품 고유 번호(SKU) 사용을 권장해요.</li><li>전환 이벤트의 <code>product_id</code>와 동일한 값이어야 해요.</li></ul></td><td><ul><li>2~100자로 입력해 주세요.</li><li>ID가 중복되면 가장 마지막 상품만 반영되고, 나머지는 노출에서 제외돼요.</li></ul></td><td><code>sku123456</code></td></tr><tr><td>상품명</td><td><code>title</code></td><td>string</td><td><ul><li>광고에 노출되는 상품명이에요.</li></ul></td><td><ul><li>5~100자로 입력해 주세요.</li></ul></td><td><code>토스 생수, 500ml, 10개</code></td></tr><tr><td>브랜드</td><td><code>brand</code></td><td>string</td><td><ul><li>상품의 브랜드명이에요.</li></ul></td><td><ul><li>1~10자로 입력해 주세요.</li><li>5자 이하를 권장해요.</li></ul></td><td><code>토스</code></td></tr><tr><td>이미지 URL</td><td><code>image_url</code></td><td>string (URL)</td><td><ul><li>상품 이미지 주소예요.</li></ul></td><td><ul><li>최대 2,048자로 입력해 주세요.</li><li><code>https://</code>로 시작해야 해요.</li><li>JPG, JPEG, PNG 형식만 허용해요.</li><li>가로와 세로가 모두 500px 이상이어야 해요.</li><li>파일 크기는 8MB 이하여야 해요.</li><li>이미지 비율이 5:7~7:5 범위를 벗어나면 노출되지 않아요. 1:1 비율을 가장 권장해요.</li><li>누구나 접근할 수 있고 HTTP 200 응답을 반환해야 해요.</li><li>이미지에 투명 영역이 없어야 해요. 투명도를 포함한 알파 채널 이미지는 허용하지 않아요.</li></ul></td><td><code>https://www.toss.com/image_1.jpg</code></td></tr><tr><td>랜딩 URL</td><td><code>landing_url</code></td><td>string (URL)</td><td><ul><li>광고 클릭 시 이동하는 상품 상세 페이지 주소예요.</li><li>상품별 개별 전환 추적 URL을 등록해야 해요.</li><li>웹으로 연결한다면 토스 픽셀이 설치된 상품 상세 페이지 URL을 입력해 주세요.</li><li>앱으로 연결한다면 앱 성과 측정 도구(MMP)의 추적 URL을 필수 파라미터와 함께 입력해 주세요.</li><li>앱으로 연결할 때는 토스 사용자의 구매 경험을 위해 fallback 경로를 앱 설치 페이지가 아닌 웹 상품 상세 페이지로 설정하는 것을 권장해요.</li><li><a href="../tracking/mat/">앱 광고 성과 측정 연동(MAT)</a>을 참고해 주세요.</li></ul></td><td><ul><li>최대 2,048자로 입력해 주세요.</li><li><code>https://</code>로 시작해야 해요.</li><li>누구나 접근할 수 있고 HTTP 200 응답을 반환해야 해요.</li><li>전환 추적 URL의 필수 파라미터가 빠지면 오류로 처리돼요.</li></ul></td><td><code>https://www.toss.com/product_1</code></td></tr><tr><td>가격</td><td><code>price</code></td><td>string</td><td><ul><li>상품 가격이에요.</li><li>원화만 지원해요.</li><li>통화 코드를 입력하지 않으면 KRW로 처리돼요.</li><li>할인 중인 상품은 <code>price</code>에 기존 가격을 입력하고 할인 가격은 <code>sale_price</code>에 입력해 주세요.</li></ul></td><td><ul><li>숫자로 변환할 수 있는 1원 이상의 값을 입력해 주세요.</li><li>숫자만 입력하거나 숫자 뒤에 KRW를 붙여 주세요.</li></ul></td><td><code>10000</code> 또는 <code>10000 KRW</code></td></tr></tbody></table>

## 선택 상품 정보

입력하지 않아도 상품 등록에는 문제가 없지만, 입력하면 광고 노출과 성과 측정에 활용돼요. 값이 잘못 입력되면 해당 정보가 광고에 사용되지 않을 수 있어요.

<table data-first-column-sticky><thead><tr><th>상품 정보</th><th width="299.75390625">컬럼명</th><th>타입</th><th width="300.28125">설명</th><th width="300.25390625">입력 규칙</th><th width="299.76953125">예시</th></tr></thead><tbody><tr><td>할인 가격</td><td><code>sale_price</code></td><td>string</td><td><ul><li>할인된 가격이 있으면 할인 가격으로 광고에 노출돼요.</li><li>원화만 지원해요.</li></ul></td><td><ul><li>1원 이상이면서 <code>price</code>보다 낮은 값을 입력해 주세요.</li><li>숫자만 입력하거나 숫자 뒤에 KRW를 붙여 주세요.</li><li>값이 잘못되면 할인 가격 대신 <code>price</code>만 광고에 노출돼요.</li></ul></td><td><code>8000</code> 또는 <code>8000 KRW</code></td></tr><tr><td>설명</td><td><code>description</code></td><td>string</td><td><ul><li>상품 설명이에요.</li><li>상품명과 다른 내용을 권장해요.</li></ul></td><td><ul><li>최대 1,000자로 입력해 주세요.</li></ul></td><td><code>청정 수원지에서 담은 500ml 생수 10개입</code></td></tr><tr><td>할인 기간</td><td><code>sale_price_effective_date</code></td><td>string (ISO 8601)</td><td><ul><li>할인 가격이 유효한 기간이에요.</li><li>기간에 해당하면 <code>sale_price</code>가 광고에 사용돼요.</li><li>값이 없으면 전체 기간 할인 상품으로 인식해요.</li></ul></td><td><ul><li>ISO 8601 형식의 시작 날짜와 종료 날짜를 한 쌍으로 입력해 주세요.</li><li>시작일은 종료일보다 앞서야 해요.</li></ul></td><td><code>2026-07-01T00:00+09:00/2026-07-31T23:59+09:00</code></td></tr><tr><td>재고</td><td><code>availability</code></td><td>string (enum)</td><td><ul><li>재고 상태예요.</li><li>재고가 없는 상품(<code>out of stock</code>, <code>discontinued</code>)은 광고 노출에서 자동으로 제외돼요.</li><li>값이 없으면 재고가 있는 상품으로 인식해요.</li></ul></td><td><ul><li>허용값은 <code>in stock</code>(있음), <code>out of stock</code>(없음), <code>available for order</code>(주문 제작), <code>discontinued</code>(판매 중단)예요.</li></ul></td><td><code>in stock</code></td></tr><tr><td>당일 출고 가능 유무</td><td><code>same_day_shipping_available</code></td><td>string (boolean)</td><td><ul><li>당일 출고가 가능한 상품인지 표시해요.</li><li>값이 없으면 당일 출고가 불가능한 상품으로 인식해요.</li></ul></td><td><ul><li>허용값은 <code>true</code>(가능), <code>false</code>(불가)예요.</li></ul></td><td><code>true</code></td></tr><tr><td>출고 마감 시각</td><td><code>shipping_cutoff_time</code></td><td>string</td><td><ul><li>당일 출고 주문 마감 시각이에요.</li><li><code>same_day_shipping_available=true</code>인 상품에만 입력해요.</li><li>이 시각 이전 주문은 <code>오늘출발</code>, 이후 주문은 <code>내일출발</code> 뱃지로 노출돼요. 영업일을 기준으로 해요.</li></ul></td><td><ul><li>24시간 형식인 HH:mm으로 입력해 주세요.</li><li>30분 단위로 입력해 주세요.</li></ul></td><td><code>12:00</code>, <code>14:30</code>, <code>18:00</code></td></tr><tr><td>배송비</td><td><code>shipping_cost</code></td><td>string (원)</td><td><ul><li>상품별 배송비예요.</li></ul></td><td><ul><li>숫자로 변환할 수 있는 0원 이상의 값을 입력해 주세요.</li><li>숫자만 입력하거나 숫자 뒤에 KRW를 붙여 주세요.</li></ul></td><td><code>2500</code> 또는 <code>0</code>(무료 배송)</td></tr><tr><td>성별</td><td><code>gender</code></td><td>string (enum)</td><td><ul><li>상품이 타게팅하는 성별이에요.</li></ul></td><td><ul><li>허용값은 <code>female</code>(여성), <code>male</code>(남성), <code>unisex</code>(남녀공용)예요.</li></ul></td><td><code>unisex</code></td></tr><tr><td>사이즈</td><td><code>product_size</code></td><td>string</td><td><ul><li>상품 사이즈예요.</li></ul></td><td><ul><li>최대 200자로 입력해 주세요.</li></ul></td><td><code>270</code> 또는 <code>M</code></td></tr><tr><td>색상</td><td><code>color</code></td><td>string</td><td><ul><li>상품의 기본 색상이에요.</li></ul></td><td><ul><li>최대 200자로 입력해 주세요.</li></ul></td><td><code>파란색</code></td></tr><tr><td>맞춤 속성 1~5</td><td><code>custom_label_0</code>, <code>custom_label_1</code>, <code>custom_label_2</code>, <code>custom_label_3</code>, <code>custom_label_4</code></td><td>string</td><td><ul><li>자유롭게 정의하는 속성이에요.</li><li>광고에 직접 노출되지는 않으니 값의 이름과 표기 방식을 미리 정해 일관되게 사용해 주세요.</li></ul></td><td><ul><li>각 항목을 최대 200자로 입력해 주세요.</li></ul></td><td><code>여름기획</code></td></tr></tbody></table>

## 카탈로그 등록 템플릿 <a href="#template" id="template"></a>

자동 등록과 수동 등록 모두 CSV와 TSV 형식을 지원해요. XML 등 다른 형식은 지원하지 않아요.

CSV와 TSV 템플릿에는 필수 항목 6개와 선택 항목 15개의 영문 컬럼명이 입력돼 있어요. 템플릿을 내려받은 뒤 첫 행의 영문 컬럼명을 수정하거나 삭제하지 말고, 두 번째 행부터 상품 정보를 입력해 주세요. 상품 정보가 없는 헤더 전용 파일은 등록할 수 없어요.

상품명이나 설명처럼 값에 쉼표(,)가 들어갈 수 있다면 CSV보다 TSV 템플릿 사용을 권장해요.

{% file src="../.gitbook/assets/toss-ads-catalog-template.csv" %}

{% file src="../.gitbook/assets/toss-ads-catalog-template.tsv" %}

## 등록 전 확인 목록

파일이나 상품 목록 URL을 등록하기 전에 아래 항목을 확인하면 오류를 줄일 수 있어요.

* 상품 데이터 파일이 CSV 또는 TSV 형식이에요.
* 자동 등록용 URL의 첫 행에 영문 컬럼명이 입력돼 있어요.
* 수동 등록용 템플릿의 첫 행에 있는 영문 컬럼명을 수정하거나 삭제하지 않았어요.
* 상품 정보가 입력된 행이 1개 이상이에요.
* 필수 상품 정보 컬럼 6개가 모두 있고, 각 상품에 필수값이 입력돼 있어요.
* 모든 상품의 `id`가 비어 있지 않고 서로 달라요.
* `image_url`과 `landing_url`이 `https://`로 시작하고 외부에서 열려요.
* 이미지의 가로와 세로가 모두 500px 이상이에요.
* 이미지 비율이 5:7\~7:5이고 파일 크기가 8MB 이하예요.
* 이미지가 JPG, JPEG 또는 PNG 형식이고 투명 영역이 없어요.
* 가격과 할인 가격이 원화 형식이고, 할인 가격이 가격보다 낮아요.
* 재고, 당일 출고 가능 유무, 성별에는 허용값만 사용했어요.
* 전환 이벤트의 `product_id`가 상품의 `id`와 같아요.

등록 절차는 [카탈로그 연동 가이드](how-to.md), 등록 후 발생한 문제는 [카탈로그 문제 해결하기](troubleshooting.md), 상품 운영 기준은 [카탈로그 심사 정책](../review/catalog.md)에서 확인할 수 있어요.
