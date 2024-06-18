#  数据管理与缓存

## 一.什么是React Query

React Query 是一个用于**管理和缓存服务器数据的 React 库**。它旨在简化在 React 应用程序中管理远程数据的复杂性，提供了一种声明性的、灵活的方式来处理数据获取、缓存和状态管理。React Query 的核心概念包括查询（Queries）、变异（Mutations）、无限滚动（Infinite Queries）等。

以下是 React Query 的一些关键概念：

1. **查询（Queries）：** Queries 用于获取数据。通过定义一个查询，你可以声明性地指定需要获取的数据，并且 React Query 会负责数据的获取、缓存和状态管理。Queries 可以接受参数，支持缓存、重新获取、后台刷新等功能。

2. **变异（Mutations）：** Mutations 用于对服务器进行更改。类似于 Queries，Mutations 提供了一种声明性的方式来指定需要进行的数据变更操作。React Query 会处理请求、缓存更新和状态管理。

3. **无限滚动（Infinite Queries）：** 用于处理无限滚动列表或分页数据的特定查询类型。它允许你在滚动时获取更多的数据，并自动处理数据的缓存和状态。

4. **缓存：** React Query 提供了强大的缓存系统，可以配置和定制缓存策略，支持手动和自动触发缓存的刷新。

5. **状态管理：** React Query 通过 React 的 Context API 进行状态管理，可以方便地在整个应用程序中共享查询状态。

6. **自动化：** 提供了许多自动化的特性，如自动重试、自动轮询、自动无效等，以减少手动处理数据流程的复杂性。

React Query 是一个强大的工具，使得在 React 应用中管理远程数据变得更加简单和灵活。它的设计理念是通过声明性的方式处理数据，从而降低了数据管理的复杂性，提高了开发效率。





## 二.useQuery钩子

```tsx
import { useQuery } from "@tanstack/react-query";
import axios from "axios";


interface Todo {
  id: number;
  title: string;
  userId: number;
  completed: boolean;
}

const TodoList = () => {
  const fetchTodos = () =>
    axios 
      .get<Todo[]>("https://jsonplaceholder.typicode.com/todos")
      .then((res) => res.data);

  const {data:todos,error,isLoading} = useQuery<Todo[],Error>({
    queryKey: ["todos"],
    queryFn: fetchTodos,
  });

  if (isLoading) return <p>Loading....</p>;  //这样直接设置了加载器，很方便
  
  if (error) return <p>{error.message}</p>;

  return (
    <ul className="list-group">
      {todos?.map((todo) => (
        <li key={todo.id} className="list-group-item">
          {todo.title}
        </li>
      ))}
    </ul>
  );
};

export default TodoList;
```

### queryKey

`queryKey` 参数用于在 React Query 中唯一标识一个查询。它是一个用于识别和管理缓存数据的关键属性。让我更详细地解释一下：

1. **唯一标识查询：**
   - 在 React Query 中，每个使用 `useQuery` 钩子的地方都会定义一个查询，用于获取特定类型的数据。
   - `queryKey` 的目的是在这些查询之间提供唯一的标识，以便 React Query 可以正确地管理和区分不同的查询。

2. **数组形式的标识：**
   - `queryKey` 是一个数组，通常包含了用于查找数据的标识符或关键信息。
   - 数组的元素可以是字符串、数字、对象等，取决于你想要查询的数据的唯一标识。

3. **共享缓存：**
   - 使用相同的 `queryKey` 在不同的地方进行相同类型的查询，会使这些查询共享相同的缓存。
   - 如果多个组件或页面都需要获取相同的数据，使用相同的 `queryKey` 可以确保它们使用相同的缓存，从而提高性能和避免重复获取相同的数据。

4. **动态查询：**
   - 虽然 `queryKey` 可以是一个静态的数组，但你也可以使用动态生成的数组，例如包含变量、函数返回值等。
   - 这使得你可以根据特定条件生成不同的 `queryKey`，从而实现根据不同条件获取不同数据的需求。

总体而言，`queryKey` 是 React Query 中用于在不同查询之间唯一标识和管理缓存的关键概念。它允许你明确指定你的查询标识，以确保在整个应用程序中查询的一致性和正确性。

这段代码是使用 React Query 库来获取和显示待办事项列表的一个示例。下面是对代码的详细解释：

1. **fetchTodos 函数：**
   
   ```typescript
   const fetchTodos = () =>
     axios
       .get<Todo[]>("https://jsonplaceholder.typicode.com/todos")
       .then((res) => res.data);
   ```
   - `fetchTodos` 是一个异步函数，用于发起对 JSONPlaceholder API 的 GET 请求，该 API 提供了模拟的待办事项数据。
   - `axios.get<Todo[]>("https://jsonplaceholder.typicode.com/todos")` 发起了一个 GET 请求，其中 `<Todo[]>` 表示预期的响应数据类型是 `Todo` 对象数组。
   - `.then((res) => res.data)` 处理异步请求的响应，从中提取实际的数据。
   
