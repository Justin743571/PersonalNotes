# Next.js

## Next.js快速渲染的关键

快速呈现给用户的重点在于 Next.js 发送给浏览器的 HTML 文件已经包含了完整的页面内容，而普通的 React 应用程序发送给浏览器的是一个基本的 HTML 文件，页面内容主要依赖于客户端的 JavaScript 代码来生成。让我们详细解释一下这个区别。

### 普通 React 应用程序

1. **请求阶段**：
   
   - 用户输入域名并发送 HTTP 请求到服务器。
2. **响应阶段**：
   
   - 服务器返回一个基本的 HTML 文件，通常只包含一个根节点，比如 `<div id="root"></div>`。
   - 同时，服务器还返回了 CSS 和 JavaScript 文件。
3. **浏览器解析**：
   
   - 浏览器下载并解析这个基本的 HTML 文件，但此时页面内容是空的。
4. **JavaScript 执行**：
   - 浏览器下载并执行 React 应用程序的 JavaScript 文件。
   - JavaScript 文件通过 React 的客户端渲染（Client-Side Rendering, CSR）生成和操作 DOM，填充页面内容。
5. **页面渲染**：
   
   - React 在客户端生成完整的 DOM 树，用户才能看到完整的页面内容。
   
   **关键问题**：页面内容的生成依赖于 JavaScript 的执行，因此用户需要等待浏览器下载并执行 JavaScript 代码才能看到页面内容。

### Next.js 应用程序

1. **请求阶段**：
   - 用户输入域名并发送 HTTP 请求到服务器。
2. **响应阶段**：
   - 服务器返回一个预渲染的 HTML 文件，这个文件已经包含了完整的页面内容。
   - 同时，服务器还返回了 CSS 和 JavaScript 文件。
3. **浏览器解析**：
   - 浏览器下载并解析这个预渲染的 HTML 文件，生成 DOM 树。
   - 因为 HTML 文件已经包含了页面的所有静态内容，用户几乎立即可以看到完整的页面。
4. **JavaScript 执行**：
   - 浏览器下载并执行必要的 JavaScript 文件，以使页面具有交互性（如事件处理）。
   - 进行 “hydration” 过程，将 React 的事件绑定等动态行为注入到已有的 DOM 节点中。
5. **页面渲染**：
   - 用户在页面加载初期就能看到完整的页面内容，并且随着 JavaScript 的执行，页面变得可交互。

   **关键优势**：因为 HTML 文件已经包含了完整的页面内容，所以浏览器不需要等待 JavaScript 的执行来生成页面内容，用户可以更快地看到完整的页面。

### 总结

- **普通 React 应用程序**：页面内容依赖于客户端 JavaScript 的执行，用户在看到完整页面内容之前，需要等待浏览器下载并执行 JavaScript 代码。这可能会导致初始加载时间较长，尤其在网络较慢或设备性能较低的情况下。
  
- **Next.js 应用程序**：预渲染的 HTML 文件已经包含了完整的页面内容，浏览器可以立即解析和渲染页面，用户几乎立即可以看到完整的页面内容。随后执行的 JavaScript 文件使页面具有交互性。这样大大提高了初始加载速度和用户体验。

这个区别是 Next.js 能够快速呈现页面内容并提供优良用户体验的关键所在。

## 一个客户端组件的初始呈现是在服务器上预呈现的

在Next.js中，一个客户端组件的初始呈现确实是在服务器上预呈现的。这是Next.js框架的一个关键特性之一，即它结合了服务器端渲染（SSR）和客户端渲染（CSR）来优化应用的性能和用户体验。

### 具体流程解释

1. **服务器端渲染（SSR）**：
   - 当用户首次访问一个页面时，Next.js会在服务器上渲染该页面的初始HTML。这包括所有需要的组件，无论是服务器组件还是客户端组件。
   - 服务器生成的HTML发送到客户端，使得用户能够立即看到页面内容，而不需要等待所有JavaScript代码的下载和执行。
   - 在这个阶段，即使是客户端组件，它们的初始HTML也会在服务器上生成。

2. **客户端接管（Hydration）**：
   - 当客户端接收到服务器发送的HTML后，浏览器会下载并执行JavaScript代码。
   - React会“接管”这个预先渲染的HTML，并使其变为可交互的（hydration过程）。
   - 此时，客户端组件将开始在浏览器中执行其JavaScript逻辑，例如事件处理等。

### 客户端组件的初始呈现
即使是标记为客户端组件的部分，它们的初始HTML也是在服务器上生成的。这种机制的优点包括：

- **更快的初始加载**：用户能够快速看到页面内容，而不需要等待JavaScript的执行。
- **SEO友好**：搜索引擎爬虫能够更好地索引页面内容，因为它们看到的是完全渲染的HTML。

