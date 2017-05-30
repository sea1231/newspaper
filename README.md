newspaper
================

뉴스 크롤러 R
-------------

### - 대부분의 신문사 뉴스를 수집하는 것을 목적으로 하는 크롤러 제작 프로젝트

### 목적: 국내외 뉴스사이트 크롤링 패키지

### WHY 뉴스?

1.  사이트마다 상이하지만 form 일정 *Note: 뉴스리스트 / 헤드라인 / 기자 / 본문 / 댓글 등*
2.  연구용 필요성

### 개발방향

-   사용자들로 하여금 뉴스 사이트의 헤드라인, 본문 등의 xpath, css만 추가 가능하도록 하여 재생산 가능한 패키지 제작

설계
----

### 엔드유저는 configure 파일만 접근

-   검색어
-   뉴스사이트

\[검색어 파일 구조\]

| 순번 | 검색어 | 기간시작 | 기간끝   |
|------|--------|----------|----------|
| 1    | 대통령 | 20150101 | 20151231 |
| 2    | 공휴일 | NULL     | NULL     |

\[뉴스사이트 파일 구조\]

<table>
<colgroup>
<col width="3%" />
<col width="3%" />
<col width="6%" />
<col width="10%" />
<col width="6%" />
<col width="6%" />
<col width="14%" />
<col width="5%" />
<col width="13%" />
<col width="6%" />
<col width="8%" />
<col width="7%" />
<col width="9%" />
</colgroup>
<thead>
<tr class="header">
<th>순번</th>
<th>구분</th>
<th>뉴스사명</th>
<th>주소</th>
<th>로긴유무</th>
<th>검색실행</th>
<th>리스트</th>
<th>페이지</th>
<th>제목</th>
<th>본문</th>
<th>뉴스코드유무</th>
<th>페이지건수</th>
<th>총페이지수</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>1</td>
<td>신문</td>
<td>조선일보</td>
<td><a href="http://" class="uri">http://</a>~~.com</td>
<td>N</td>
<td>NULL</td>
<td>.result.news dl dt a</td>
<td>page_no</td>
<td>#news_title_text_id</td>
<td>div.par p</td>
<td>NULL</td>
<td>10</td>
<td>h3 em</td>
</tr>
</tbody>
</table>

이슈: 주소를 GET으로 처리하되, 검색어 등을 변수 $search 등의 변수로 간주

### Code 이슈

(Docker와 Slenium은 최대한 자제?)

이슈: WHY? 순수한 R코드로 작성? 글을 적는 시점에도 풀리지 않는 의문점: 왜 나는 굳이 PYTHON 대신 R로 하는가? R 사용자들의 참여를 돕기 위해?

### Workflow

1.  configure 처리
2.  기본 URL
3.  (검색결과기본 URL - 검색 없을 시 생략)
4.  뉴스페이지

-   Link 추출, Max 페이지 추출(초기 1회)
-   이슈: 페이지에 더보기가 있는 경우 처리, async

1.  뉴스수집

-   뉴스헤더, 기자, 본문, 날짜 등
-   이슈: async

1.  결과물 종합

-   이슈: 한 페이지별 저장? 1건 별 저장?
