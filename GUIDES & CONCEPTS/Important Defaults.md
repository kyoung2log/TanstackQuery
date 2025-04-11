### 탄스택 쿼리의 주요 기본 값

- 기본적으로 `useQuery` 나 `useInfiniteQuery`로 만든 쿼리 인스턴스는 기본 값이 stale 상태다. staleTime이 0이기 때문에 데이터를 가져오는 즉시 stale 상태가 됨

- 오래된 커리는 다음 상황에서 자동으로 재요청 된다.

  - 쿼리의 새 인스턴스가 마운트될떄 -> `refetchOnMount`
  - 브라우저 창이 다시 포커스될때 -> `refetchOnWindowFocus`
  - 네트워크가 재연결될때 -> `refetchOnReconnect`
  - `refetchInterval` 설정한 경우 -> `refetchInterval`

- 활성 인스턴스가 없는 쿼리 결과는 비활성으로 표시되며 5분간 캐시에 남아있음
  -> 활성 인스턴스가 없다는 것은 `useQuery` 내부에 전달된 값이 언마운트 되었다는 의미
  -> 5분내에 다시 마운트 되면 캐싱된 값을 가져다 씀
- 비활성 쿼리는 기본적으로 5분 후에 GC됨 -> `gcTime`
