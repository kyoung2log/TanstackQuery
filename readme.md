## README

이 레포지토리는 `Tanstack Query` 공식문서를 톺아보고 알게된 점을 기록합니다.

<br/>

### 👀 공식문서 읽으면서 알게된 점

**`전체적으로 배운 것`**

- 영어 문서를 읽는 방법... 아직 완전하진 않지만 계속 도전해야겠다.
- 공식문서가 진~짜 친절하다는 것.. '이 정도까지 고려한다고?' 싶을 만큼, 사용자 경험을 개선할 수 있는 옵션을 제공한다. 사용자 수가 많은 이유를 알겠음
- 패키지를 추가할 때, 서비스의 요구사항이 패키지에 구현되어 있는지 아닌지 확인하면서 선택해야겠다. 그러려면 영어를 잘해서 공식문서를 한눈에 파악할 줄 알아야겠지..

**`GUIDES & CONCEPTS`**

- `important defaults` 캐싱이 된다 정도만 알았지, 어느 경우에 오래된 상태로 취급하는지와 `inactive` 상태로 전환 뒤 5분 뒤 가비지 컬렉터의 대상(캐시에서 삭제)이 된다.
- `important defaults` 5분간 캐싱이라는데, 한 60분 캐싱하면 성능이 안좋아질까 ?
- `queries` 서버 데이터를 수정하는 요청의 경우 뮤테이션을 사용해라... 라는걸 공식문서에서 명시적으로 확인할 수 있었다.
- `queries` fetchStatus가 있는것도 첨 알았는데 이거로 상태를 조합할 수 있다니 신기. 특히 status는 데이터의 상태를, fetchStatus는 queryFn의 실행 상태를 구분하는 것을 알게 되었다.
- `query keys` 쿼리키 배열 순서는 중요하지만 객체 내부 요소는 해시를 사용하기 때문에 순서는 중요하지 않다.
- `query functions` 쿼리 함수에 `QueryFunctionContext`가 자동으로 같이 전달된다.
- `query options` 동일한 쿼리 요청을 여러 군데에서 사용되는 경우(ex. `useQuery`, `useSuspenseQuery`, `useQueries` 등) 쿼리 옵션을 사용하면 일관적으로 관리할 수 있다.
- `parallel queries` 기본적으로 `useQuery`의 요청이 병렬로 수행된다는 것을 알게됨. 그리고 `useQueries`가 동적 쿼리를 요청하는 훅이구나 라는걸 알게됨(그동안은 useQuery와 차이점이 뭐지 했었음)
- `background fetching indicators` `useIsFetching`라는 훅을 통해 데이터를 fetching 받는중인지 아닌지에 대해 알 수 있다는 것.. 얘를 사용하면 깃허브 프로그레스바를 구현하기 용이할 것 같다. 직접 사용해봐야 알겠지만..!
- `disabling/pausing queries` isLoading === isPending && isFetching 라는 것
- `disabling/pausing queries` skipToken을 사용해서 요청하면 enable을 사용했을 경우보다 명확한 타입 지정이 가능하다는 것을 알게되었고, 이 경우는 refetch에서 동작하지 않으므로, 조건이 만족되지 않으면 아예 쿼리를 "존재하지 않는 것처럼" 다루고 싶을 때 사용하면 좋다는 것을 알게됨
- `invalidations from mutations` 뮤테이션의 올바른 사용방법을 알게되었다...! 그간 필요할때마다 검색해서 코드 긁어왔는데... 흑..
- `updates from mutation responses` 뮤테이션 실행 후 쿼리무효화 + 네트워크 요청 없이 뮤테이션 응답 객체로 네트워크 부하를 줄이는 방법을 알게되었다. 하지만 상황에 따라 invalidateQueries와 setQueryData의 사용을 명확히 구분하는 것이 중요할 듯 하다.

<br/>

### 🙇‍♀️ REF

- [Tanstack Query 공식문서](https://tanstack.com/query/latest)
- [탄스택 쿼리 공식문서 톺아보기 스터디 노션](https://tanstackquery.notion.site/?v=1ce2522077a080279f6f000c4afae6c6&pvs=74)