### 总结
- **初始呈现**：在服务器上完成，包括客户端组件的HTML生成。
- **客户端接管**：在浏览器中完成，使页面变为可交互的。

这就是Next.js通过服务器端渲染和客户端接管相结合的方式，来提供更快的页面加载速度和更好的用户体验的原因。



## Next.js的Node.js runtime

Next.js 是一个基于 React 的框架，它在 Node.js 环境中运行。**Next.js 的 Node.js runtime 提供了一些强大的功能**，使开发者能够构建高性能、SEO 友好的 Web 应用程序。以下是 Next.js 中 Node.js runtime 的一些关键特点和功能：

### 1. **服务器端渲染（SSR）**

Next.js 最显著的特点之一是其支持服务器端渲染。这意味着在用户请求页面时，服务器会先渲染页面并将 HTML 发送到客户端。这样可以提高页面加载速度和 SEO 性能。

### 2. **静态站点生成（SSG）**

Next.js 还支持静态站点生成，在构建时生成静态 HTML 文件，适用于内容不经常变化的页面。这种方法可以显著提高性能和缩短页面加载时间。

### 3. **API Routes**

Next.js 允许你在同一框架中创建 API 端点。这使得你可以轻松地创建后端逻辑并与前端组件共享代码。

### 4. **动态路由**

Next.js 支持动态路由，可以根据 URL 参数渲染不同的页面内容。

### 5. **中间件**

Next.js 支持中间件，使你可以在请求到达页面之前处理请求。你可以用中间件进行认证、日志记录、重定向等操作。

### 6. **构建优化**

Next.js 自动进行代码拆分、预加载和优化，这些功能使应用程序在生产环境中运行得更快。

### 7. **自定义服务器**

你可以使用 Node.js 自定义 Next.js 服务器以满足特定需求，比如在 Express.js 中集成 Next.js。

总的来说，Next.js 中的 Node.js runtime 提供了强大的功能，使开发者能够创建高性能、现代化的 Web 应用程序，既可以在服务器端渲染，也可以生成静态站点，还可以轻松创建 API。







## 缓存

在 Next.js 中，缓存机制是一个关键的性能优化手段，帮助加快页面加载速度和减少服务器负载。下面是对三种缓存的详细介绍：

### 1.  Data Cache

**Data Cache** 指的是对通过数据获取方法（如 fetch()）获取的数据进行缓存。缓存在data cache里面，不会向服务器不会发送http获得新数据



### 2. Full Route Cache


在 Next.js 中，路由可以是**静态路由或动态路由。**

#### 静态路由页面

在 Next.js 中，静态路由页面通常是通过静态生成 (Static Generation, SSG) 方式预渲染的。这意味着在构建时（即 `next build` 时），这些页面会被生成并储存在服务器的文件系统中。具体步骤如下：

1. **构建时预渲染**：Next.js 会在构建时预先生成所有静态路由页面，并将生成的 HTML 文件存储在服务器的文件系统中。
2. **用户请求**：当用户请求一个静态页面时，服务器会直接将存储的 HTML 文件发送给用户，而不需要再次生成页面。这种方式极大地提高了页面的加载速度和性能，因为不需要每次请求都进行计算和生成。

#### 动态路由页面

对于动态路由页面，Next.js 提供了多种数据获取方法，常用的有以下几种：

1. **服务器端渲染 (Server-Side Rendering, SSR)**：
   
   - 每次用户请求动态路由页面时，服务器会运行页面的代码（包括数据获取逻辑），生成最新的 HTML 并发送给用户。
   - 这种方式保证了页面数据的实时性，但每次请求都需要服务器计算生成，可能会比静态页面稍慢。
   
2. **增量静态生成 (ISR)**
   
   ISR 使你能够在构建时生成静态页面，并允许你定义一个时间间隔，在这个时间间隔后重新生成这些页面，以确保它们包含最新的数据。这种机制结合了静态生成的高性能和服务器端渲染的数据实时性。

   ##### 工作流程
   
   1. **初次生成和缓存**：
      - 在你构建 Next.js 应用时（通过 `next build`），ISR 会生成一些静态页面，并将这些页面存储在服务器的文件系统中。
      - 当用户首次请求这些页面时，Next.js 会直接返回生成好的静态 HTML 页面，这些页面的生成时间是非常快的，因为它们已经预先生成好了。
   2. **设定重新生成间隔**：
      - 你可以在页面的 `getStaticProps` 函数中设置 `revalidate` 参数，以指定页面重新生成的时间间隔（以秒为单位）。
      - 例如，`revalidate: 60` 表示这个页面会在第一次生成后的 60 秒内保持静态内容。60 秒之后，页面将被重新生成。
   3. **重新生成**：
      - 在设定的重新生成间隔过后，当有新的请求到达时，Next.js 会在后台异步地重新生成该页面。
      - 在后台重新生成页面的过程中，用户仍然会看到之前缓存的页面，不会有任何延迟。
      - 一旦重新生成完成，缓存中的页面将被更新，后续的请求将获取最新的页面内容。
   