2. **useQuery 钩子的使用：**
   ```typescript
   const {data: todos, error} = useQuery<Todo[], Error>({
     queryKey: ["todos"],
     queryFn: fetchTodos,
   });
   ```
   - `useQuery` 是 React Query 提供的一个钩子，用于执行查询操作。这里它接收一个泛型参数 `<Todo[], Error>`，表示查询返回的数据类型和可能出现的错误类型。
   - `queryKey: ["todos"]` 指定查询的键（key）。这个键是用于标识查询的唯一标识符，这里使用了字符串数组 `["todos"]`。
   - `queryFn: fetchTodos` 是一个函数，用于执行实际的查询操作，这里调用了之前定义的 `fetchTodos` 函数。

3. **错误处理：**
   ```typescript
   if (error) return <p>{error.message}</p>;
   ```
   - 如果在查询过程中发生了错误，会通过 `error` 变量捕获，并在页面上显示错误消息。

4. **渲染待办事项列表：**
   ```typescript
   return (
     <ul className="list-group">
       {todos?.map((todo) => (
         <li key={todo.id} className="list-group-item">
           {todo.title}
         </li>
       ))}
     </ul>
   );
   ```
   - 如果没有发生错误，通过 `todos?.map` 渲染待办事项列表。
   - `todos?.map` 利用可选链语法，确保 `todos` 不为 `null` 或 `undefined`，然后遍历每个待办事项并显示其标题。

总体而言，这段代码演示了如何使用 React Query 进行数据查询，以及如何处理可能发生的错误。



## 三.创建一个自定义查询钩子

**TodoList.tsx**

```tsx
import useTodo from "../hooks/useTodo";

const TodoList = () => {
  const { data: todos, error, isLoading } = useTodo();

  if (isLoading) return <p>Loading....</p>;

  if (error) return <p>{error.message}</p>;

  return (
    <ul className="list-group">
      {todos?.map((todo) => (
        <li key={todo.id} className="list-group-item">
          {todo.title}
        </li>
      ))}
    </ul>
  );
};

export default TodoList;
```

**useTodo.ts**

```tsx
import { useQuery } from "@tanstack/react-query";
import axios from "axios";

interface Todo {
  id: number;
  title: string;
  userId: number;
  completed: boolean;
}

const useTodo = () => {
  const fetchTodos = () =>
    axios
      .get("https://jsonplaceholder.typicode.com/todos")
      .then((res) => res.data);

  return useQuery<Todo[], Error>({
    queryKey: ["todos"],
    queryFn: fetchTodos,
  });
};

export default useTodo;

```



## 四.使用React Query 开发工具(DevTools)

下载包

```
npm i @tanstack/react-query-devtools@4.28
```





## 五.自定义查询设置

默认的设置已经完全可以了，不需要去自定义

唯一需要自定义的是陈腐的时间(在缓存中存在的时间) （有时我们需要高频获取数据来更新状态）



在useQuery钩子中去自定义

```tsx
import { useQuery } from "@tanstack/react-query";
import axios from "axios";


interface Todo {
    id: number;
    title: string;
    userId: number;
    completed: boolean;
  }

const useTodo = () => {
    const fetchTodos = () =>
    axios
      .get<Todo[]>("https://jsonplaceholder.typicode.com/todos")
      .then((res) => res.data);

    return useQuery<Todo[],Error>({
        queryKey: ["todos"],
        queryFn: fetchTodos,
        staleTime: 10 * 1000, //10秒
      });
}


export default useTodo;
```



## 六.参数化查询

**PostList.tsx**

```tsx
import { useState } from "react";
import usePosts from "../hooks/usePosts";


const PostList = () => {
  const [userId,setUserId] = useState<number>();
  const { data: posts, error, isLoading } = usePosts(userId);
 
  if (isLoading) return <p>Loading...</p>;

  if (error) return <p>{error.message}</p>;

  return (
    <>
      <select
        onChange={(event) => setUserId(parseInt(event.target.value))}
        value={userId}  
        className="form-select mb-3">
        <option value=""></option>
        <option value="1">User 1</option>
        <option value="2">User 2</option>
        <option value="3">User 3</option>
      </select>
      <ul className="list-group">
        {posts?.map((post) => (
          <li key={post.id} className="list-group-item">
            {post.title}
          </li>
        ))}
      </ul>
    </>
  );
};

export default PostList;
```

**usePosts.ts**

```tsx
import { useQuery } from "@tanstack/react-query";
import axios from "axios";

interface Post {
  id: number;
  title: string;
  body: string;
  userId: number;
}

const usePosts = (userId: number | undefined) =>
  useQuery<Post[], Error>({
    queryKey: userId ? ["users", userId, "posts"] : ["posts"],
    queryFn: () =>
      axios
        .get("https://jsonplaceholder.typicode.com/posts", {
          params: {
            userId,
          },
        })
        .then((res) => res.data),
    staleTime: 10 * 60 * 1000, //1m
  });
export default usePosts;


```

