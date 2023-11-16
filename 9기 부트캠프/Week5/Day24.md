# Day24 요약 및 헷갈리는 개념

## 스트림

1. 스트림 생성 
2. 중간 연산 (n번 수행 가능)
    * skip, limit, distinct, filter, map, flatmap, peek, sorted
3. 최종 연산 (1번)
    * foreach, sum, count, max, min, allMatch, anyMatch, noneMatch, findFirst, reduce, collect

**collect() vs reduce()**

* reduce() - 전체, 최종연산 - sum(), count()
* collect() - 그룹별 reduce()

> 스트림 사용법은 아직 생소하다. 실습 많이하기.