3. **客户端渲染 (Client-Side Rendering, CSR)**：
   - 页面初次加载时只是一个基本的 HTML 框架，实际数据通过 JavaScript 在客户端获取和渲染。这种方式适合需要频繁更新或与用户交互较多的页面。

#### 总结

- **静态路由页面**：在构建时预渲染并储存在服务器文件系统中，用户请求时直接提供预生成的 HTML 文件。
- **动态路由页面**：
  - **SSR**：每次请求时生成最新的 HTML 页面。
  - **ISR**：初次生成页面后缓存，定期重新生成和更新缓存。
  - **CSR**：初次加载时在客户端获取和渲染数据。

根据项目需求选择合适的渲染方式，可以在性能和实时性之间取得平衡。





###  3. Client-side Cache(Router Cache)

#### 此缓存用于储存页面的有效负载

**为了给用户更好的体验，当用户在应用程序中导航时，next.js路由器自动存储页面的输出，下次用户返回到他们上一次已经访问过的页面时，next.js不会向后端发送请求，它将从Client-side Cache返回结果**

**这个Client-side Cache持续一个会话，当我们刷新它会重新加载新会话**

**Client-side Cache也有自动失效期，如静态页面5分钟，动态页面30秒**

**我们可以强制刷新来获取新数据**

 

## 静态路由缓存解决方案

对于静态路由的页面，我们可以告诉next.js让这个页面退出静态呈现   具体操作为在该页面下写下面代码

```tsx
export const dynamic = "force-dynamic";
```

然后如果是提交后，由于有客户端缓存，需要用户重新刷新页面，才可以看到最新数据，所以需要在提交里面去使用到刷新方法

这里需要Next.js中的useRouter()方法

```tsx
router.refresh()
```



## 下载daisyUI

配置文件





## 特殊文件

page.tsx 主要显示HTML页面，只有这个文件可公开访问

layout.tsx 布局文件

loading.tsx 显示加载文件

route.tsx  创建API的路由文件

not-found.tsx  显示找不到页面的页面，可以自定义错误

error.tsx  显示一般自定义错误页面



## 路由和导航

在App路由器文件夹中，可以通过文件夹来定义路由(前提为有特定文件page.tsx)在一个文件夹中只有page.tsx文件公开，其他文件不公开

路由可以嵌套，以文件夹的形式来实现

使用next自带的Link组件来导航 



### 客户端组件和服务器组件

在next.js中有两种组件**服务器组件**和**客户端组件**

#### 服务器组件有很多好处

对搜索引擎友好，引擎可以看到HTML文件构成，可以定义索引

对客户端用户友好，在服务器渲染html，这样就不用在用户电脑进行渲染，和加快网页呈现

#### 服务器组件坏处

没有互动性（点击，onChange，onSubmit）

不能使用一些钩子如{useState(),useEffect()... }

不能使用 浏览器API 



#### 一般在现实项目中，我们需要将互动性组件设置成客户端组件

默认情况下App文件夹下都是服务器组件

对比旧的page路由器系统中的组件都不是服务器组件，App路由器系统的所以组件都是服务器组件





#### 把服务器组件变成客户端组件

在文件中最顶端加入'use client'命令

```
'use client'
```





#### 对于一些需要使用到use client 的组件，我们可以把他们抽离出来，我们把他设置成为一个单独的组件，来优化项目

​	



### 获取数据 fetch()

在服务器中获取数据比在客户端获取数据有很多很多好处

**所以获取数据尽量在服务器组件上获取它**



```tsx
import React, { use } from "react";

interface User {
  id: number;
  name: string;
}

const UserPage = async () => {
  const res = await fetch("https://jsonplaceholder.typicode.com/users");
  const users: User[] = await res.json();
  return (
    <>
      <h1>Users</h1>
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </>
  );
};

export default UserPage;

```



### 缓存

**next.js内置数据缓存**

```tsx
import React, { use } from "react";

interface User {
  id: number;
  name: string;
}

const UserPage = async () => {
  const res = await fetch(
    "https://jsonplaceholder.typicode.com/users",
    { next: { revalidate: 10}});//10秒重新获取数据
                               //{ cache:'no-store'} 禁止缓存
  const users: User[] = await res.json();
  return (
    <>
      <h1>Users</h1>
      <ul>
        {users.map((user) => (
          <li key={user.id}>{user.name}</li>
        ))}
      </ul>
    </>
  );
};

export default UserPage;

```

#### 此缓存行为仅在fetch函数中实现