**它通过传递一个状态变量到useQuery钩子中来切换用户信息**

在`usePosts.ts`文件中，`params: { userId }` 是用于发送HTTP GET 请求时的参数设置。在这里，它是通过axios库发送的GET请求，针对JSONPlaceholder（一个免费的在线REST API服务）的`https://jsonplaceholder.typicode.com/posts`端点。

具体来说，这段代码是将`userId`作为请求的参数传递给服务器。在JSONPlaceholder中，当你请求 `/posts` 时，你可以通过参数 `userId` 来过滤出特定用户的帖子。这是一种模拟真实世界中，根据用户的标识来获取相应的数据的常见方式。

例如，如果你选择了一个用户（通过`setUserId`设置了`userId`），然后在请求中使用了`axios.get`，它会将该用户的`userId`作为参数发送到服务器。服务器将返回与该用户相关的帖子数据，这样你就可以在组件中显示这些帖子。

总结起来，`params: { userId }` 的作用是将选定的用户ID作为参数添加到GET请求中，以获取与该用户相关的帖子数据。







## 七.分页查询

**PostList.tsx**

```tsx
import { useState } from "react";
import usePosts from "../hooks/usePosts";


const PostList = () => {
  const pageSize = 10;
  const [page, setPage] = useState(1);
  const { data: posts, error, isLoading } = usePosts({page,pageSize});
 
  if (isLoading) return <p>Loading...</p>;

  if (error) return <p>{error.message}</p>;

  return (
    <>
      <ul className="list-group">
        {posts?.map((post) => (
          <li key={post.id} className="list-group-item">
            {post.title}
          </li>
        ))}
      </ul>
      <button 
      disabled={page===1}
      className="btn btn-primary my-3"
      onClick={() => setPage(page-1)}>上一页</button>
      <button 
      className="btn btn-primary my-3 ms-3"
      onClick={() => setPage(page+1)}>下一页</button>
    </>
  );
};

export default PostList;

```

**usePosts.ts**

```tsx
import { useQuery } from "@tanstack/react-query";
import axios from "axios";

interface Post {
  id: number;
  title: string;
  body: string;
  userId: number;
}

interface PostQuery {
  page: number;
  pageSize: number;
}

const usePosts = (query: PostQuery) =>
  useQuery<Post[], Error>({
    queryKey: ["posts",query],
    queryFn: () =>
      axios
        .get("https://jsonplaceholder.typicode.com/posts",{
          params: {
            _start: (query.page - 1) * query.pageSize,
            _limit: query.pageSize,
          }
        })
        .then((res) => res.data),
    staleTime: 10 * 60 * 1000, //1m
    keepPreviousData:true
  });
export default usePosts;

```

在`usePosts.ts`文件中，`params`被用于向服务器发送GET请求时的参数设置。在你的例子中，使用了`axios`库，该库允许你通过`params`对象来指定GET请求的参数。让我解释一下相关的部分：

1. **`params: { _start: (query.page - 1) * query.pageSize, _limit: query.pageSize }`：**
   - `_start` 和 `_limit` 是JSONPlaceholder API 特定的参数，用于分页。
   - `_start` 表示从哪一条记录开始获取，计算方式是 `(query.page - 1) * query.pageSize`。这里的`query.page`是你在组件中设置的当前页码，而`query.pageSize`是每页的数据量。
   - `_limit` 表示每页获取的记录数，即`query.pageSize`。

2. **`keepPreviousData: true`：**
   - 这是React Query库的一个配置选项。
   - 当`keepPreviousData`设置为`true`时，即使在数据正在重新加载时，React Query也会保留上一次成功加载的数据。**这对于在重新加载新数据时保持用户界面的一致性很有用。**在你的例子中，通过点击"上一页"或"下一页"按钮时，新数据正在加载，但是React Query会保留上一次的数据，直到新数据加载成功。
   

总结：`params`中的`_start`和`_limit`用于分页，根据当前页码和每页数据量来计算获取数据的范围。`keepPreviousData: true` 则是为了保持在数据重新加载时保留先前加载的数据。

**_start**

`_start` 是用于指定**从数据集的哪一条记录开始获取数据的参数**，通常用于实现分页。在你的例子中，`_start` 的计算方式是 `(query.page - 1) * query.pageSize`。

具体来说，假设你有一个包含100条数据的集合，每页显示10条数据。用户想要查看第三页的数据，此时 `query.page` 的值是3，`query.pageSize` 的值是10。那么计算 `_start` 的方式为 `(3 - 1) * 10`，结果是20。

这意味着你会从数据集的第21条记录开始获取，以获取第三页的数据。通过调整 `_start` 的值，你可以控制从数据集的哪一条记录开始获取数据，从而实现分页效果。

在JSONPlaceholder API中，使用 `_start` 和 `_limit` 这两个参数来实现分页非常常见。 `_start` 表示从哪一条记录开始获取，而 `_limit` 表示每页获取的记录数。



