---
title: Azure Data Factory Mapping Data Flow 식 함수
description: Azure Data Factory Mapping Data Flow 식 함수
author: kromerm
ms.author: makromer
ms.reviewer: douglasl
ms.service: data-factory
ms.topic: conceptual
ms.date: 02/15/2019
ms.openlocfilehash: 793624b34c718abccaeeff5b0fe3b83f446d0809
ms.sourcegitcommit: 2d0fb4f3fc8086d61e2d8e506d5c2b930ba525a7
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/18/2019
ms.locfileid: "58171009"
---
# <a name="mapping-data-flow-data-transformation-expressions"></a>데이터 흐름 데이터 변환 식 매핑

[!INCLUDE [notes](../../includes/data-factory-data-flow-preview.md)]

## <a name="expression-functions"></a>식 함수

Data Factory Mapping Data Flow에는 데이터 변환을 구성하는 데 사용할 수 있는 식 언어가 있습니다.

<code>abs</code>
==============================
<code><b>abs(<i>&lt;value1&gt;</i> : number) => number</b></code><br/><br/>
숫자 쌍의 양의 모듈러스입니다.
* ``abs(-20) -> 20``
* ``abs(10) -> 10``
*********************************
<code>acos</code>
==============================
<code><b>acos(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
역코사인 값을 계산합니다. * ``acos(1) -> 0.0``
*********************************
<code>add</code>
==============================
<code><b>add(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => any</b></code><br/><br/>
문자열 또는 숫자의 쌍을 추가합니다. 날짜에 일 수를 추가합니다. 유사한 형식의 한 배열을 다른 배열에 추가합니다. + 연산자와 같습니다. * ``add(10, 20) -> 30``
* ``10 + 20 -> 30``
* ``add('ice', 'cream') -> 'icecream'``
* ``'ice' + 'cream' + ' cone' -> 'icecream cone'``
* ``add(toDate('2012-12-12'), 3) -> 2012-12-15 (date value)``
* ``toDate('2012-12-12') + 3 -> 2012-12-15 (date value)``
* ``[10, 20] + [30, 40] => [10, 20, 30, 40]``
*********************************
<code>addDays</code>
==============================
<code><b>addDays(<i>&lt;date/timestamp&gt;</i> : datetime, <i>&lt;days to add&gt;</i> : integral) => datetime</b></code><br/><br/>
날짜 또는 타임스탬프에 일을 추가합니다. 날짜에 대한 + 연산자와 같습니다. * ``addDays(toDate('2016-08-08'), 1) -> 2016-08-09``
*********************************
<code>addMonths</code>
==============================
<code><b>addMonths(<i>&lt;date/timestamp&gt;</i> : datetime, <i>&lt;months to add&gt;</i> : integral) => datetime</b></code><br/><br/>
날짜 또는 타임스탬프에 월을 추가합니다. * ``addMonths(toDate('2016-08-31'), 1) -> 2016-09-30``
* ``addMonths(toTimestamp('2016-09-30 10:10:10'), -1) -> 2016-08-31 10:10:10``
*********************************
<code>and</code>
==============================
<code><b>and(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : boolean) => boolean</b></code><br/><br/>
논리 AND 연산자입니다. &&와 같습니다. * ``and(true, false) -> false``
* ``true && false -> false``
*********************************
<code>asin</code>
==============================
<code><b>asin(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
역 사인 값을 계산합니다. * ``asin(0) -> 0.0``
*********************************
<code>atan</code>
==============================
<code><b>atan(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
역 탄젠트 값을 계산합니다. * ``atan(0) -> 0.0``
*********************************
<code>atan2</code>
==============================
<code><b>atan2(<i>&lt;value1&gt;</i> : number, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
평면의 양의 x축과 좌표로 지정된 점 사이의 라디안 각도를 반환합니다. * ``atan2(0, 0) -> 0.0``
*********************************
<code>avg</code>
==============================
<code><b>avg(<i>&lt;value1&gt;</i> : number) => number</b></code><br/><br/>
열 값의 평균을 가져옵니다. * ``avg(sales) -> 7523420.234``
*********************************
<code>avgIf</code>
==============================
<code><b>avgIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => number</b></code><br/><br/>
조건에 따라 열 값의 평균을 가져옵니다. * ``avgIf(region == 'West', sales) -> 7523420.234``
*********************************
<code>case</code>
==============================
<code><b>case(<i>&lt;condition&gt;</i> : boolean, <i>&lt;true_expression&gt;</i> : any, <i>&lt;false_expression&gt;</i> : any, ...) => any</b></code><br/><br/>
교대로 나오는 조건에 따라 하나의 값 또는 다른 값이 적용됩니다. 입력 수가 짝수이면 마지막 조건에서 다른 값은 NULL입니다. * ``case(custType == 'Premium', 10, 4.5)``
* ``case(custType == 'Premium', price*0.95, custType == 'Elite',   price*0.9, price*2)``
* ``case(dayOfWeek(saleDate) == 1, 'Sunday', dayOfWeek(saleDate) == 6, 'Saturday')``
*********************************
<code>cbrt</code>
==============================
<code><b>cbrt(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
숫자의 세제곱근을 계산합니다. * ``cbrt(8) -> 2.0``
*********************************
<code>ceil</code>
==============================
<code><b>ceil(<i>&lt;value1&gt;</i> : number) => number</b></code><br/><br/>
해당 수보다 작지 않은 가장 작은 정수를 반환합니다. * ``ceil(-0.1) -> 0``
*********************************
<code>concat</code>
==============================
<code><b>concat(<i>&lt;this&gt;</i> : string, <i>&lt;that&gt;</i> : string, ...) => string</b></code><br/><br/>
가변 개수의 문자열을 함께 연결합니다. 문자열이 있는 + 연산자와 같습니다. * ``concat('Awesome', 'Cool', 'Product') -> 'AwesomeCoolProduct'``
* ``'Awesome' + 'Cool' + 'Product' -> 'AwesomeCoolProduct'``
* ``concat(addrLine1, ' ', addrLine2, ' ', city, ' ', state, ' ', zip)``
* ``addrLine1 + ' ' + addrLine2 + ' ' + city + ' ' + state + ' ' + zip``
*********************************
<code>concatWS</code>
==============================
<code><b>concatWS(<i>&lt;separator&gt;</i> : string, <i>&lt;this&gt;</i> : string, <i>&lt;that&gt;</i> : string, ...) => string</b></code><br/><br/>
가변 개수의 문자열을 구분 기호와 함께 연결합니다. 첫 번째 매개 변수는 구분 기호입니다. * ``concatWS(' ', 'Awesome', 'Cool', 'Product') -> 'Awesome Cool Product'``
* ``concatWS(' ' , addrLine1, addrLine2, city, state, zip) -> ``
* ``concatWS(',' , toString(order_total), toString(order_discount))``
*********************************
<code>cos</code>
==============================
<code><b>cos(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
코사인 값을 계산합니다. * ``cos(10) -> -0.83907152907``
*********************************
<code>cosh</code>
==============================
<code><b>cosh(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
값의 쌍곡선 코사인을 계산합니다. * ``cosh(0) -> 1.0``
*********************************
<code>count</code>
==============================
<code><b>count([<i>&lt;value1&gt;</i> : any]) => long</b></code><br/><br/>
값의 집계 개수를 가져옵니다. 선택적 열을 지정하면 개수에서 NULL 값을 무시합니다. * ``count(custId) -> 100``
* ``count(custId, custName) -> 50``
* ``count() -> 125``
* ``count(iif(isNull(custId), 1, NULL)) -> 5``
*********************************
<code>countDistinct</code>
==============================
<code><b>countDistinct(<i>&lt;value1&gt;</i> : any, [<i>&lt;value2&gt;</i> : any], ...) => long</b></code><br/><br/>
열 세트의 고유 값에 대한 집계 합계를 가져옵니다. * ``countDistinct(custId, custName) -> 60``
*********************************
<code>countIf</code>
==============================
<code><b>countIf(<i>&lt;value1&gt;</i> : boolean, [<i>&lt;value2&gt;</i> : any]) => long</b></code><br/><br/>
조건에 따라 값의 집계 개수를 가져옵니다. 선택적 열을 지정하면 개수에서 NULL 값을 무시합니다. * ``countIf(state == 'CA' && commission < 10000, name) -> 100``
*********************************
<code>covariancePopulation</code>
==============================
<code><b>covariancePopulation(<i>&lt;value1&gt;</i> : number, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
두 열 간의 모집단 공변성(covariance)을 가져옵니다. * ``covariancePopulation(sales, profit) -> 122.12``
*********************************
<code>covariancePopulationIf</code>
==============================
<code><b>covariancePopulationIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number, <i>&lt;value3&gt;</i> : number) => double</b></code><br/><br/>
조건에 따라 두 열의 모집단 공변성(covariance)을 가져옵니다. * ``covariancePopulationIf(region == 'West', sales) -> 122.12``
*********************************
<code>covarianceSample</code>
==============================
<code><b>covarianceSample(<i>&lt;value1&gt;</i> : number, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
두 열의 샘플 공변성(covariance)을 가져옵니다. * ``covarianceSample(sales, profit) -> 122.12``
*********************************
<code>covarianceSampleIf</code>
==============================
<code><b>covarianceSampleIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number, <i>&lt;value3&gt;</i> : number) => double</b></code><br/><br/>
조건에 따라 두 열의 샘플 공변성(covariance)을 가져옵니다. * ``covarianceSampleIf(region == 'West', sales, profit) -> 122.12``
*********************************
<code>crc32</code>
==============================
<code><b>crc32(<i>&lt;value1&gt;</i> : any, ...) => long</b></code><br/><br/>
0(256), 224, 256, 384, 512 값의 지정된 비트 길이를 갖는 다양한 기본 데이터 형식의 열 세트에서 CRC32 해시를 계산합니다. 행의 지문을 계산하는 데 사용할 수 있습니다. * ``crc32(256, 'gunchus', 8.2, 'bojjus', true, toDate('2010-4-4')) -> 3630253689``
*********************************
<code>cumeDist</code>
==============================
<code><b>cumeDist() => integer</b></code><br/><br/>
CumeDist 함수는 파티션의 모든 값을 기준으로 값의 위치를 계산합니다. 결과는 파티션 순서에서 현재 행보다 앞에 있거나 같은 위치에 있는 행 수를 창 파티션의 총 행 수로 나눈 값입니다. 동률 값 순서에서 같은 위치로 계산 됩니다.
* ``cumeDist() -> 1``
*********************************
<code>currentDate</code>
==============================
<code><b>currentDate([<i>&lt;value1&gt;</i> : string]) => date</b></code><br/><br/>
이 작업 실행이 시작되는 현재 날짜를 가져옵니다. 'GMT', 'PST', 'UTC', 'America/Cayman' 형태로 선택적 표준 시간대를 제공할 수 있습니다. 현지 표준 시간대가 기본적으로 사용됩니다.
* ``currentDate() -> 12-12-2030``
* ``currentDate('PST') -> 12-31-2050``
*********************************
<code>currentTimestamp</code>
==============================
<code><b>currentTimestamp() => timestamp</b></code><br/><br/>
현지 표준 시간대를 사용하여 작업 실행을 시작하는 현재 타임스탬프를 가져옵니다. * ``currentTimestamp() -> 12-12-2030T12:12:12``
*********************************
<code>currentUTC</code>
==============================
<code><b>currentUTC([<i>&lt;value1&gt;</i> : string]) => timestamp</b></code><br/><br/>
현재 타임스탬프를 UTC로 가져옵니다. 'GMT', 'PST', 'UTC', 'America/Cayman' 형태로 선택적 표준 시간대를 제공할 수 있습니다. 기본적으로 현재 표준 시간대가 사용됩니다. * ``currentUTC() -> 12-12-2030T19:18:12``
* ``currentUTC('Asia/Seoul') -> 12-13-2030T11:18:12``
*********************************
<code>dayOfMonth</code>
==============================
<code><b>dayOfMonth(<i>&lt;value1&gt;</i> : datetime) => integer</b></code><br/><br/>
지정된 날짜의 월중 일을 가져옵니다. * ``dayOfMonth(toDate('2018-06-08')) -> 08``
*********************************
<code>dayOfWeek</code>
==============================
<code><b>dayOfWeek(<i>&lt;value1&gt;</i> : datetime) => integer</b></code><br/><br/>
지정된 날짜의 요일을 가져옵니다. 1 - 일요일, 2 - 월요일 ..., 7 - 토요일 * ``dayOfWeek(toDate('2018-06-08')) -> 7``
*********************************
<code>dayOfYear</code>
==============================
<code><b>dayOfYear(<i>&lt;value1&gt;</i> : datetime) => integer</b></code><br/><br/>
지정된 날짜의 연중 일을 가져옵니다. * ``dayOfYear(toDate('2016-04-09')) -> 100``
*********************************
<code>degrees</code>
==============================
<code><b>degrees(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
라디안을 도로 변환합니다. * ``degrees(3.141592653589793) -> 180``
*********************************
<code>denseRank</code>
==============================
<code><b>denseRank(<i>&lt;value1&gt;</i> : any, ...) => integer</b></code><br/><br/>
값 그룹에 있는 값의 순위를 계산합니다. 결과는 파티션 순서에서 현재 행보다 앞에 있거나 같은 위치에 있는 행의 수에 1을 더한 것입니다. 값은 시퀀스에 간격을 생성하지 않습니다. 데이터가 정렬되지 않을 때도 Dense Rank가 작동하고 값 변경을 확인합니다. * ``denseRank(salesQtr, salesAmt) -> 1``
*********************************
<code>divide</code>
==============================
<code><b>divide(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => any</b></code><br/><br/>
숫자 쌍을 나눕니다. / 연산자와 같습니다. * ``divide(20, 10) -> 2``
* ``20 / 10 -> 2``
*********************************
<code>endsWith</code>
==============================
<code><b>endsWith(<i>&lt;string&gt;</i> : string, <i>&lt;substring to check&gt;</i> : string) => boolean</b></code><br/><br/>
문자열이 제공된 문자열로 끝나는지 확인합니다. * ``endsWith('great', 'eat') -> true``
*********************************
<code>equals</code>
==============================
<code><b>equals(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => boolean</b></code><br/><br/>
비교 같음 연산자. == 연산자와 같습니다. * ``equals(12, 24) -> false``
* ``12==24 -> false``
* ``'abc'=='abc' -> true``
*********************************
<code>equalsIgnoreCase</code>
==============================
<code><b>equalsIgnoreCase(<i>&lt;value1&gt;</i> : string, <i>&lt;value2&gt;</i> : string) => boolean</b></code><br/><br/>
비교는 대/소문자를 무시하는 연산자와 같습니다. <=> 연산자와 같습니다. * ``'abc'=='abc' -> true``
* ``equalsIgnoreCase('abc', 'Abc') -> true``
*********************************
<code>factorial</code>
==============================
<code><b>factorial(<i>&lt;value1&gt;</i> : number) => long</b></code><br/><br/>
숫자의 계승값을 계산합니다. * ``factorial(5) -> 120``
*********************************
<code>false</code>
==============================
<code><b>false() => boolean</b></code><br/><br/>
항상 false 값을 반환합니다. 'false'라는 열이 있는 경우 함수 syntax(false())를 사용합니다. * ``isDiscounted == false()``
* ``isDiscounted() == false``
*********************************
<code>first</code>
==============================
<code><b>first(<i>&lt;value1&gt;</i> : any, [<i>&lt;value2&gt;</i> : boolean]) => any</b></code><br/><br/>
열 그룹의 첫 번째 값을 가져옵니다. 두 번째 매개 변수 ignoreNulls를 생략하면 false로 간주됩니다. * ``first(sales) -> 12233.23``
* ``first(sales, false) -> NULL``
*********************************
<code>floor</code>
==============================
<code><b>floor(<i>&lt;value1&gt;</i> : number) => number</b></code><br/><br/>
해당 수보다 크지 않은 가장 큰 정수를 반환합니다. * ``floor(-0.1) -> -1``
*********************************
<code>greater</code>
==============================
<code><b>greater(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => boolean</b></code><br/><br/>
비교 보다 큼 연산자. > 연산자와 같습니다. * ``greater(12, 24) -> false``
* ``'abcd' > 'abc' -> true``
*********************************
<code>greaterOrEqual</code>
==============================
<code><b>greaterOrEqual(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => boolean</b></code><br/><br/>
비교 보다 크거나 같음 연산자. >= 연산자와 같습니다. * ``greaterOrEqual(12, 12) -> false``
* ``'abcd' >= 'abc' -> true``
*********************************
<code>greatest</code>
==============================
<code><b>greatest(<i>&lt;value1&gt;</i> : any, ...) => any</b></code><br/><br/>
값 목록 중에서 가장 큰 값을 입력으로 반환합니다. 모든 입력이 null이면 null을 반환합니다. * ``greatest(10, 30, 15, 20) -> 30``
* ``greatest(toDate('12/12/2010'), toDate('12/12/2011'), toDate('12/12/2000')) -> '12/12/2011'``
*********************************
<code>hour</code>
==============================
<code><b>hour(<i>&lt;value1&gt;</i> : timestamp, [<i>&lt;value2&gt;</i> : string]) => integer</b></code><br/><br/>
타임스탬프의 시간 값을 가져옵니다. 'GMT', 'PST', 'UTC', 'America/Cayman' 형태로 선택적 표준 시간대를 제공할 수 있습니다. 현지 표준 시간대가 기본적으로 사용됩니다.
* ``hour(toTimestamp('2009-07-30T12:58:59')) -> 12``
* ``hour(toTimestamp('2009-07-30T12:58:59'), 'PST') -> 12``
*********************************
<code>iif</code>
==============================
<code><b>iif(<i>&lt;condition&gt;</i> : boolean, <i>&lt;true_expression&gt;</i> : any, [<i>&lt;false_expression&gt;</i> : any]) => any</b></code><br/><br/>
조건에 따라 하나의 값 또는 다른 값이 적용됩니다. 지정 된 다른 없으면 NULL을 간주 됩니다. 두 값은 호환되어야 합니다(숫자, 문자열 등). * ``iif(custType == 'Premium', 10, 4.5)``
* ``iif(amount > 100, 'High')``
* ``iif(dayOfWeek(saleDate) == 6, 'Weekend', 'Weekday')``
*********************************
<code>in</code>
==============================
<code><b>in(<i>&lt;array of items&gt;</i> : array, <i>&lt;item to find&gt;</i> : any) => boolean</b></code><br/><br/>
항목이 배열에 있는지 확인합니다. * ``in([10, 20, 30], 10) -> true``
* ``in(['good', 'kid'], 'bad') -> false``
*********************************
<code>initCap</code>
==============================
<code><b>initCap(<i>&lt;value1&gt;</i> : string) => string</b></code><br/><br/>
모든 단어의 첫 글자를 대문자로 변환합니다. 단어는 공백으로 구분하여 식별됩니다. * ``initCap('cool iceCREAM') -> 'Cool IceCREAM'``
*********************************
<code>instr</code>
==============================
<code><b>instr(<i>&lt;string&gt;</i> : string, <i>&lt;substring to find&gt;</i> : string) => integer</b></code><br/><br/>
문자열 내에서 부분 문자열의 위치(1부터 시작)를 찾습니다. 찾을 수 없으면 0을 반환합니다. * ``instr('great', 'eat') -> 3``
* ``instr('microsoft', 'o') -> 7``
* ``instr('good', 'bad') -> 0``
*********************************
<code>isDelete</code>
==============================
<code><b>isDelete([<i>&lt;value1&gt;</i> : integer]) => boolean</b></code><br/><br/>
행이 삭제용으로 표시되어 있는지 확인합니다. 둘 이상의 입력된 스트림을 수행 하는 변환에 대 한 스트림 인덱스 (1부터 시작)를 전달할 수 있습니다. 스트림 인덱스의 기본값은 1입니다. * ``isDelete() -> true``
* ``isDelete(1) -> false``
*********************************
<code>isError</code>
==============================
<code><b>isError([<i>&lt;value1&gt;</i> : integer]) => boolean</b></code><br/><br/>
행이 오류로 표시되는지 여부를 확인합니다. 둘 이상의 입력된 스트림을 수행 하는 변환에 대 한 스트림 인덱스 (1부터 시작)를 전달할 수 있습니다. 스트림 인덱스의 기본값은 1입니다. * ``isError() -> true``
* ``isError(1) -> false``
*********************************
<code>isIgnore</code>
==============================
<code><b>isIgnore([<i>&lt;value1&gt;</i> : integer]) => boolean</b></code><br/><br/>
행이 무시되도록 표시되는지 여부를 확인합니다. 둘 이상의 입력된 스트림을 수행 하는 변환에 대 한 스트림 인덱스 (1부터 시작)를 전달할 수 있습니다. 스트림 인덱스의 기본값은 1입니다. * ``isIgnore() -> true``
* ``isIgnore(1) -> false``
*********************************
<code>isInsert</code>
==============================
<code><b>isInsert([<i>&lt;value1&gt;</i> : integer]) => boolean</b></code><br/><br/>
행이 삽입용으로 표시되어 있는지 확인합니다. 둘 이상의 입력된 스트림을 수행 하는 변환에 대 한 스트림 인덱스 (1부터 시작)를 전달할 수 있습니다. 스트림 인덱스의 기본값은 1입니다. * ``isInsert() -> true``
* ``isInsert(1) -> false``
*********************************
<code>isMatch</code>
==============================
<code><b>isMatch([<i>&lt;value1&gt;</i> : integer]) => boolean</b></code><br/><br/>
조회 시 행이 일치하는지 여부를 확인합니다. 둘 이상의 입력된 스트림을 수행 하는 변환에 대 한 스트림 인덱스 (1부터 시작)를 전달할 수 있습니다. 스트림 인덱스의 기본값은 1입니다. * ``isMatch() -> true``
* ``isMatch(1) -> false``
*********************************
<code>isNull</code>
==============================
<code><b>isNull(<i>&lt;value1&gt;</i> : any) => boolean</b></code><br/><br/>
값이 NULL인지 확인합니다. * ``isNull(NULL()) -> true``
* ``isNull('') -> false'``
*********************************
<code>isUpdate</code>
==============================
<code><b>isUpdate([<i>&lt;value1&gt;</i> : integer]) => boolean</b></code><br/><br/>
행이 업데이트용으로 표시되어 있는지 확인합니다. 둘 이상의 입력된 스트림을 수행 하는 변환에 대 한 스트림 인덱스 (1부터 시작)를 전달할 수 있습니다. 스트림 인덱스의 기본값은 1입니다. * ``isUpdate() -> true``
* ``isUpdate(1) -> false``
*********************************
<code>kurtosis</code>
==============================
<code><b>kurtosis(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
열의 첨도를 가져옵니다. * ``kurtosis(sales) -> 122.12``
*********************************
<code>kurtosisIf</code>
==============================
<code><b>kurtosisIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
조건에 따라 열의 첨도 가져옵니다. * ``kurtosisIf(region == 'West', sales) -> 122.12``
*********************************
<code>lag</code>
==============================
<code><b>lag(<i>&lt;value&gt;</i> : any, [<i>&lt;number of rows to look before&gt;</i> : number], [<i>&lt;default value&gt;</i> : any]) => any</b></code><br/><br/>
현재 행보다 n개 행 전에 평가되는 첫 번째 매개 변수의 값을 가져옵니다. 두 번째 매개 변수를 거슬러 올라가야 행 개수 이며 기본값은 1입니다. 기본값을 지정하지 않은 경우, 행이 많지 않으면 null 값이 반환됩니다. * ``lag(amount, 2) -> 60``
* ``lag(amount, 2000, 100) -> 100``
*********************************
<code>last</code>
==============================
<code><b>last(<i>&lt;value1&gt;</i> : any, [<i>&lt;value2&gt;</i> : boolean]) => any</b></code><br/><br/>
열 그룹의 마지막 값을 가져옵니다. 두 번째 매개 변수 ignoreNulls를 생략하면 false로 간주됩니다. * ``last(sales) -> 523.12``
* ``last(sales, false) -> NULL``
*********************************
<code>lastDayOfMonth</code>
==============================
<code><b>lastDayOfMonth(<i>&lt;value1&gt;</i> : datetime) => date</b></code><br/><br/>
지정된 날짜의 월중 마지막 날짜를 가져옵니다. * ``lastDayOfMonth(toDate('2009-01-12')) -> 2009-01-31``
*********************************
<code>lead</code>
==============================
<code><b>lead(<i>&lt;value&gt;</i> : any, [<i>&lt;number of rows to look after&gt;</i> : number], [<i>&lt;default value&gt;</i> : any]) => any</b></code><br/><br/>
현재 행보다 n개 행 뒤에 평가되는 첫 번째 매개 변수의 값을 가져옵니다. 두 번째 매개 변수 기대 하는 행 수 이며 기본값은 1입니다. 기본값을 지정하지 않은 경우, 행이 많지 않으면 null 값이 반환됩니다. * ``lead(amount, 2) -> 60``
* ``lead(amount, 2000, 100) -> 100``
*********************************
<code>least</code>
==============================
<code><b>least(<i>&lt;value1&gt;</i> : any, ...) => any</b></code><br/><br/>
비교 보다 작거나 같음 연산자. <= 연산자와 같습니다. * ``least(10, 30, 15, 20) -> 10``
* ``least(toDate('12/12/2010'), toDate('12/12/2011'), toDate('12/12/2000')) -> '12/12/2000'``
*********************************
<code>left</code>
==============================
<code><b>left(<i>&lt;string to subset&gt;</i> : string, <i>&lt;number of characters&gt;</i> : integral) => string</b></code><br/><br/>
인덱스 1에서 시작하여 지정된 문자 수를 갖는 부분 문자열을 추출합니다. SUBSTRING(str, 1, n)과 같습니다. * ``left('bojjus', 2) -> 'bo'``
* ``left('bojjus', 20) -> 'bojjus'``
*********************************
<code>length</code>
==============================
<code><b>length(<i>&lt;value1&gt;</i> : string) => integer</b></code><br/><br/>
문자열의 길이를 반환합니다. * ``length('kiddo') -> 5``
*********************************
<code>lesser</code>
==============================
<code><b>lesser(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => boolean</b></code><br/><br/>
비교 보다 작음 연산자. < 연산자와 같습니다. * ``lesser(12 < 24) -> true``
* ``'abcd' < 'abc' -> false``
*********************************
<code>lesserOrEqual</code>
==============================
<code><b>lesserOrEqual(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => boolean</b></code><br/><br/>
비교 보다 작거나 같음 연산자. <= 연산자와 같습니다. * ``lesserOrEqual(12, 12) -> true``
* ``'abcd' <= 'abc' -> false``
*********************************
<code>levenshtein</code>
==============================
<code><b>levenshtein(<i>&lt;from string&gt;</i> : string, <i>&lt;to string&gt;</i> : string) => integer</b></code><br/><br/>
두 문자열 간의 levenshtein 거리를 가져옵니다. * ``levenshtein('boys', 'girls') -> 4``
*********************************
<code>like</code>
==============================
<code><b>like(<i>&lt;string&gt;</i> : string, <i>&lt;pattern match&gt;</i> : string) => boolean</b></code><br/><br/>
문자 그대로 일치 하는 문자열을 패턴으로 합니다. 예외는 다음 특수 기호: _ (유사 입력에 있는 한 문자 일치 합니다. .과 유사). %는 입력의 0개 이상의 문자와 일치합니다(posix 정규식의 .*와 유사).
이스케이프 문자는 ''입니다. 특수 기호 또는 다른 이스케이프 문자 앞에 이스케이프 문자가 오면 다음 문자는 글자 그대로 일치됩니다. 다른 모든 문자를 이스케이프하는 것은 유효하지 않습니다.
* ``like('icecream', 'ice%') -> true``
*********************************
<code>locate</code>
==============================
<code><b>locate(<i>&lt;substring to find&gt;</i> : string, <i>&lt;string&gt;</i> : string, [<i>&lt;from index - 1-based&gt;</i> : integral]) => integer</b></code><br/><br/>
특정 위치에서 시작하는 문자열 내에서 부분 문자열의 위치(1부터 시작)를 찾습니다. 이 위치를 생략하면 문자열의 시작 부분에서 찾습니다. 찾을 수 없으면 0을 반환합니다. * ``locate('eat', 'great') -> 3``
* ``locate('o', 'microsoft', 6) -> 7``
* ``locate('bad', 'good') -> 0``
*********************************
<code>log</code>
==============================
<code><b>log(<i>&lt;value1&gt;</i> : number, [<i>&lt;value2&gt;</i> : number]) => double</b></code><br/><br/>
로그 값을 계산합니다. 오일러 수 이외의 선택적인 밑을 제공할 수 있습니다(사용할 경우). * ``log(100, 10) -> 2``
*********************************
<code>log10</code>
==============================
<code><b>log10(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
밑이 10인 로그 값을 계산합니다. * ``log10(100) -> 2``
*********************************
<code>lower</code>
==============================
<code><b>lower(<i>&lt;value1&gt;</i> : string) => string</b></code><br/><br/>
문자열을 소문자로 바꿉니다. * ``lower('GunChus') -> 'gunchus'``
*********************************
<code>lpad</code>
==============================
<code><b>lpad(<i>&lt;string to pad&gt;</i> : string, <i>&lt;final padded length&gt;</i> : integral, <i>&lt;padding&gt;</i> : string) => string</b></code><br/><br/>
특정 길이가 될 때까지 제공된 패딩으로 문자열의 왼쪽 여백을 채웁니다. 문자열 길이 보다 크거나 같은 경우 작동 하지 않는 것으로 간주 됩니다 * ``lpad('great', 10, '-') -> '-----great'`` 
* ``lpad('great', 4, '-') -> 'great'`` 
* ' lpad ('훌륭한' 8 ' <>')-> ' <><great'``
*********************************
<code>ltrim</code>
==============================
<code><b>ltrim(<i>&lt;string to trim&gt;</i> : string, <i>&lt;trim characters&gt;</i> : string) => string</b></code><br/><br/>
왼쪽의 선행 문자열을 삭제합니다. 두 번째 매개 변수를 지정하지 않으면 공백을 삭제합니다. 그렇지 않은 경우 두 번째 매개 변수에 지정된 모든 문자를 삭제합니다. * ``ltrim('!--!wor!ld!', '-!') -> 'wor!ld!'``
*********************************
<code>max</code>
==============================
<code><b>max(<i>&lt;value1&gt;</i> : any) => any</b></code><br/><br/>
열의 최대값을 가져옵니다. * ``MAX(sales) -> 12312131.12``
*********************************
<code>maxIf</code>
==============================
<code><b>maxIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : any) => any</b></code><br/><br/>
조건에 따라 열의 최대값을 가져옵니다. * ``maxIf(region == 'West', sales) -> 99999.56``
*********************************
<code>md5</code>
==============================
<code><b>md5(<i>&lt;value1&gt;</i> : any, ...) => string</b></code><br/><br/>
다양한 기본 데이터 형식의 열 세트에서 MD5 다이제스트를 계산하고 32자의 16진수 문자열을 반환합니다. 행의 지문을 계산하는 데 사용할 수 있습니다. * ``md5(5, 'gunchus', 8.2, 'bojjus', true, toDate('2010-4-4')) -> 'c1527622a922c83665e49835e46350fe'``
*********************************
<code>mean</code>
==============================
<code><b>mean(<i>&lt;value1&gt;</i> : number) => number</b></code><br/><br/>
열 값의 평균값을 가져옵니다. AVG와 같습니다. * ``mean(sales) -> 7523420.234``
*********************************
<code>meanIf</code>
==============================
<code><b>meanIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => number</b></code><br/><br/>
조건에 따라 열 값의 평균값을 가져옵니다. avgIf와 같습니다. * ``meanIf(region == 'West', sales) -> 7523420.234``
*********************************
<code>min</code>
==============================
<code><b>min(<i>&lt;value1&gt;</i> : any) => any</b></code><br/><br/>
열의 최소값을 가져옵니다. * ``min(sales) -> 00.01``
* ``min(orderDate) -> 12/12/2000``
*********************************
<code>minIf</code>
==============================
<code><b>minIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : any) => any</b></code><br/><br/>
조건에 따라 열의 최소값을 가져옵니다. * ``minIf(region == 'West', sales) -> 00.01``
*********************************
<code>minus</code>
==============================
<code><b>minus(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => any</b></code><br/><br/>
숫자를 뺍니다. 날짜에서 일 수를 뺍니다. - 연산자와 같습니다. * ``minus(20, 10) -> 10``
* ``20 - 10 -> 10``
* ``minus(toDate('2012-12-15'), 3) -> 2012-12-12 (date value)``
* ``toDate('2012-12-15') - 3 -> 2012-12-13 (date value)``
*********************************
<code>minute</code>
==============================
<code><b>minute(<i>&lt;value1&gt;</i> : timestamp, [<i>&lt;value2&gt;</i> : string]) => integer</b></code><br/><br/>
타임스탬프의 분 값을 가져옵니다. 'GMT', 'PST', 'UTC', 'America/Cayman' 형태로 선택적 표준 시간대를 제공할 수 있습니다. 현지 표준 시간대가 기본적으로 사용됩니다.
* ``minute(toTimestamp('2009-07-30T12:58:59')) -> 58``
* ``minute(toTimestamp('2009-07-30T12:58:59', 'PST')) -> 58``
*********************************
<code>mod</code>
==============================
<code><b>mod(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => any</b></code><br/><br/>
숫자 쌍의 모듈러스입니다. % 연산자와 같습니다. * ``mod(20, 8) -> 4``
* ``20 % 8 -> 4``
*********************************
<code>month</code>
==============================
<code><b>month(<i>&lt;value1&gt;</i> : datetime) => integer</b></code><br/><br/>
날짜 또는 타임스탬프의 월 값을 가져옵니다. * ``month(toDate('2012-8-8')) -> 8``
*********************************
<code>monthsBetween</code>
==============================
<code><b>monthsBetween(<i>&lt;from date/timestamp&gt;</i> : datetime, <i>&lt;to date/timestamp&gt;</i> : datetime, [<i>&lt;time zone&gt;</i> : boolean], [<i>&lt;value4&gt;</i> : string]) => double</b></code><br/><br/>
가져옵니다 두 datesYou 사이의 개월 수 'GMT', '태평양 표준시', 'UTC', ' America/케이맨 ' 형태로 선택적 표준 시간대를 전달할 수 있습니다. 현지 표준 시간대가 기본적으로 사용됩니다.
* ``monthsBetween(toDate('1997-02-28 10:30:00'), toDate('1996-10-30')) -> 3.94959677``
*********************************
<code>multiply</code>
==============================
<code><b>multiply(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => any</b></code><br/><br/>
숫자 쌍을 곱합니다. * 연산자와 같습니다. * ``multiply(20, 10) -> 200``
* ``20 * 10 -> 200``
*********************************
<code>nTile</code>
==============================
<code><b>nTile([<i>&lt;value1&gt;</i> : integer]) => integer</b></code><br/><br/>
NTile 함수는 각 창 파티션의 행을 1부터 `n`개 이내의 `n` 버킷 수로 나눕니다. 버킷 값 차이는 최대 1 이내입니다. 파티션의 행 수가 버킷 수로 균일하게 나누어 떨어지지 않으면 나머지 값은 첫 번째 버킷부터 시작해서 하나씩 분산됩니다. NTile 함수 tertiles, 변 위치, 10 분 위 수, 및 기타 일반적인 요약 통계 계산에 특히 유용합니다. 이 함수는 초기화하는 동안 두 개의 변수를 계산합니다. 일반 버킷의 크기를 하나 추가 행을 추가 해야 합니다. 두 변수는 현재 파티션의 크기를 기반으로 합니다. 계산 프로세스 동안 이 함수는 현재 행 번호, 현재 버킷 수 및 버킷이 변경되는 행 번호(bucketThreshold)를 추적합니다. 현재 행 번호가 버킷 임계값에 도달하면 버킷 값이 1씩 커지고, 임계값은 버킷 크기만큼 커집니다(현재 버킷이 채워질 경우 하나씩 추가).
* ``nTile() -> 1``
* ``nTile(numOfBuckets) -> 1``
*********************************
<code>negate</code>
==============================
<code><b>negate(<i>&lt;value1&gt;</i> : number) => number</b></code><br/><br/>
숫자를 부정합니다. 양수를 음수로, 음수를 양수로 변환합니다. * ``negate(13) -> -13``
*********************************
<code>nextSequence</code>
==============================
<code><b>nextSequence() => long</b></code><br/><br/>
고유한 다음 시퀀스를 반환합니다. 이 수는 파티션 내에서만 연속되며 앞에 partitionId가 붙습니다. * ``nextSequence() -> 12313112``
*********************************
<code>not</code>
==============================
<code><b>not(<i>&lt;value1&gt;</i> : boolean) => boolean</b></code><br/><br/>
논리 부정 연산자 * ``not(true) -> false``
* ``not(premium)``
*********************************
<code>notEquals</code>
==============================
<code><b>notEquals(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => boolean</b></code><br/><br/>
비교 같지 않음 연산자. != 연산자와 같습니다. * ``12!=24 -> true``
* ``'abc'!='abc' -> false``
*********************************
<code>null</code>
==============================
<code><b>null() => null</b></code><br/><br/>
NULL 값을 반환합니다. 'Null' 명명 된 열 이름이 없으면 함수 syntax(null())를 사용 합니다. 사용하는 모든 작업은 결과적으로 NULL이 됩니다. * ``custId = NULL (for derived field)``
* ``custId == NULL -> NULL``
* ``'nothing' + NULL -> NULL``
* ``10 * NULL -> NULL'``
* ``NULL == '' -> NULL'``
*********************************
<code>or</code>
==============================
<code><b>or(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : boolean) => boolean</b></code><br/><br/>
논리 OR 연산자입니다. ||과 같습니다. * ``or(true, false) -> true``
* ``true || false -> true``
*********************************
<code>pMod</code>
==============================
<code><b>pMod(<i>&lt;value1&gt;</i> : any, <i>&lt;value2&gt;</i> : any) => any</b></code><br/><br/>
숫자 쌍의 양의 모듈러스입니다.
* ``pmod(-20, 8) -> 4``
*********************************
<code>power</code>
==============================
<code><b>power(<i>&lt;value1&gt;</i> : number, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
한 수를 다른 수의 승수로 거듭제곱합니다. * ``power(10, 2) -> 100``
*********************************
<code>rank</code>
==============================
<code><b>rank(<i>&lt;value1&gt;</i> : any, ...) => integer</b></code><br/><br/>
값 그룹에 있는 값의 순위를 계산합니다. 결과는 파티션 순서에서 현재 행보다 앞에 있거나 같은 위치에 있는 행의 수에 1을 더한 것입니다. 값은 시퀀스에 간격을 생성합니다. 데이터가 정렬되지 않을 때도 Rank가 작동하고 값 변경을 확인합니다. * ``rank(salesQtr, salesAmt) -> 1``
*********************************
<code>regexExtract</code>
==============================
<code><b>regexExtract(<i>&lt;string&gt;</i> : string, <i>&lt;regex to find&gt;</i> : string, [<i>&lt;match group 1-based index&gt;</i> : integral]) => string</b></code><br/><br/>
지정된 정규식 패턴에 대해 일치하는 부분 문자열을 추출합니다. 마지막 매개 변수는 일치 그룹을 식별하고 생략하면 기본적으로 1이 지정됩니다. 이스케이프 없이 문자열을 일치시키려면 `<regex>'(따옴표)를 사용합니다. * ``regexExtract('Cost is between 600 and 800 dollars', '(\\d+) and (\\d+)', 2) -> '800'``
* ``regexExtract('Cost is between 600 and 800 dollars', `(\d+) and (\d+)`, 2) -> '800'``
*********************************
<code>regexMatch</code>
==============================
<code><b>regexMatch(<i>&lt;string&gt;</i> : string, <i>&lt;regex to match&gt;</i> : string) => boolean</b></code><br/><br/>
문자열이 지정된 정규식 패턴과 일치하는지 확인합니다. 이스케이프 없이 문자열을 일치시키려면 `<regex>'(따옴표)를 사용합니다. * ``regexMatch('200.50', '(\\d+).(\\d+)') -> true``
* ``regexMatch('200.50', `(\d+).(\d+)`) -> true``
*********************************
<code>regexReplace</code>
==============================
<code><b>regexReplace(<i>&lt;string&gt;</i> : string, <i>&lt;regex to find&gt;</i> : string, <i>&lt;substring to replace&gt;</i> : string) => string</b></code><br/><br/>
한 정규식 패턴이 나오는 모든 경오를 지정된 문자열의 다른 부분 문자열로 바꿉니다. 이스케이프 없이 문자열을 일치시키려면 `<regex>`(따옴표)를 사용합니다. * ``regexReplace('100 and 200', '(\\d+)', 'bojjus') -> 'bojjus and bojjus'``
* ``regexReplace('100 and 200', `(\d+)`, 'gunchus') -> 'gunchus and gunchus'``
*********************************
<code>regexSplit</code>
==============================
<code><b>regexSplit(<i>&lt;string to split&gt;</i> : string, <i>&lt;regex expression&gt;</i> : string) => array</b></code><br/><br/>
정규식을 기준으로 구분 기호에 따라 문자열을 분할하고 문자열의 배열을 반환합니다. * ``regexSplit('oneAtwoBthreeC', '[CAB]') -> ['one', 'two', 'three']``
* ``regexSplit('oneAtwoBthreeC', '[CAB]')[1] -> 'one'``
* ``regexSplit('oneAtwoBthreeC', '[CAB]')[0] -> NULL``
* ``regexSplit('oneAtwoBthreeC', '[CAB]')[20] -> NULL``
*********************************
<code>replace</code>
==============================
<code><b>replace(<i>&lt;string&gt;</i> : string, <i>&lt;substring to find&gt;</i> : string, <i>&lt;substring to replace&gt;</i> : string) => string</b></code><br/><br/>
한 부분 문자열이 나오는 모든 경우를 지정된 문자열의 다른 부분 문자열로 바꿉니다. * ``replace('doggie dog', 'dog', 'cat') -> 'catgie cat'``
* ``replace('doggie dog', 'dog', '') -> 'gie'``
*********************************
<code>reverse</code>
==============================
<code><b>reverse(<i>&lt;value1&gt;</i> : string) => string</b></code><br/><br/>
문자열을 반대로 바꿉니다. * ``reverse('gunchus') -> 'suhcnug'``
*********************************
<code>right</code>
==============================
<code><b>right(<i>&lt;string to subset&gt;</i> : string, <i>&lt;number of characters&gt;</i> : integral) => string</b></code><br/><br/>
오른쪽부터 지정된 문자 수를 갖는 부분 문자열을 추출합니다. SUBSTRING(str, LENGTH(str) - n, n)과 같습니다. * ``right('bojjus', 2) -> 'us'``
* ``right('bojjus', 20) -> 'bojjus'``
*********************************
<code>rlike</code>
==============================
<code><b>rlike(<i>&lt;string&gt;</i> : string, <i>&lt;pattern match&gt;</i> : string) => boolean</b></code><br/><br/>
문자열이 지정된 정규식 패턴과 일치하는지 확인합니다. * ``rlike('200.50', '(\d+).(\d+)') -> true``
*********************************
<code>round</code>
==============================
<code><b>round(<i>&lt;number&gt;</i> : number, [<i>&lt;scale to round&gt;</i> : number], [<i>&lt;rounding option&gt;</i> : integral]) => double</b></code><br/><br/>
선택적 확장을 및 선택적 반올림 모드를 지정 된 숫자를 반올림 합니다. 소수 자릿수를 생략 하면 0으로 기본값으로 설정 됩니다.  반올림 모드를 생략하면 기본적으로 ROUND_HALF_UP(5)이 사용됩니다. 반올림 값에는 1 - ROUND_UP 2 - ROUND_DOWN 3 - ROUND_CEILING 4 - ROUND_FLOOR 5 - ROUND_HALF_UP 6 - ROUND_HALF_DOWN 7 - ROUND_HALF_EVEN 8 - ROUND_UNNECESSARY가 포함됩니다. * ``round(100.123) -> 100.0``
* ``round(2.5, 0) -> 3.0``
* ``round(5.3999999999999995, 2, 7) -> 5.40``
*********************************
<code>rowNumber</code>
==============================
<code><b>rowNumber() => integer</b></code><br/><br/>
1부터 시작 하는 창에서 행에 대 한 번호 매기기 순차 행 할당 * ``rowNumber() -> 1``
*********************************
<code>rpad</code>
==============================
<code><b>rpad(<i>&lt;string to pad&gt;</i> : string, <i>&lt;final padded length&gt;</i> : integral, <i>&lt;padding&gt;</i> : string) => string</b></code><br/><br/>
특정 길이가 될 때까지 제공된 패딩으로 문자열의 오른쪽 여백을 채웁니다. 문자열 길이 보다 크거나 같은 경우 작동 하지 않는 것으로 간주 됩니다 * ``rpad('great', 10, '-') -> 'great-----'`` 
* ``rpad('great', 4, '-') -> 'great'`` 
* ``rpad('great', 8, '<>') -> 'great<><'`` 
*********************************
<code>rtrim</code>rtrim</code>
==============================
<code><b>rtrim(<i>&lt;string to trim&gt;</i> : string, <i>&lt;trim characters&gt;</i> : string) => string</b></code><br/><br/>
오른쪽의 선행 문자열을 삭제합니다. 두 번째 매개 변수를 지정하지 않으면 공백을 삭제합니다. 그렇지 않은 경우 두 번째 매개 변수에 지정된 모든 문자를 삭제합니다. * ``rtrim('!--!wor!ld!', '-!') -> '!--!wor!ld'``
*********************************
<code>second</code>
==============================
<code><b>second(<i>&lt;value1&gt;</i> : timestamp, [<i>&lt;value2&gt;</i> : string]) => integer</b></code><br/><br/>
날짜의 초 값을 가져옵니다. 'GMT', 'PST', 'UTC', 'America/Cayman' 형태로 선택적 표준 시간대를 제공할 수 있습니다. 현지 표준 시간대가 기본적으로 사용됩니다.
* ``second(toTimestamp('2009-07-30T12:58:59')) -> 59``
*********************************
<code>sha1</code>
==============================
<code><b>sha1(<i>&lt;value1&gt;</i> : any, ...) => string</b></code><br/><br/>
다양한 기본 데이터 형식의 열 세트에서 SHA-1 다이제스트를 계산하고 40자의 16진수 문자열을 반환합니다. 행의 지문을 계산하는 데 사용할 수 있습니다. * ``sha1(5, 'gunchus', 8.2, 'bojjus', true, toDate('2010-4-4')) -> '63849fd2abb65fbc626c60b1f827bd05573f0cea'``
*********************************
<code>sha2</code>
==============================
<code><b>sha2(<i>&lt;value1&gt;</i> : integer, <i>&lt;value2&gt;</i> : any, ...) => string</b></code><br/><br/>
계산 열 값 0(256)의 수만 있는 비트 길이 지정 하는 기본 데이터 형식이 다양 한 집합의 sha-2 다이제스트 224, 256, 384 512입니다. 행의 지문을 계산하는 데 사용할 수 있습니다. * ``sha2(256, 'gunchus', 8.2, 'bojjus', true, toDate('2010-4-4')) -> 'd3b2bff62c3a00e9370b1ac85e428e661a7df73959fa1a96ae136599e9ee20fd'``
*********************************
<code>sin</code>
==============================
<code><b>sin(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
사인 값을 계산합니다. * ``sin(2) -> 0.90929742682``
*********************************
<code>sinh</code>
==============================
<code><b>sinh(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
쌍곡선 사인 값을 계산합니다. * ``sinh(0) -> 0.0``
*********************************
<code>skewness</code>
==============================
<code><b>skewness(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
열의 왜곡도를 가져옵니다. * ``skewness(sales) -> 122.12``
*********************************
<code>skewnessIf</code>
==============================
<code><b>skewnessIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
조건에 따라 열의 왜곡도 가져옵니다. * ``skewnessIf(region == 'West', sales) -> 122.12``
*********************************
<code>slice</code>
==============================
<code><b>slice(<i>&lt;array to slice&gt;</i> : array, <i>&lt;from 1-based index&gt;</i> : integral, [<i>&lt;number of items&gt;</i> : integral]) => array</b></code><br/><br/>
특정 위치에서 배열의 하위 세트를 추출합니다. 위치는 1부터 시작합니다. 길이를 생략하면 기본적으로 문자열 끝까지입니다. * ``slice([10, 20, 30, 40], 1, 2) -> [10, 20]``
* ``slice([10, 20, 30, 40], 2) -> [20, 30, 40]``
* ``slice([10, 20, 30, 40], 2)[1] -> 20``
* ``slice([10, 20, 30, 40], 2)[0] -> NULL``
* ``slice([10, 20, 30, 40], 2)[20] -> NULL``
* ``slice([10, 20, 30, 40], 8) -> []``
*********************************
<code>soundex</code>
==============================
<code><b>soundex(<i>&lt;value1&gt;</i> : string) => string</b></code><br/><br/>
문자열의 soundex 코드를 가져옵니다. * ``soundex('genius') -> 'G520'``
*********************************
<code>split</code>
==============================
<code><b>split(<i>&lt;string to split&gt;</i> : string, <i>&lt;split characters&gt;</i> : string) => array</b></code><br/><br/>
구분 기호를 기준으로 문자열을 분할하고 문자열의 배열을 반환합니다. * ``split('100,200,300', ',') -> ['100', '200', '300']``
* ``split('100,200,300', '|') -> ['100,200,300']``
* ``split('100, 200, 300', ', ') -> ['100', '200', '300']``
* ``split('100, 200, 300', ', ')[1] -> '100'``
* ``split('100, 200, 300', ', ')[0] -> NULL``
* ``split('100, 200, 300', ', ')[20] -> NULL``
* ``split('100200300', ',') -> ['100200300']``
*********************************
<code>sqrt</code>
==============================
<code><b>sqrt(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
숫자의 제곱근을 계산합니다. * ``sqrt(9) -> 3``
*********************************
<code>startsWith</code>
==============================
<code><b>startsWith(<i>&lt;string&gt;</i> : string, <i>&lt;substring to check&gt;</i> : string) => boolean</b></code><br/><br/>
문자열이 제공된 문자열로 시작하는지 확인합니다. * ``startsWith('great', 'gr') -> true``
*********************************
<code>stddev</code>
==============================
<code><b>stddev(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
열의 표준 편차를 가져옵니다. * ``stdDev(sales) -> 122.12``
*********************************
<code>stddevIf</code>
==============================
<code><b>stddevIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
조건에 따라 열의 표준 편차를 가져옵니다. * ``stddevIf(region == 'West', sales) -> 122.12``
*********************************
<code>stddevPopulation</code>
==============================
<code><b>stddevPopulation(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
열의 모집단 표준 편차를 가져옵니다. * ``stddevPopulation(sales) -> 122.12``
*********************************
<code>stddevPopulationIf</code>
==============================
<code><b>stddevPopulationIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
조건에 따라 열의 모집단 표준 편차를 가져옵니다. * ``stddevPopulationIf(region == 'West', sales) -> 122.12``
*********************************
<code>stddevSample</code>
==============================
<code><b>stddevSample(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
열의 샘플 표준 편차를 가져옵니다. * ``stddevSample(sales) -> 122.12``
*********************************
<code>stddevSampleIf</code>
==============================
<code><b>stddevSampleIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
조건에 따라 열의 샘플 표준 편차를 가져옵니다. * ``stddevSampleIf(region == 'West', sales) -> 122.12``
*********************************
<code>subDays</code>
==============================
<code><b>subDays(<i>&lt;date/timestamp&gt;</i> : datetime, <i>&lt;days to subtract&gt;</i> : integral) => datetime</b></code><br/><br/>
날짜에서 월을 뺍니다. 날짜에 대한 - 연산자와 같습니다. * ``subDays(toDate('2016-08-08'), 1) -> 2016-08-09``
*********************************
<code>subMonths</code>
==============================
<code><b>subMonths(<i>&lt;date/timestamp&gt;</i> : datetime, <i>&lt;months to subtract&gt;</i> : integral) => datetime</b></code><br/><br/>
날짜 또는 타임스탬프에서 월을 뺍니다. * ``subMonths(toDate('2016-09-30'), 1) -> 2016-08-31``
*********************************
<code>substring</code>
==============================
<code><b>substring(<i>&lt;string to subset&gt;</i> : string, <i>&lt;from 1-based index&gt;</i> : integral, [<i>&lt;number of characters&gt;</i> : integral]) => string</b></code><br/><br/>
특정 위치에서 특정 길이의 부분 문자열을 추출합니다. 위치는 1부터 시작합니다. 길이를 생략하면 기본적으로 문자열 끝까지입니다. * ``substring('Cat in the hat', 5, 2) -> 'in'``
* ``substring('Cat in the hat', 5, 100) -> 'in the hat'``
* ``substring('Cat in the hat', 5) -> 'in the hat'``
* ``substring('Cat in the hat', 100, 100) -> ''``
*********************************
<code>sum</code>
==============================
<code><b>sum(<i>&lt;value1&gt;</i> : number) => number</b></code><br/><br/>
숫자 열의 집계 합계를 가져옵니다. * ``sum(col) -> value``
*********************************
<code>sumDistinct</code>
==============================
<code><b>sumDistinct(<i>&lt;value1&gt;</i> : number) => number</b></code><br/><br/>
숫자 열의 고유 값에 대한 집계 합계를 가져옵니다. * ``sumDistinct(col) -> value``
*********************************
<code>sumDistinctIf</code>
==============================
<code><b>sumDistinctIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => number</b></code><br/><br/>
기준에 따라 숫자 열의 집계 합계를 가져옵니다. 조건의 기준은 어떤 열도 될 수 있습니다. * ``sumDistinctIf(state == 'CA' && commission < 10000, sales) -> value``
* ``sumDistinctIf(true, sales) -> SUM(sales) ``
*********************************
<code>sumIf</code>
==============================
<code><b>sumIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => number</b></code><br/><br/>
기준에 따라 숫자 열의 집계 합계를 가져옵니다. 조건의 기준은 어떤 열도 될 수 있습니다. * ``sumIf(state == 'CA' && commission < 10000, sales) -> value``
* ``sumIf(true, sales) -> SUM(sales) ``
*********************************
<code>tan</code>
==============================
<code><b>tan(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
탄젠트 값을 계산합니다. * ``tan(0) -> 0.0``
*********************************
<code>tanh</code>
==============================
<code><b>tanh(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
쌍곡선 탄젠트 값을 계산합니다. * ``tanh(0) -> 0.0``
*********************************
<code>toBoolean</code>
==============================
<code><b>toBoolean(<i>&lt;value1&gt;</i> : string) => boolean</b></code><br/><br/>
('t', 'true', 'y', 'yes', '1') 값을 true로 변환하고 ('f', 'false', 'n', 'no', '0') 값을 false로 변환하고, 다른 모든 값은 NULL로 변환합니다. * ``toBoolean('true') -> true``
* ``toBoolean('n') -> false``
* ``toBoolean('truthy') -> NULL``
*********************************
<code>toDate</code>
==============================
<code><b>toDate(<i>&lt;string&gt;</i> : any, [<i>&lt;date format&gt;</i> : string]) => date</b></code><br/><br/>
선택적 날짜 형식 지정 된 날짜를 문자열로 변환 합니다. 가능한 모든 형식에 대 한 Java SimpleDateFormat를 가리킵니다. 날짜 형식을 생략하면 다음 조합은 허용됩니다. [ yyyy, yyyy-[M]M, yyyy-[M]M-[d]d, yyyy-[M]M-[d]d, yyyy-[M]M-[d]d, yyyy-[M]M-[d]dT* ] * ``toDate('2012-8-8') -> 2012-8-8``
* ``toDate('12/12/2012', 'MM/dd/yyyy') -> 2012-12-12``
*********************************
<code>toDecimal</code>
==============================
<code><b>toDecimal(<i>&lt;value&gt;</i> : any, [<i>&lt;format&gt;</i> : integral], [<i>&lt;value3&gt;</i> : integral], [<i>&lt;value4&gt;</i> : string]) => decimal(10,0)</b></code><br/><br/>
숫자 또는 문자열을 10진수 값으로 변환합니다. 자릿수와 소수 자릿수를 지정하지 않으면 기본값인 (10,2)가 사용됩니다. 변환을 위해 선택적인 Java 10진수 형식을 사용할 수 있습니다.
* ``toDecimal(123.45) -> 123.45``
* ``toDecimal('123.45', 8, 4) -> 123.4500``
* ``toDecimal('$123.45', 8, 4,'$###.00') -> 123.4500``
*********************************
<code>toDouble</code>
==============================
<code><b>toDouble(<i>&lt;value&gt;</i> : any, [<i>&lt;format&gt;</i> : string]) => double</b></code><br/><br/>
숫자 또는 문자열을 배정도 값으로 변환합니다. 변환을 위해 선택적인 Java 10진수 형식을 사용할 수 있습니다.
* ``toDouble(123.45) -> 123.45``
* ``toDouble('123.45') -> 123.45``
* ``toDouble('$123.45', '$###.00') -> 123.45``
*********************************
<code>toFloat</code>
==============================
<code><b>toFloat(<i>&lt;value&gt;</i> : any, [<i>&lt;format&gt;</i> : string]) => float</b></code><br/><br/>
숫자 또는 문자열을 부동 소수점 값으로 변환합니다. 변환을 위해 선택적인 Java 10진수 형식을 사용할 수 있습니다. double은 자릅니다. * ``toFloat(123.45) -> 123.45``
* ``toFloat('123.45') -> 123.45``
* ``toFloat('$123.45', '$###.00') -> 123.45``
*********************************
<code>toInteger</code>
==============================
<code><b>toInteger(<i>&lt;value&gt;</i> : any, [<i>&lt;format&gt;</i> : string]) => integer</b></code><br/><br/>
모든 숫자 또는 문자열을 정수 값으로 변환합니다. 변환을 위해 선택적인 Java 10진수 형식을 사용할 수 있습니다. long, float, double은 자릅니다. * ``toInteger(123) -> 123``
* ``toInteger('123') -> 123``
* ``toInteger('$123', '$###') -> 123``
*********************************
<code>toLong</code>
==============================
<code><b>toLong(<i>&lt;value&gt;</i> : any, [<i>&lt;format&gt;</i> : string]) => long</b></code><br/><br/>
숫자 또는 문자열을 긴 값으로 변환합니다. 변환을 위해 선택적인 Java 10진수 형식을 사용할 수 있습니다. float, double은 자릅니다. * ``toLong(123) -> 123``
* ``toLong('123') -> 123``
* ``toLong('$123', '$###') -> 123``
*********************************
<code>toShort</code>
==============================
<code><b>toShort(<i>&lt;value&gt;</i> : any, [<i>&lt;format&gt;</i> : string]) => short</b></code><br/><br/>
숫자 또는 문자열을 짧은 값으로 변환합니다. 변환을 위해 선택적인 Java 10진수 형식을 사용할 수 있습니다. integer, long, float, double은 자릅니다. * ``toShort(123) -> 123``
* ``toShort('123') -> 123``
* ``toShort('$123', '$###') -> 123``
*********************************
<code>toString</code>
==============================
<code><b>toString(<i>&lt;value&gt;</i> : any, [<i>&lt;number format/date format&gt;</i> : string]) => string</b></code><br/><br/>
기본 데이터 형식을 문자열로 변환합니다. 숫자 및 날짜의 경우 형식을 지정할 수 있습니다. 지정하지 않으면 시스템 기본값은 picked.Java입니다. 숫자에는 10진수 형식이 사용됩니다. 모든 날짜 형식에 대 한 Java SimpleDateFormat 참조 기본 형식은 yyyy-월-일 * ``toString(10) -> '10'``
* ``toString('engineer') -> 'engineer'``
* ``toString(123456.789, '##,###.##') -> '123,456.79'``
* ``toString(123.78, '000000.000') -> '000123.780'``
* ``toString(12345, '##0.#####E0') -> '12.345E3'``
* ``toString(toDate('2018-12-31')) -> '2018-12-31'``
* ``toString(toDate('2018-12-31'), 'MM/dd/yy') -> '12/31/18'``
* ``toString(4 == 20) -> 'false'``
*********************************
<code>toTimestamp</code>
==============================
<code><b>toTimestamp(<i>&lt;string&gt;</i> : any, [<i>&lt;timestamp format&gt;</i> : string], [<i>&lt;time zone&gt;</i> : string]) => timestamp</b></code><br/><br/>
지정된 선택적 타임스탬프 형식으로 문자열을 날짜로 변환합니다. 가능한 모든 형식에 대 한 Java SimpleDateFormat를 가리킵니다. 타임 스탬프를 생략하면 기본 패턴 yyyy-[M]M-[d]d hh:mm:ss[.f...]가 사용됩니다. * ``toTimestamp('2016-12-31 00:12:00') -> 2012-8-8T00:12:00``
* ``toTimestamp('2016/12/31T00:12:00', 'MM/dd/yyyyThh:mm:ss') -> 2012-12-12T00:12:00``
*********************************
<code>toUTC</code>
==============================
<code><b>toUTC(<i>&lt;value1&gt;</i> : timestamp, [<i>&lt;value2&gt;</i> : string]) => timestamp</b></code><br/><br/>
타임스탬프를 UTC로 변환합니다. 'GMT', 'PST', 'UTC', 'America/Cayman' 형태로 선택적 표준 시간대를 제공할 수 있습니다. 기본적으로 현재 표준 시간대가 사용됩니다. * ``toUTC(currentTimeStamp()) -> 12-12-2030T19:18:12``
* ``toUTC(currentTimeStamp(), 'Asia/Seoul') -> 12-13-2030T11:18:12``
*********************************
<code>translate</code>
==============================
<code><b>translate(<i>&lt;string to translate&gt;</i> : string, <i>&lt;lookup characters&gt;</i> : string, <i>&lt;replace characters&gt;</i> : string) => string</b></code><br/><br/>
하나의 문자 세트를 문자열의 다른 문자 세트로 바꿉니다. 문자는 1:1로 대체됩니다. * ``translate('(Hello)', '()', '[]') -> '[Hello]'``
* ``translate('(Hello)', '()', '[') -> '[Hello'``
*********************************
<code>trim</code>
==============================
<code><b>trim(<i>&lt;string to trim&gt;</i> : string, [<i>&lt;trim characters&gt;</i> : string]) => string</b></code><br/><br/>
선행 및 후행 문자열을 삭제합니다. 두 번째 매개 변수를 지정하지 않으면 공백을 삭제합니다. 그렇지 않은 경우 두 번째 매개 변수에 지정된 모든 문자를 삭제합니다. * ``trim('!--!wor!ld!', '-!') -> 'wor!ld'``
*********************************
<code>true</code>
==============================
<code><b>true() => boolean</b></code><br/><br/>
항상 true 값을 반환합니다. 'true'라는 열이 있는 경우 함수 syntax(true())를 사용합니다. * ``isDiscounted == true()``
* ``isDiscounted() == true``
*********************************
<code>typeMatch</code>
==============================
<code><b>typeMatch(<i>&lt;type&gt;</i> : string, <i>&lt;base type&gt;</i> : string) => boolean</b></code><br/><br/>
열의 형식과 일치합니다. 패턴 식에서만 사용할 수 있습니다. number는 short, integer, long, double, float 또는 decimal과 일치하고, integral은 short, integer, long과 일치하고, fractional은 double, float, decimal과 일치하고, datetime은 date 또는 timestamp 형식과 일치합니다. * ``typeMatch(type, 'number') -> true``
* ``typeMatch('date', 'number') -> false``
*********************************
<code>upper</code>
==============================
<code><b>upper(<i>&lt;value1&gt;</i> : string) => string</b></code><br/><br/>
문자열을 대문자로 바꿉니다. * ``upper('bojjus') -> 'BOJJUS'``
*********************************
<code>variance</code>
==============================
<code><b>variance(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
열의 분산을 가져옵니다. * ``variance(sales) -> 122.12``
*********************************
<code>varianceIf</code>
==============================
<code><b>varianceIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
조건에 따라 열의 분산을 가져옵니다. * ``varianceIf(region == 'West', sales) -> 122.12``
*********************************
<code>variancePopulation</code>
==============================
<code><b>variancePopulation(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
열의 모집단 분산을 가져옵니다. * ``variancePopulation(sales) -> 122.12``
*********************************
<code>variancePopulationIf</code>
==============================
<code><b>variancePopulationIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
조건에 따라 열의 모집단 분산을 가져옵니다. * ``variancePopulationIf(region == 'West', sales) -> 122.12``
*********************************
<code>varianceSample</code>
==============================
<code><b>varianceSample(<i>&lt;value1&gt;</i> : number) => double</b></code><br/><br/>
열의 불편 분산을 가져옵니다. * ``varianceSample(sales) -> 122.12``
*********************************
<code>varianceSampleIf</code>
==============================
<code><b>varianceSampleIf(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : number) => double</b></code><br/><br/>
조건에 따라 열의 불편 분산을 가져옵니다. * ``varianceSampleIf(region == 'West', sales) -> 122.12``
*********************************
<code>weekOfYear</code>
==============================
<code><b>weekOfYear(<i>&lt;value1&gt;</i> : datetime) => integer</b></code><br/><br/>
지정된 날짜의 연중 주를 가져옵니다. * ``weekOfYear(toDate('2008-02-20')) -> 8``
*********************************
<code>xor</code>
==============================
<code><b>xor(<i>&lt;value1&gt;</i> : boolean, <i>&lt;value2&gt;</i> : boolean) => boolean</b></code><br/><br/>
논리 XOR 연산자입니다. ^ 연산자와 같습니다. * ``xor(true, false) -> true``
* ``xor(true, true) -> false``
* ``true ^ false -> true``
*********************************
<code>year</code>
==============================
<code><b>year(<i>&lt;value1&gt;</i> : datetime) => integer</b></code><br/><br/>
날짜의 연도 값을 가져옵니다. * ``year(toDate('2012-8-8')) -> 2012``

## <a name="next-steps"></a>다음 단계

[식 작성기를 사용 하는 방법을 알아봅니다](concepts-data-flow-expression-builder.md)
