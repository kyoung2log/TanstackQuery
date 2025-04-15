## README

이 레포지토리는 `Tanstack Query` 공식문서를 톺아보고 알게된 점을 기록합니다.

<br/>

### 👀 공식문서 읽으면서 알게된 점

**`GUIDES & CONCEPTS`**

- `important defaults` 캐싱이 된다 정도만 알았지, 어느 경우에 오래된 상태로 취급하는지와 `inactive` 상태로 전환 뒤 5분 뒤 가비지 컬렉터의 대상(캐시에서 삭제)이 된다.
- `important defaults` 5분간 캐싱이라는데, 한 60분 캐싱하면 성능이 안좋아질까 ?
- `queries` 서버 데이터를 수정하는 요청의 경우 뮤테이션을 사용해라... 라는걸 공식문서에서 명시적으로 확인할 수 있었다.
- `queries` fetchStatus가 있는것도 첨 알았는데 이거로 상태를 조합할 수 있다니 신기. 특히 status는 데이터의 상태를, fetchStatus는 queryFn의 실행 상태를 구분하는 것을 알게 되었다.
- `query keys` 쿼리키 배열 순서는 중요하지만 객체 내부 요소는 해시를 사용하기 때문에 순서는 중요하지 않다.
- `query functions` 쿼리 함수에 `QueryFunctionContext`가 자동으로 같이 전달된다.
- `query options` 동일한 쿼리 요청을 여러 군데에서 사용되는 경우(ex. `useQuery`, `useSuspenseQuery`, `useQueries` 등) 쿼리 옵션을 사용하면 일관적으로 관리할 수 있다.
- `parallel queries` 기본적으로 `useQuery`의 요청이 병렬로 수행된다는 것을 알게됨. 그리고 `useQueries`가 동적 쿼리를 요청하는 훅이구나 라는걸 알게됨(그동안은 useQuery와 차이점이 뭐지 했었음)

<br/>

### 🙇‍♀️ REF

- [Tanstack Query 공식문서](https://tanstack.com/query/latest)
- [탄스택 쿼리 공식문서 톺아보기 스터디 노션](https://fedeepdive.notion.site/?v=1ce2522077a080279f6f000c4afae6c6&pvs=74)