### `params`被用于向服务器发送GET请求时的参数设置

在Web开发中，当你使用HTTP协议中的GET请求时，你可以通过URL的查询字符串（query string）来传递参数。`params`就是一个对象，用于设置这些查询参数。

在JavaScript的AJAX请求或使用类似于axios的HTTP库时，你可以通过`params`选项将一个包含键值对的对象传递给服务器。这些键值对就是你要发送到服务器的查询参数。

例如，考虑以下URL：

```
https://example.com/api/data?param1=value1&param2=value2
```

这里，`param1`和`param2`就是查询参数，而它们的值分别是`value1`和`value2`。在axios中，你可以通过`params`选项来设置这些参数：

```javascript
axios.get('https://example.com/api/data', {
  params: {
    param1: 'value1',
    param2: 'value2'
  }
})
```

在你的`usePosts.ts`中，具体的例子是：

```javascript
axios.get("https://jsonplaceholder.typicode.com/posts", {
  params: {
    _start: (query.page - 1) * query.pageSize,
    _limit: query.pageSize,
  }
})
```

这样，`_start`和`_limit`就成为了查询参数，通过`axios`库发送给了服务器。这是一种通用的方式，通过GET请求的查询参数来告诉服务器你想要获取特定的数据。



## 八.无限查询



**PostList.tsx**

```tsx
import usePosts from "../hooks/usePosts";
import React from "react";

const PostList = () => {
  const pageSize = 10;
  const {
    data,
    error,
    isLoading,
    fetchNextPage,
    isFetchingNextPage,
  } = usePosts({ pageSize });

  if (isLoading) return <p>Loading...</p>;

  if (error) return <p>{error.message}</p>;

  return (
    <>
      <ul className="list-group">
        {data.pages.map((page,index) => (
          <React.Fragment key={index}>
            {page.map((post) => (
              <li key={post.id} className="list-group-item">
                {post.title}
              </li>
            ))}
          </React.Fragment>
        ))}
      </ul>
      <button
        className="btn btn-primary my-3 ms-3"
        disabled={isFetchingNextPage}
        onClick={() => fetchNextPage()}
      >
        {isFetchingNextPage ? "Loading..." : "Load More"}
      </button>
    </>
  );
};

export default PostList;

```



**usePosts.ts**

```tsx
import { useInfiniteQuery, useQuery } from "@tanstack/react-query";
import axios from "axios";

interface Post {
  id: number;
  title: string;
  body: string;
  userId: number;
}

interface PostQuery {
  pageSize: number;
}

const usePosts = (query: PostQuery) =>
  useInfiniteQuery<Post[], Error>({
    queryKey: ["posts",query],
    queryFn: ({ pageParam=1 }) =>
      axios
        .get("https://jsonplaceholder.typicode.com/posts",{
          params: {
            _start: (pageParam - 1) * query.pageSize,
            _limit: query.pageSize,
          }
        })
        .then((res) => res.data),
    staleTime: 10 * 60 * 1000, //1m
    keepPreviousData:true,
    getNextPageParam: (lastPage, allPages) => {
      // 1 -> 2
      return lastPage.length > 0 ? allPages.length + 1 : undefined;
    }
  });
export default usePosts;

```

在 `useInfiniteQuery` 中，`getNextPageParam` 函数用于指定下一页的参数，它接受两个参数 `lastPage` 和 `allPages`。让我们详细解释这两个参数的含义和用法。

### `getNextPageParam` 函数

`getNextPageParam` 函数的主要目的是根据当前的分页数据计算下一页的页码。`useInfiniteQuery` 使用这个函数来确定何时以及如何加载更多数据。

### 参数解释

1. **`lastPage`**：
   - `lastPage` 是前一次请求返回的数据。它表示最近一次加载的数据页面的内容。
   - 例如，如果你当前在加载第2页，那么 `lastPage` 就包含第2页的数据。
2. **`allPages`**：
   - `allPages` 是一个数组，包含了所有已加载的数据页。每个元素都是一个页面的数据。
   - 例如，如果你已经加载了前两页，那么 `allPages` 将是一个包含第1页和第2页数据的数组。



## 九.Mutating Data 

在 React Query 中，“数据变异”指的是**对缓存中的数据进行更改或更新**。React Query 提供了一组变异函数，允许您以不同的方式与数据进行交互，**例如添加、更新或删除记录。变异通常用于执行修改服务器上数据的操作。**

**TodoForm.tsx**

