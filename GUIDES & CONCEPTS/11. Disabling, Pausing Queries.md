## Disabling/Pausing Queries

- 자동으로 쿼리 요청되는것을 비활성화 하고싶으면 enable 옵션을 사용하거라
- 근데 "The query will ignore query client invalidateQueries and refetchQueries calls that would normally result in the query refetching" 이 말은 쿼리 무효화도 처리 안해준다는 것 같은데 그럼 탄스택 쿼리를 쓰는 의미가 있나 ..? -> 바로 아래에 ㅋㅋ 똑같은 말이 있네요..
- 대부분의 경우에 사용자가 원하는건 지연로딩이다. 즉 초기에 바로 요청을 보내는 것이 아니라, 어떤 데이터가 로드된 후 요청을 보내는 식이니까 무작정 `enabled`에 `false`를 쓰지말고 조건부로 처리해라

  ```tsx
  function Todos() {
    const [filter, setFilter] = React.useState('');

    const { data } = useQuery({
      queryKey: ['todos', filter],
      queryFn: () => fetchTodos(filter),
      // ⬇️ disabled as long as the filter is empty -> 이렇게 조건부로 하걸아
      enabled: !!filter,
    });

    return (
      <div>
        <FiltersForm onApply={setFilter} />
        {data && <TodosTable data={data} />}
      </div>
    );
  }
  ```

- `isLoading` === `isPending && isFetching` 입니다.

- TS 유저는 `enabled = false` 대신 skipToken을 선호할 수 있다.

  ```tsx
  import { skipToken, useQuery } from '@tanstack/react-query';

  function Todos() {
    const [filter, setFilter] = React.useState<string | undefined>();

    const { data } = useQuery({
      queryKey: ['todos', filter],
      // ⬇️ disabled as long as the filter is undefined or empty
      queryFn: filter ? () => fetchTodos(filter) : skipToken,
    });

    return (
      <div>
        // 🚀 applying the filter will enable and execute the query
        <FiltersForm onApply={setFilter} />
        {data && <TodosTable data={data} />}
      </div>
    );
  }
  ```

- `enabled = false`을 사용하면 데이터의 타입을 `데이터타입 | undefined`로 지정해야 한다. 이러면 명확한 타입 지정이 어려워짐
- 따라서 skipToken을 사용하면 조건부로 쿼리요청을 할 수 있다.
- 하지만 이 경우에는 refetch와 함께 작동하지 않음
- 그렇기 때문에 **조건이 만족되지 않으면 아예 쿼리를 "존재하지 않는 것처럼" 다루고 싶을 때 사용하면 좋다.**
