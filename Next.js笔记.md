# Next.js

next.js是React库的框架

1.服务器渲染

2.快速创建路由

3.有热模块

..................





## 关于Full Route Cache


在 Next.js 中，路由可以是**静态路由或动态路由。**

- **静态路由**：指的是路由没有任何参数，例如 `/about`。这些路由会在构建时预渲染，并且生成静态 HTML 文件，用户访问时直接获取这些文件，不依赖于动态数据加载或服务器端渲染。
- **动态路由**：指的是带有参数的路由，例如 `/posts/[id]`，其中 `[id]` 是一个参数。动态路由可以根据不同的参数值动态生成页面内容。这些页面可以在服务器端渲染时动态生成，也可以在客户端根据路由参数进行加载。

#### 所以，当提到没有参数的路由被视为静态路由时，这意味着这些路由不包含动态参数，而是作为静态页面在构建时被预渲染。而带有参数的路由则被视为动态路由，可以根据不同的参数值来生成页面内容。



### 没有参数的路由将会被视为静态路由。这意味着这些路由将被 Next.js 预渲染，并且不依赖于动态数据加载或服务器端渲染。



##  关于Client Cache

#### 客户端缓存有Session,其中的自动失效期会导致再向服务器获取数据

### 静态路由页面的自动失效期可能为5分钟

### 而动态路由页面的自动失效期可能为30秒

#### 当用户在动态路由的页面中创建数据后，在一定的时间内（比如30秒），除非刷新页面或者等待缓存失效，否则页面不会自动更新以显示最新的数据。

#### 这是因为浏览器通常会缓存页面内容以提高性能和用户体验。在这种情况下，页面内容在一定时间内不会更新，除非用户主动刷新页面或者等待缓存失效。





## 缓存

在 Next.js 中，缓存机制是一个关键的性能优化手段，帮助加快页面加载速度和减少服务器负载。下面是对三种缓存的详细介绍：

### 1. Data Cache

**Data Cache** 指的是对通过数据获取方法（如 `getStaticProps` 和 `getServerSideProps`）获取的数据进行缓存。这种缓存机制在构建时和请求时都可能发生。

- **静态生成（Static Generation）**：在构建时，数据被获取并静态地嵌入到生成的 HTML 文件中。这个缓存是长期有效的，直到下次构建或者手动清除缓存。
- **服务器端渲染（Server-side Rendering）**：每次请求都会触发数据获取并渲染页面，但为了优化性能，可以在服务器端对获取的数据进行缓存，以减少对数据源的频繁请求。

**存储位置**：在静态生成场景下，缓存的数据通常存储在生成的静态文件中，这些文件通常存储在 CDN 或文件系统中。在服务器端渲染场景下，数据缓存一般存储在服务器内存或持久化存储系统（如 Redis 等）中。

### 2. Full Route Cache

**Full Route Cache** 是指对整个页面（路由）的缓存。对于使用静态生成的页面，这种缓存直接表现为生成的 HTML 文件。这些文件在构建时创建，并存储在文件系统中，以便在请求时快速响应。

- **静态页面（Static Pages）**：这些页面在构建时生成并缓存，直到下次构建或内容更新。
- **增量静态再生（Incremental Static Regeneration, ISR）**：允许在构建后更新部分静态页面，新的静态页面会在第一次请求时生成，并存储到文件系统中，后续请求可以直接使用缓存的版本。

**存储位置**：这些缓存文件主要存储在文件系统中，比如服务器的磁盘或云存储服务中。

### 3. Client Cache

**Client Cache** 是指在客户端进行的缓存，通常使用浏览器的缓存机制，如 HTTP 缓存、Service Worker 缓存等。这种缓存有助于减少客户端的加载时间和网络请求。

- **HTTP 缓存**：利用 HTTP 头信息（如 `Cache-Control`、`ETag` 等）在浏览器中缓存静态资源和数据请求。
- **Service Worker**：可以在客户端创建高级缓存策略，缓存静态资源和 API 请求。

**存储位置**：这些缓存存储在用户的浏览器中，是基于客户端的缓存机制。

### 关于“data cache 和 full route cache 大多数存在于服务器”的理解

这句话的意思是，对于大多数应用来说，数据缓存和整个路由的缓存主要是在服务器端进行的。也就是说：

- **Data Cache** 在服务器端缓存数据，以便在后续请求中更快地获取和处理。这通常是通过内存缓存、数据库或其他持久化存储机制实现的。
- **Full Route Cache** 通常指静态生成的页面，这些页面在构建时生成并存储在服务器的文件系统中，或者通过 CDN 分发到全球各地，用户请求时可以快速响应。

虽然部分缓存可能存储在用户文件系统中（如客户端缓存），但核心缓存逻辑和数据处理通常在服务器端进行，以确保数据的一致性和高效的资源管理。



## 路由和导航

在App路由器文件夹中，可以通过文件夹来定义路由(前提为有特定文件page)

路由可以嵌套，以文件夹的形式来实现

使用next自带的Link组件来导航 



### 客户端组件和服务器组件

在next.js中有两种组件**服务器组件**和**客户端组件**

#### 服务器组件有很多好处

对搜索引擎友好，引擎可以看到HTML文件构成，可以定义索引

对客户端用户友好，在服务器渲染html，这样就不用在用户电脑进行渲染，和加快网页呈现

#### 服务器组件坏处

没有互动性（点击，onChange，onSubmit）

。。。



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



## 获取数据

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





### 导航

#### Link组件

**1.只下载目标页面的内容**

**2.预取视口中的链接**

**3.在客户端缓存页面**



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