```tsx
import { useMutation, useQueryClient } from "@tanstack/react-query";
import { useRef } from "react";
import { Todo } from "../hooks/useTodo";
import axios from "axios";

const TodoForm = () => {
  const queryClient = useQueryClient();
  const addTodo = useMutation({
    mutationFn: (todo: Todo) =>
      axios
        .post<Todo>("https://jsonplaceholder.typicode.com/todos", todo)
        .then((res) => res.data),
    onSuccess: (saveTodo, newTodo) =>{
      console.log(saveTodo)
      //更新数据,在前端上
      //方法一: 使该数据无效，重新获取
      //queryClient.invalidateQueries({
      //  queryKey: ['todos']
      //})

      //方法二:在缓存中更新数据
      queryClient.setQueryData<Todo[]>(['todos'], todos=>[saveTodo,...(todos||[])])
    }
  }); 
  const ref = useRef<HTMLInputElement>(null);

  return (
    <form
      className="row mb-3"
      onSubmit={(event) => {
        event.preventDefault();

        if (ref.current && ref.current.value)
          addTodo.mutate({
            id: 0,
            title: ref.current?.value,
            completed: false,
            userId: 1,
          });
      }}
    >
      <div className="col">
        <input ref={ref} type="text" className="form-control" />
      </div>
      <div className="col">
        <button className="btn btn-primary">Add</button>
      </div>
    </form>
  );
};

export default TodoForm;

```

这是一个React组件，用于添加Todo项的表单，同时使用了React Query中的`useMutation`和`useQueryClient`钩子。以下是对这个组件的解释：

1. **`useQueryClient`：**
   - `useQueryClient` 是 React Query 提供的一个钩子，用于获取当前的 QueryClient 实例。
   - QueryClient 是 React Query 库的核心，用于管理数据查询和缓存等操作。

2. **`useMutation` 钩子：**
   - `useMutation` 用于定义一个数据变异（mutation）。在这里，它用于发起一个 POST 请求，将新的 Todo 项添加到服务器上。
   - `mutationFn` 是一个包含了进行变异的函数。在这里，它是一个使用 axios 发送 POST 请求的函数，成功后返回响应数据。
   - `onSuccess` 是一个回调函数，它会在变异成功时被调用。在这里，它用于更新前端缓存中的数据。

3. **`ref` 和表单提交事件：**
   - 使用 `useRef` 创建了一个 `ref` 对象，它将用于引用输入框元素。
   - 表单提交事件 (`onSubmit`) 用于处理用户提交表单的操作。
   - 当表单提交时，阻止默认行为，然后检查输入框的值，调用 `addTodo.mutate` 来触发变异。

4. **`onSuccess` 中的更新数据操作：**
   - 在 `onSuccess` 回调中，首先通过 `console.log(saveTodo)` 打印出成功添加的 Todo 项的数据。
   - `queryClient.setQueryData` 用于在缓存中更新数据。在这里，通过将新的 Todo 项添加到之前的 Todo 数组中，来实现更新。
   - 你还可以看到注释中提到的另一种更新数据的方式，即使用 `queryClient.invalidateQueries` 来使该数据无效，然后重新获取。这是 React Query 中的一种手动触发重新获取数据的方法。

总体而言，这个组件允许用户通过输入框添加新的 Todo 项，同时通过使用 React Query 中的 `useMutation` 和 `useQueryClient` 来处理数据的变异和缓存更新。



## 十.处理错误数据

```tsx
import { useMutation, useQueryClient } from "@tanstack/react-query";
import { useRef } from "react";
import { Todo } from "../hooks/useTodo";
import axios from "axios";

const TodoForm = () => {
  const queryClient = useQueryClient();   //这里需要声明类型<Todo,Error,Todo>
  const addTodo = useMutation<Todo,Error,Todo>({
    mutationFn: (todo: Todo) =>
      axios
        .post<Todo>("https://jsonplaceholder.typicode.com/todos", todo)
        .then((res) => res.data),
    onSuccess: (saveTodo, newTodo) => {
      console.log(saveTodo);
      queryClient.setQueryData<Todo[]>(["todos"], (todos) => [
        saveTodo,
        ...(todos || []),
      ]);
    },
  });
  const ref = useRef<HTMLInputElement>(null);

  return (
    <> //这里显示错误
      { addTodo.error && 
      <div className="alert alert-danger">
        {addTodo.error.message}
      </div>}
      <form
        className="row mb-3"
        onSubmit={(event) => {
          event.preventDefault();

          if (ref.current && ref.current.value)
            addTodo.mutate({
              id: 0,
              title: ref.current?.value,
              completed: false,
              userId: 1,
            });
        }}
      >
        <div className="col">
          <input ref={ref} type="text" className="form-control" />
        </div>
        <div className="col">
          <button className="btn btn-primary">Add</button>
        </div>
      </form>
    </>
  );
};

export default TodoForm;

```

## 十一.处理事件中和优化ref输入框