类似于使用第三方包axios获取数据不会得到缓存





### 静态渲染和动态渲染

在next.js中，如果在获取数据时，使用了缓存，文件都会被视为静态文件，数据储存在缓存中，不会再向服务器获取数据

如果在获取数据时，禁止了缓存，在请求数据时，会提供最新数据



### 动态路由

文件结构 /app/users/[id]

下面是[id]文件夹下的page.tsx文件

```tsx
import React from 'react'

interface Props {
    params: { id : number}
}

const UserDetailPage = ( {params:{id}}: Props) => {
  return (
    <div>UserDetailPage {id}</div>
  )
}

export default UserDetailPage
```

**在 Next.js 中，动态路由的参数会作为组件的 props 传递给页面组件。对于动态路由页面，如果路径中包含动态参数（比如 `/app/users/[id]` 中的 `[id]`），那么 Next.js 会自动将匹配的参数传递给页面组件。**

**`params` 对象是在 Next.js 中自动生成的，其中包含了路由中动态参数的值。所以，只有当路由中包含动态参数时，`params` 对象才会存在，并且包含相应的动态参数值。在这种情况下，我们可以通过解构 `params` 对象来获取动态参数的值，例如 `id` 属性。**

因此，为了得到 `id` 属性，确保你的路由是动态路由，并且在路径中包含相应的动态参数。如果路径中没有动态参数，那么 `params` 对象可能不存在，从而无法获取 `id` 属性。



### 全面覆盖的分段

**一条路线中使用不同数量的参数(类似于: /products/grocery/dairy/milk)**



该文件结构为/app/products/[...slug]

```tsx
import React from 'react'

interface Props {
    params: { slug: string[]}
}


const ProductPage = ({params:{slug}}: Props) => {
  return (
    <div>ProductPage {slug}</div>
  )
}

export default ProductPage
```



如果我们访问/app/products该页面会找不到,是由于我们没创建products文件夹的page.tsx文件，如果我们不想创建，但是为了显示该参数可以为空，可以把[...slug]路由参数设置为可选，我们应该把它包在两个括号里[[..slug]]，这样就可以访问了





### 访问查询字符串参数

我们想访问**http://localhost:3000/products?sortOrder=name**

我们想通过点击Name,Email来排序并且当点击页面上的Name或Email时

我们把url跳转**products?sortOrder=(参数)**

排序需要用到fast-sort第三方包

```
npm i fast-sort
```



#### UserTable.tsx

```tsx
import { sort } from "fast-sort";
import Link from "next/link";
import React from "react";

interface User {
  id: number;
  name: string;
  email: string;
}

interface Props {
  sortOrder: string;
}

const UserTable = async ({ sortOrder }: Props) => {
  const res = await fetch("https://jsonplaceholder.typicode.com/users", {
    next: { revalidate: 10 },
  });
  const users: User[] = await res.json();

  const sortedUsers = sort(users).asc(
    sortOrder === "email" ? (user) => user.email : (user) => user.name
  );

  return (
    <table className="table table-bordered">
      <thead>
        <tr>
          <th>
            <Link href="/users?sortOrder=name">Name</Link>
          </th>
          <th>
            <Link href="/users?sortOrder=email">Email</Link>
          </th>
        </tr>
      </thead>
      <tbody>
        {sortedUsers.map((user) => (
          <tr key={user.id}>
            <td>{user.name}</td>
            <td>{user.email}</td>
          </tr>
        ))}
      </tbody>
    </table>
  );
};

export default UserTable;

```

#### page.tsx

```tsx
import React, { use } from "react";
import UserTable from "./UserTable";

interface Props {
  searchParams:{sortOrder:string}
}

const UserPage = async ({searchParams:{sortOrder}}: Props) => {
  return (
    <>
      <h1>Users</h1>
      <UserTable sortOrder={sortOrder}/>
    </>
  );
};

export default UserPage;

```





### 布局

#### /App/admin文件夹下

**layout.tsx**

这里创建一个接口定义布局，children就是该路由下的page文件

```tsx
import React, { ReactNode } from 'react'

interface Props{
    children: ReactNode
}

const AdminLayout = ({children}: Props) => {
  return (
    <div className='flex'>
        <aside className='bg-slate-200 p-5 mr-5'>Admin Sidebar</aside>
        <div>{children}</div>
    </div>
  )
}

export default AdminLayout
```

page.tsx

```tsx
import React from 'react'

const AdminHomePage = () => {
  return (
    <div>Admin HomePage</div>
  )
}

export default AdminHomePage
```



#### 在根布局中定义导航栏

**NavBar.tsx**

```tsx
import Link from 'next/link'
import React from 'react'

const NavBar = () => {
  return (
    <div className='flex bg-slate-200 p-5'>
        <Link href='/' className='mr-5'>Next.js</Link>
        <Link href='/users'>Users</Link>
    </div>
  )
}

export default NavBar
```



