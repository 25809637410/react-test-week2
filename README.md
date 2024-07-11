### [과제] 숙련주차 과제 답

1. 추가하기 버튼을 클릭해도 추가한 아이템이 화면에 표시되지 않음.
ADD_TODO의 액션을 수행하는 todos.js 리듀서에서 새 todo를 추가할 때 상태를 업데이트 하지 않고 배열을 덮어쓰는 문제를 해결하기 위해 todos.js 코드를 수정함.
Form.jsx에서 todo 추가기능이 제대로 작동하지 않아 useDispatch를 수정함으로 작동가능하게 수정함

```
// todos.js

case ADD_TODO:
  return {
    ...state,
    todos: [...state.todos, action.payload],
  };

// Form.jsx

// useDispatch 사용

const dispatch = useDispatch();

// onSubmitHandler 수정

 const onSubmitHandler = (event) => {
    event.preventDefault();
    if (todo.title.trim() === "" || todo.body.trim() === "") return;
    
    dispatch(addTodo({ ...todo, id }));
    setTodo({
      id: 0,
      title: "",
      body: "",
      isDone: false,
    });
  };

```


2. 추가하기 버튼 클릭 후 기존에 존재하던 아이템들이 사라짐
1번 문제와 해결 방법이 같음

```
// todos.js

case ADD_TODO:
  return {
    ...state,
    todos: [...state.todos, action.payload],
  };
```


3. 삭제 기능이 동작하지 않음.
삭제 기능에 대한 액션의 정의가 되지 않았기 때문에 todos 리듀서에 삭제 케이스를 추가함
```
// todos.js

case DELETE_TODO:
  return {
    ...state,
    todos: state.todos.filter((todo) => todo.id !== action.payload),
  };

```

4. 상세 페이지에 진입 하였을 때 데이터가 업데이트 되지 않음.
Detail.jsx에서  useEffect에 대한 `getTodoByID` 액션을 디스패치 해줌

```
// Detail.jsx

useEffect(() => {
  dispatch(getTodoByID(id));
}, [dispatch, id]);

```

5. 완료된 카드의 상세 페이지에 진입 하였을 때 올바른 데이터를 불러오지 못함.
4번의 해결방법과 같음

```
// Detail.jsx

useEffect(() => {
  dispatch(getTodoByID(id));
}, [dispatch, id]);

```

6. 취소 버튼 클릭시 기능이 작동하지 않음.
진행 중인 할 일과 완료된 할 일 모두에 대해 Link 컴포넌트 경로를 일관되게 설정하고, "취소" 버튼의 onClick 핸들러에서 id 매개변수를 전달하도록 수정합니다.

```
// List.jsx
// ...
const onToggleStatusTodo = (id) => {
  dispatch(toggleStatusTodo(id));
};
// ...

// 완료된 할 일에 대한 `todos.map` 내부
<StButton
	borderColor="green"
        onClick={() => onToggleStatusTodo(todo.id)}
 >
 {todo.isDone ? "취소!" : "완료!"}
</StButton>

//…

```