```tsx
import { useMutation, useQueryClient } from "@tanstack/react-query";
import { useRef } from "react";
import { Todo } from "../hooks/useTodo";
import axios from "axios";

const TodoForm = () => {
  const queryClient = useQueryClient();
  const addTodo = useMutation<Todo,Error,Todo>({
    mutationFn: (todo: Todo) =>
      axios
        .post<Todo>("https://jsonplaceholder.typicode.com/todos", todo)
        .then((res) => res.data),
    onSuccess: (saveTodo, newTodo) => {
      console.log(saveTodo);
      //更新数据,在前端上
      //方法一: 使该数据无效，重新获取
      //queryClient.invalidateQueries({
      //  queryKey: ['todos']
      //})

      //方法二:在缓存中更新数据
      queryClient.setQueryData<Todo[]>(["todos"], (todos) => [
        saveTodo,
        ...(todos || []),
      ]);

      if (ref.current) ref.current.value = ''; //清理输入框
    },
  });
  const ref = useRef<HTMLInputElement>(null);

  return (
    <>
      { addTodo.error && 
      <div className="alert alert-danger">
        {addTodo.error.message}
      </div>}
      <form
        className="row mb-3"
        onSubmit={(event) => {
          event.preventDefault();

          if (ref.current && ref.current.value)
            addTodo.mutate({
              id: 0,
              title: ref.current?.value,
              completed: false,
              userId: 1,
            });
        }}
      >
        <div className="col">
          <input ref={ref} type="text" className="form-control" />
        </div>
        <div className="col">
          <button 
          disabled ={addTodo.isLoading}
          className="btn btn-primary">
            {addTodo.isLoading ? 'Adding...':'Add'} 设置加载按钮
          </button>
        </div>
      </form>
    </>
  );
};

export default TodoForm;

```



## 十二.乐观更新

**先更新UI，再传递给后端**

```tsx
import { useMutation, useQueryClient } from "@tanstack/react-query";
import { useRef } from "react";
import { Todo } from "../hooks/useTodo";
import axios from "axios";

interface AddTodoContext {
  previousTodos: Todo[]
}

const TodoForm = () => {
  const queryClient = useQueryClient();
  const addTodo = useMutation<Todo, Error, Todo, AddTodoContext>({
    mutationFn: (todo: Todo) =>
      axios
        .post<Todo>("https://jsonplaceholder.typicode.com/todos", todo)
        .then((res) => res.data),

    onMutate: (newTodo: Todo) => {
      const previousTodos = queryClient.getQueryData<Todo[]>(['todos']) || []; 


      queryClient.setQueryData<Todo[]>(["todos"], (todos) => [
        newTodo,
        ...(todos || []),
      ]);

      if (ref.current) ref.current.value = "";
      return { previousTodos };
    },

    onSuccess: (saveTodo, newTodo) => {
      queryClient.setQueryData<Todo[]>(["todos"], (todos) =>
        todos?.map((todo) => (todo === newTodo ? saveTodo : todo))
      );
    },

    onError: (error, newTodo, context) =>{
      if (!context) return;

      queryClient.setQueryData<Todo[]>(['todos'], context.previousTodos);
    }
  });
  const ref = useRef<HTMLInputElement>(null);

  return (
    <>
      {addTodo.error && (
        <div className="alert alert-danger">{addTodo.error.message}</div>
      )}
      <form
        className="row mb-3"
        onSubmit={(event) => {
          event.preventDefault();

          if (ref.current && ref.current.value)
            addTodo.mutate({
              id: 0,
              title: ref.current?.value,
              completed: false,
              userId: 1,
            });
        }}
      >
        <div className="col">
          <input ref={ref} type="text" className="form-control" />
        </div>
        <div className="col">
          <button disabled={addTodo.isLoading} className="btn btn-primary">
            {addTodo.isLoading ? "Adding..." : "Add"}
          </button>
        </div>
      </form>
    </>
  );
};

export default TodoForm;

```

`onMutate` 方法中的操作确实已经更新了缓存。我失误地提到了 `onSuccess` 方法中使用 `map` 的目的，这是一个错误的描述。让我更正一下：

在你的代码中，`onMutate` 方法执行了以下操作：

```javascript
onMutate: (newTodo: Todo) => {
  const previousTodos = queryClient.getQueryData<Todo[]>(['todos']) || []; 

  queryClient.setQueryData<Todo[]>(["todos"], (todos) => [
    newTodo,
    ...(todos || []),
  ]);

  if (ref.current) ref.current.value = "";
  return { previousTodos };
},
```

- `queryClient.setQueryData` 更新了缓存，将 `newTodo` 添加到了缓存数据的最前面。
- `return { previousTodos };` 返回了一个包含之前缓存数据的对象。

而在 `onSuccess` 方法中，`map` 方法实际上是用于更新缓存的，确保 React Query 能够正确地重新渲染组件。在你的代码中，`onSuccess` 方法的目的是在缓存中找到先前的 `newTodo`，将其替换为从服务器返回的 `saveTodo`：

```javascript
onSuccess: (saveTodo, newTodo) => {
  queryClient.setQueryData<Todo[]>(["todos"], (todos) =>
    todos?.map((todo) => (todo === newTodo ? saveTodo : todo))
  );
},
```

这个 `map` 方法的作用是在缓存中找到先前的 `newTodo`，将其替换为从服务器返回的 `saveTodo`。这确保了在缓存中的数据更新后，React Query 能够正确地重新渲染组件。