**根布局 layout.tsx**

```tsx
import "./globals.css";
import type { Metadata } from "next";
import { Inter } from "next/font/google";
import NavBar from "./NavBar";

const inter = Inter({ subsets: ["latin"] });

export const metadata: Metadata = {
  title: "Create Next App",
  description: "Generated by create next app",
};

export default function RootLayout({
  children,
}: {
  children: React.ReactNode;
}) {
  return (
    <html lang="en" data-theme="winter">
      <body className={inter.className}>
        <NavBar />
        <main className="p-5">{children}</main>
      </body>
    </html>
  );
}

```





**在使用TailwindCSS框架时，基本元素被该的不喜欢了可以重新更改**

**在全局css文件中改 globals.css**

```css
@tailwind base;
@tailwind components;
@tailwind utilities;

:root {
  --foreground-rgb: 0, 0, 0;
}

@media (prefers-color-scheme: dark) {
  :root {
    --foreground-rgb: 255, 255, 255;
  }
}

body {
  color: rgb(var(--foreground-rgb));
}

//下面是改的h1标题
@layer base {
  h1 {
    @apply font-extrabold text-2xl mb-3;
  }
}
```







### Link组件

#### 1.只下载目标页面的内容

#### 2.预取视口页面  

**预取功能的工作原理**

- **预取条件**：Next.js 中的 `<Link>` 组件默认会预取即将进入视口的链接页面（即那些用户可能会点击的链接），以提升导航速度和用户体验。但它并不是预取视口内所有页面，而是预取这些链接指向的页面。
- **预取的页面**：预取会下载该链接指向的页面的 JavaScript 和数据，以便用户点击该链接时，页面能够立即展示。这会减少用户在导航时的等待时间。

#### 3.预取的页面会缓存在客户端

预取的页面代码会被缓存到客户端，以便在用户点击链接时能够快速展示页面。这种缓存机制提高了导航性能，但需要注意的是，缓存的内容主要是页面的 JavaScript 代码，而不是具体的数据。



### 程序化导航

#### 有时我们需要把用户带到一个新页面，由于是单击按钮或提交表单，这被称为程序化导航

#### /users/new

**page.tsx**

```tsx
'use client'
import { useRouter } from 'next/navigation'
import React from 'react'

const NewUserPage = () => {
  const router = useRouter()
  return (
    <button className='btn btn-primary' onClick={() => router.push('/users')}>Create</button>
  )
}

export default NewUserPage
```

**这里使用了useRouter()钩子来处理客户端组件的点击跳转**



### 显示加载UI

#### Suspense组件显示加载

```tsx
import React, { Suspense, use } from "react";
import UserTable from "./UserTable";
import Link from "next/link";

interface Props {
  searchParams:{sortOrder:string}
}

const UserPage = async ({searchParams:{sortOrder}}: Props) => {
  return (
    <>
      <h1>Users</h1>
      <Link href='/users/new' className="btn">NEW USER</Link>
      <Suspense fallback={<p>Loading...</p>}>//加载时显示字Loading...
      <UserTable sortOrder={sortOrder}/>
      </Suspense>
    </>
  );
};

export default UserPage;

```

#### 特殊文件显示加载 loading.tsx

```tsx
import React from 'react'

const Loading = () => {
  return (
    <span className="loading loading-spinner loading-md"></span>
  )
}

export default Loading
```





### 处理not-found错误

#### 创建not-found.tsx特殊文件

```tsx
import React from 'react'

const NotFoundPage = () => {
  return (
    <div>该页面不存在</div>
  )
}

export default NotFoundPage
```



#### 处理一般普遍错误

#### 创建特殊文件error.tsx

**该文件还得是客户端组件**

```tsx
'use client'
import React from 'react'

interface Props{
    error: Error,
    reset: () => void
}

const ErrorPage = ({error,reset}: Props) => {
    console.log('Error',error)

  return (
    <>
    <div>一个不期待的错误发生了</div>
    <button className='btn' onClick={() => reset()}>重试</button>
    </>
  )
}

export default ErrorPage
```

**在该文件中，我们无法捕获根布局中发生的错误，需要global-error文件来捕获**





## 创建API

**在给定的文件夹或URL中，只允许出现一个page文件或route文件，不能两者兼有**

**route.tsx文件是用来处理http请求，比如:GET POST PUT DELETE**



### 创建一个API端点来获取对象集合

#### /App/api/users

**route.tsx**

```tsx
import { NextRequest, NextResponse } from "next/server";


export function GET(request:NextRequest){
    return NextResponse.json([
        { id:1, name: 'Mosh'},
        { id:2, name: 'John'},
    ])
}
```

**这里添加了一个request参数是为了不让next.js缓存此数据，**

**如果缓存了Next.js不会再获取数据了，该数据就是死的了，无法获取最新数据**





### 获取单一对象

```tsx
import { NextRequest, NextResponse } from "next/server";


export function GET(
  request: NextRequest,
  { params }: { params: { id: number } }
) {
  if (params.id > 10)
    return NextResponse.json({ error: "这个用户不存在" }, { status: 404 });
  return NextResponse.json({ id: 1, name: "Mosh" });
}


```



### 创建一个对象

```tsx
import { NextRequest, NextResponse } from "next/server";

export function GET(request: NextRequest) {
  return NextResponse.json([
    { id: 1, name: "Mosh" },
    { id: 2, name: "John" },
  ]);
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  if (!body.name)
    return NextResponse.json({ error: "用户名是必填项" }, { status: 400 });
  return NextResponse.json({ id: 1, name: body.name },{status:201});
}

```



### 更新一个对象

```tsx
import { NextRequest, NextResponse } from "next/server";

export function GET(
  request: NextRequest,
  { params }: { params: { id: number } }
) {
  if (params.id > 10)
    return NextResponse.json({ error: "这个用户不存在" }, { status: 404 });
  return NextResponse.json({ id: 1, name: "Mosh" });
}

export async function PUT(
    request: NextRequest,
  { params }: { params: { id: number } }
){
    const body = await request.json()
    if (!body.name) return NextResponse.json({error: '用户为必填项'},{status:400})
    
    if (params.id>10) return NextResponse.json({error:'用户不存在'},{status:404})

    return NextResponse.json({id:1,name:body.name})
    
}
```



### 删除一个对象

```tsx
export function DELETE(
    request: NextRequest,
    { params }: { params: { id: number } }
){
    if (params.id>10) return NextResponse.json({error:'用户不存在'},{status:404})
    
    return NextResponse.json({})
}
```



### 使用Zod来验证请求

下载Zod

```
npm i Zod
```

定义对象类型和约束

**schema.ts**

```ts
import { z } from "zod";


const schema = z.object({
    name:z.string().min(3),
})

export default schema
```

**router.tsx**

```tsx
import { NextRequest, NextResponse } from "next/server";
import schema from "./schema";

export function GET(request: NextRequest) {
  return NextResponse.json([
    { id: 1, name: "Mosh" },
    { id: 2, name: "John" },
  ]);
}

export async function POST(request: NextRequest) {
  const body = await request.json();
  const validation=schema.safeParse(body)
  if (!validation.success)
    return NextResponse.json(validation.error.errors, { status: 400 });
  return NextResponse.json({ id: 1, name: body.name },{status:201});
}

```





## 数据库集成

### 配置prisma

下载prisma插件和prisma包

```
npm i prisma
```

初始化prisma到App中

```
npx prisma init
```

配置.env 和schema.prisma文件



### 定义数据模型

**定义模型需要再schema.prisma文件中定义**

```mysql

model User {
  id        Int     @id @default(autoincrement())
  email     String  @unique
  name      String
  followers Int     @default(0)
  isActive  Boolean @default(true)
}

```



```
npx prisma format  //自动排版命令
```





### 创建迁移

**创建迁移与数据库同步**

```
npx prisma migrate dev
```





### 创建一个prisma客户端

为了使用我们的数据库，我们需要创建一个prisma客户端

我们只需要一个prisma客户端实例，所以需要访问prisma部分代码写上去

```ts
import { PrismaClient } from '@prisma/client'

const prismaClientSingleton = () => {
  return new PrismaClient()
}

declare global {
  var prismaGlobal: undefined | ReturnType<typeof prismaClientSingleton>
}

const prisma = globalThis.prismaGlobal ?? prismaClientSingleton()

export default prisma

if (process.env.NODE_ENV !== 'production') globalThis.prismaGlobal = prisma
```





### 获取数据

```tsx
import { NextRequest, NextResponse } from "next/server";
import schema from "./schema";
import prisma from "@/prisma/client";

export async function GET(request: NextRequest) {
  const users = await prisma.user.findMany()
  return NextResponse.json(users);
}

```



```tsx
import { NextRequest, NextResponse } from "next/server";
import schema from "../schema";
import prisma from "@/prisma/client";

export async function GET(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const user = await prisma.user.findUnique({
    where: { id: parseInt(params.id) },
  });

  if (!user)
    return NextResponse.json({ error: "这个用户不存在" }, { status: 404 });
  return NextResponse.json(user);
}

```





### 创建数据