这是一个React组件，用于添加Todo项的表单，使用了React Query中的`useMutation`和`useQueryClient`钩子。以下是对这个组件的解释：

1. **`onMutate`:**
   - `onMutate` 是 `useMutation` 中的生命周期回调函数，它在发起变异之前被调用。
   - 在这里，使用 `queryClient.getQueryData` 获取当前缓存中的 Todo 数据作为 `previousTodos`。
   - 使用 `queryClient.setQueryData` 在缓存中添加新的 Todo 项，并将其前置到已有的 Todo 数组前面。
   - 如果输入框存在，将其值清空。
   - 返回一个对象 `{ previousTodos }`，这个对象将在 `onError` 中使用。

   ```javascript
   onMutate: (newTodo: Todo) => {
     const previousTodos = queryClient.getQueryData<Todo[]>(['todos']) || [];
   
     queryClient.setQueryData<Todo[]>(["todos"], (todos) => [
       newTodo,
       ...(todos || []),
     ]);
   
     if (ref.current) ref.current.value = "";
     return { previousTodos };
   },
   ```

2. **`onSuccess`:**
   - `onSuccess` 是 `useMutation` 中的另一个生命周期回调函数，它在变异成功时被调用。
   - 在这里，使用 `queryClient.setQueryData` 更新缓存中的数据，将之前添加的虚拟 Todo 项替换为服务器返回的实际保存的 Todo 项。

   ```javascript
   onSuccess: (saveTodo, newTodo) => {
     queryClient.setQueryData<Todo[]>(["todos"], (todos) =>
       todos?.map((todo) => (todo === newTodo ? saveTodo : todo))
     );
   },
   ```

3. **`onError`:**
   - `onError` 是 `useMutation` 中的另一个生命周期回调函数，它在变异发生错误时被调用。
   - 如果 `context` 存在（即 `onMutate` 返回的对象存在），使用 `queryClient.setQueryData` 恢复到之前的 Todo 数据。

   ```javascript
   onError: (error, newTodo, context) => {
     if (!context) return;
   
     queryClient.setQueryData<Todo[]>(['todos'], context.previousTodos);
   }
   ```

这些生命周期回调函数主要用于处理在不同阶段的数据更新。`onMutate` 在发起变异前更新缓存，`onSuccess` 在变异成功时更新缓存，`onError` 在变异发生错误时回滚到之前的数据。整体而言，这个组件实现了在添加 Todo 项时使用 React Query 进行数据变异和缓存管理。



## 十三.自定义钩子

**useAddTodo.ts**

```ts
import { useMutation, useQueryClient } from "@tanstack/react-query";
import { Todo } from "./useTodo";
import axios from "axios";
import { CACHE_KEY_TODOS } from "../react-query/constans";

interface AddTodoContext {
  previousTodos: Todo[];
}

const useAddTodo = (onAdd: () => void) => {
  const queryClient = useQueryClient();
  return useMutation<Todo, Error, Todo, AddTodoContext>({
    mutationFn: (todo: Todo) =>
      axios
        .post<Todo>("https://jsonplaceholder.typicode.com/todos", todo)
        .then((res) => res.data),

    onMutate: (newTodo: Todo) => {
      const previousTodos = queryClient.getQueryData<Todo[]>(CACHE_KEY_TODOS) || [];

      queryClient.setQueryData<Todo[]>(CACHE_KEY_TODOS, (todos = []) => [
        newTodo,
        ...todos,
      ]);

      onAdd();
      
      return { previousTodos };
    },

    onSuccess: (saveTodo, newTodo) => {
      queryClient.setQueryData<Todo[]>(CACHE_KEY_TODOS, (todos) =>
        todos?.map((todo) => (todo === newTodo ? saveTodo : todo))
      );
    },

    onError: (error, newTodo, context) => {
      if (!context) return;

      queryClient.setQueryData<Todo[]>(CACHE_KEY_TODOS, context.previousTodos);
    },
  });
};

export default useAddTodo;

```

**TodoForm.tsx**

```tsx
import { useRef } from "react";
import useAddTodo from "../hooks/useAddTodo";

const TodoForm = () => {
  const ref = useRef<HTMLInputElement>(null);
  const addTodo = useAddTodo(() => {
    if (ref.current) ref.current.value = "";
  });

  return (
    <>
      {addTodo.error && (
        <div className="alert alert-danger">{addTodo.error.message}</div>
      )}
      <form
        className="row mb-3"
        onSubmit={(event) => {
          event.preventDefault();

          if (ref.current && ref.current.value)
            addTodo.mutate({
              id: 0,
              title: ref.current?.value,
              completed: false,
              userId: 1,
            });
        }}
      >
        <div className="col">
          <input ref={ref} type="text" className="form-control" />
        </div>
        <div className="col">
          <button disabled={addTodo.isLoading} className="btn btn-primary">
            {addTodo.isLoading ? "Adding..." : "Add"}
          </button>
        </div>
      </form>
    </>
  );
};

export default TodoForm;

```