```tsx
export async function POST(request: NextRequest) {
  const body = await request.json();
  const validation = schema.safeParse(body);
  if (!validation.success)
    return NextResponse.json(validation.error.errors, { status: 400 });
    //判断用户是否存在
  const user = await prisma.user.findUnique({
    where: {
      email: body.email,
    },
  });
  if (user)
    return NextResponse.json({ error: "该用户已经存在" }, { status: 400 });
  //创建新用户
  const newUser = await prisma.user.create({
    data: {
      name: body.name,
      email: body.email,
    },
  });
  return NextResponse.json(newUser, { status: 201 });
}

```





### 更新数据

```tsx
export async function PUT(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const body = await request.json();
  const validation = schema.safeParse(body);
  if (!validation.success)
    return NextResponse.json(validation.error.errors, { status: 400 });

  const user = await prisma.user.findUnique({
    where: { id: parseInt(params.id) },
  });
  if (!user) return NextResponse.json({ error: "用户不存在" }, { status: 404 });

  const updatedUser = await prisma.user.update({
    where: { id: user.id },
    data: {
      name: body.name,
      email: body.email,
    },
  });

  return NextResponse.json(updatedUser);
}

```





### 删除数据

```tsx
export async function DELETE(
  request: NextRequest,
  { params }: { params: { id: string } }
) {
  const user = await prisma.user.findUnique({
    where: { id: parseInt(params.id) },
  });
  if (!user) return NextResponse.json({ error: "用户不存在" }, { status: 404 });

  await prisma.user.delete({
    where: { id: user.id },
  });

  return NextResponse.json({});
}

```







## 上传文件

**储存用户上传的文件我们必须用到云平台**

这里我们需要用到 **Cloudinary** 云平台



我们需要用到该库的组件

它将投入到我们项目中上传和查看文件

```
npm i next-cloudinary
```

配置文件



### 上传文件

#### /app/upload

**page.tsx**

```tsx
'use client'
import { CldUploadWidget } from "next-cloudinary";
import React from "react";

const UploadPage = () => {
  return (
    <CldUploadWidget uploadPreset="biipclzo">
      {({ open }) => (
        <button className="btn btn-primary" onClick={() => open()}>
          Upload
        </button>
      )}
    </CldUploadWidget>
  );
};

export default UploadPage;

```



### 显示上传图片

```tsx
"use client";
import { CldImage, CldUploadWidget } from "next-cloudinary";
import React, { useState } from "react";

interface CloudinaryResult {
  public_id: string;
}

const UploadPage = () => {
  const [publicId, setPuclicId] = useState("");

  return (
    <>
      {publicId && (
        <CldImage src={publicId} alt="woman" width={270} height={180} />
      )}
      <CldUploadWidget
        uploadPreset="biipclzo"
        onUpload={(result, widget) => {
          if (result.event !== "success") return;
          const info = result.info as CloudinaryResult;
          setPuclicId(info.public_id);
        }}
      >
        {({ open }) => (
          <button className="btn btn-primary" onClick={() => open()}>
            Upload
          </button>
        )}
      </CldUploadWidget>
    </>
  );
};

export default UploadPage;

```









## 认证

身份认证会话是在网络应用程序中管理用户身份认证状态的一种机制。它通常包括以下几个重要组件：

1. **认证（Authentication）**：认证是确认用户身份的过程，通常涉及用户提供凭据（例如用户名和密码）以验证其身份。认证成功后，系统会颁发一个令牌或会话标识符，用于标识该用户。

2. **会话（Session）**：会话是在用户与应用程序之间建立的一种持久连接，用于存储关于用户身份和其他相关信息的状态。会话通常在服务器端存储，并且会分配一个唯一的会话标识符给每个用户。在会话中，用户的身份认证状态、权限和其他用户相关的信息都可以被记录和跟踪。

3. **令牌（Token）**：令牌是一种轻量级的身份验证机制，用于在客户端和服务器之间传递身份认证信息。令牌可以是短期的（如访问令牌），也可以是长期的（如刷新令牌）。通过使用令牌，应用程序可以避免在每个请求中发送用户的凭据，而只需发送一个令牌。

4. **持久性和过期性**：会话可以是持久性的（在一段时间内保持有效）或是临时性的（仅在用户关闭浏览器后失效）。同样，令牌也可以设置过期时间，以保证安全性。

身份认证会话的工作流程通常如下：

- 用户进行身份认证，提供凭据进行验证。
- 如果认证成功，服务器为用户创建一个会话，并返回会话标识符给客户端。
- 客户端在后续的请求中携带会话标识符。
- 服务器验证会话标识符，以确定用户的身份和权限。
- 如果会话有效且用户有权限访问请求的资源，服务器则处理请求。

身份认证会话是许多网络应用程序中常见的一种用户身份管理机制，它提供了一种安全、方便的方式来管理用户的登录状态和权限。

### 配置next-auth

```
npm install next-auth
```

配置文件

**看视频**



### 配置Googel Provider

**看视频**



### 身份认证会话

当用户登录时，NextAuth为该用户创建身份验证会话，该会话表示为JSON Web令牌





### 访问客户端上的Session







### 访问服务器上的Session





### 注销用户

```tsx
'use client'
import { useSession } from "next-auth/react";
import Link from "next/link";
import React from "react";

const NavBar = () => {
  const { status, data: session } = useSession();
  return (
    <div className="flex bg-slate-200 p-5 space-x-3">
      <Link href="/" className="mr-5">
        Next.js
      </Link>
      <Link href="/users">Users</Link>
      {status === "authenticated" && 
      <div>
        {session.user!.name}
        <Link href='api/auth/signout' className="ml-3">Sign Out</Link>//
      </div>
      }
      {status === "unauthenticated" && (
        <Link href="/api/auth/signin">Login</Link>
      )}
    </div>
  );
};

export default NavBar;
```

**'api/auth/signout'这是next auth处理的一个端点**



### 保护路由

**使用特殊文件middleware.ts**



```ts
import middleware from "next-auth/middleware";

export default middleware;

export const config = {
  // *: zero or more
  // +: one or more
  // ?: zero or one
  matcher: ["/users/:id*"], //禁止的URL，需要登录才可以访问
};

```

这段代码是一个 Next.js 中使用的中间件，用于身份认证，通常与 NextAuth.js 库一起使用。让我逐行解释：

1. `import middleware from "next-auth/middleware";`：这一行代码导入了 NextAuth.js 提供的中间件模块。

2. `export default middleware;`：这一行代码导出了导入的中间件，默认导出。

3. `export const config = { ... }`：这一行代码定义了一个名为 `config` 的常量对象，其中包含中间件的配置选项。

4. `matcher: ["/users/:id*"]`：这里指定了中间件的匹配规则。`"/users/:id*"` 是一个路由匹配模式，用于匹配所有 `/users/:id` 及其子路径的请求。其中，`:id*` 表示匹配任意 `id` 参数值，而 `*` 表示匹配任意子路径。换句话说，这个中间件将会拦截所有 `/users/:id` 及其子路径的请求，以便进行身份认证处理。

该中间件的作用是在访问指定路由时对用户进行身份认证，确保用户已登录或具有所需的访问权限。





### 数据适配器

当用户登录我们应用程序时，我们需要将用户储存在数据库中





### 凭证登录

使用用户名，密码登录应用程序

#### /api/auth/[...nextauth]

**route.ts**



### 用户注册

实现用户注册，需要先创建一个端点，此端点将由呈现表单的客户端组件调用

#### /api/register 

**route.ts**





## 发送邮件

### 设置 React Email

```
npm i react-email @react-email/components
```

添加预览email工具 



### 创建一个Email Template





### 预览Emails

```
npm run preview-email
```





### 样式Emails

```tsx
import {
  Body,
  Tailwind,
  Container,
  Html,
  Link,
  Preview,
  Text,
} from "@react-email/components";
import React from "react";

const WelcomeTemplate = ({ name }: { name: string }) => {
  return (
    <Html>
      <Preview>Welcome aboard!</Preview>
      <Tailwind>
        <Body className="bg-white">
          <Container>
            <Text className="font-bold text-3xl">Hello {name}</Text>
            <Link href="https://codewithmosh.com">www.codewithmosh.com</Link>
          </Container>
        </Body>
      </Tailwind>
    </Html>
  );
};

export default WelcomeTemplate;

```



### 发送电子邮件

利用不同的电子邮件服务提供商，使用 React 发送电子邮件

可以在react-email网站中找集成来实现发送电子邮件





## 优化

### 优化图片

#### 显示本地图片

```tsx
import Image from "next/image";
import woman from "@/public/images/woman.jpg"   

export default async function Home() {
  
  return (
    <main>
      <Image src={woman} alt="Woman"></Image>
    </main>
  );
}

```

#### 显示远程图片

```tsx
import Image from "next/image";

export default async function Home() {
  return (
    <main>
      <Image
        src="https://bit.ly/react-cover"
        alt=""
        fill
        className="object-cover"
        sizes="(max-width: 480px) 100vw, (max-width:768px) 50vw, 33vw"
        quality={100}
        priority
      ></Image>
    </main>
  );
}

```



### 与第三方服务集成





### 字体



### 搜索引擎优化

 



### 惰性加载

在 Next.js 中，Lazy Loading 是一种优化技术，可以帮助提高网站或应用程序的性能。Lazy Loading 的核心思想是延迟加载（也称为惰性加载）组件或模块，只有当其在视口中或用户需要时才会被加载，而不是一次性加载所有内容。

延迟加载是将来**加载客户端组件或第三方库**的一种策略





## 部署