## 十四.自定义apiClient

把所有请求的代码放到这个文件中 **apiClient.ts**

```tsx
import axios from "axios";

const axiosInstance = axios.create({
  baseURL: "https://jsonplaceholder.typicode.com",
});

class APIClient<T> {
  endpoint: string;

  constructor(endpoint: string) {
    this.endpoint = endpoint;
  }

  getAll = () => {
    return axiosInstance
      .get<T[]>(this.endpoint)
      .then((res) => res.data);
  }

  post = (data: T) => {
    return axiosInstance
      .post<T>(this.endpoint, data)
      .then(res => res.data);
  }
}


export default APIClient;
```



**useTodo.ts**

```ts
import { useQuery } from "@tanstack/react-query";
import { CACHE_KEY_TODOS } from "../constans";
import APIClient from "../react-query/services/apiClient";

const apiClient = new APIClient<Todo>('/todos')


export interface Todo {
  id: number;
  title: string;
  userId: number;
  completed: boolean;
}

const useTodo = () => {

  return useQuery<Todo[], Error>({
    queryKey: CACHE_KEY_TODOS,
    queryFn: apiClient.getAll,
    staleTime: 10 * 1000, //10s
  });
};

export default useTodo;

```



**useAddTodo.ts**

```ts
import { useMutation, useQueryClient } from "@tanstack/react-query";
import { Todo } from "./useTodo";
import { CACHE_KEY_TODOS } from "../constans";
import APIClient from "../react-query/services/apiClient";

const apiClient = new APIClient<Todo>("/todos");

interface AddTodoContext {
  previousTodos: Todo[];
}

const useAddTodo = (onAdd: () => void) => {
  const queryClient = useQueryClient();
  return useMutation<Todo, Error, Todo, AddTodoContext>({
    mutationFn: apiClient.post,

    onMutate: (newTodo: Todo) => {
      const previousTodos =
        queryClient.getQueryData<Todo[]>(CACHE_KEY_TODOS) || [];

      queryClient.setQueryData<Todo[]>(CACHE_KEY_TODOS, (todos = []) => [
        newTodo,
        ...todos,
      ]);

      onAdd();

      return { previousTodos };
    },

    onSuccess: (saveTodo, newTodo) => {
      queryClient.setQueryData<Todo[]>(CACHE_KEY_TODOS, (todos) =>
        todos?.map((todo) => (todo === newTodo ? saveTodo : todo))
      );
    },

    onError: (error, newTodo, context) => {
      if (!context) return;

      queryClient.setQueryData<Todo[]>(CACHE_KEY_TODOS, context.previousTodos);
    },
  });
};

export default useAddTodo;

```



## 十五.创建一个可重用的HTTP Service

**通过创建一个todoService.ts文件**

**1.储存 Todo对象定义(放到一个新文件中，让它们全部依赖这个文件)**

**2.创建类的实例(之前重复创建对象有点丑陋)**



**todoService.ts**

```ts
import APIClient from "./apiClient";

export interface Todo {
  id: number;
  title: string;
  userId: number;
  completed: boolean;
}

export default new APIClient<Todo>("/todos");
```



**useTodo.ts**

```ts
import { useQuery } from "@tanstack/react-query";
import { CACHE_KEY_TODOS } from "../constans";
import todoService, { Todo } from "../react-query/services/todoService";

const useTodo = () => {
  return useQuery<Todo[], Error>({
    queryKey: CACHE_KEY_TODOS,
    queryFn: todoService.getAll,
    staleTime: 10 * 1000, //10s
  });
};

export default useTodo;

```



**useAddTodo.ts**

```ts
import { useMutation, useQueryClient } from "@tanstack/react-query";
import { CACHE_KEY_TODOS } from "../constans";
import todoService, { Todo } from "../react-query/services/todoService";

interface AddTodoContext {
  previousTodos: Todo[];
}

const useAddTodo = (onAdd: () => void) => {
  const queryClient = useQueryClient();
  return useMutation<Todo, Error, Todo, AddTodoContext>({
    mutationFn: todoService.post,

    onMutate: (newTodo: Todo) => {
      const previousTodos =
        queryClient.getQueryData<Todo[]>(CACHE_KEY_TODOS) || [];

      queryClient.setQueryData<Todo[]>(CACHE_KEY_TODOS, (todos = []) => [
        newTodo,
        ...todos,
      ]);

      onAdd();

      return { previousTodos };
    },

    onSuccess: (saveTodo, newTodo) => {
      queryClient.setQueryData<Todo[]>(CACHE_KEY_TODOS, (todos) =>
        todos?.map((todo) => (todo === newTodo ? saveTodo : todo))
      );
    },

    onError: (error, newTodo, context) => {
      if (!context) return;

      queryClient.setQueryData<Todo[]>(CACHE_KEY_TODOS, context.previousTodos);
    },
  });
};

export default useAddTodo;

```





# 全球状态管理

# 路由