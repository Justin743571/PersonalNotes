# Dom

### 浏览器是如何处理 HTML 文件并渲染页面的

理清楚浏览器是如何处理 HTML 文件并渲染页面的。以下是一个简化的步骤概述，解释从浏览器接收到 HTML 文件到最终渲染页面的过程。

### 浏览器渲染过程

1. **浏览器请求和接收 HTML 文件**：
    - 当你在浏览器中输入 URL 并按下回车键，浏览器会发送一个 HTTP 请求到服务器，要求获取相应的 HTML 文件。
    - 服务器响应这个请求并将 HTML 文件返回给浏览器。

2. **HTML 解析**：
    - 浏览器接收到 HTML 文件后，开始解析 HTML 内容。解析是逐行进行的，从头到尾读取 HTML 文件。
    - 在解析过程中，浏览器会遇到各种标签（如 `<html>`、`<head>`、`<body>`、`<div>` 等）和文本内容，并将其转换为一棵树形结构，称为 **DOM 树**（Document Object Model）。

3. **构建 DOM 树**：
    - DOM 树是 HTML 文档的内存表示形式，每个节点对应一个 HTML 标签。
    - 例如，以下 HTML 会被解析成一个简单的 DOM 树：

      ```html
      <html>
        <head>
          <title>My Page</title>
        </head>
        <body>
          <div>
            Hello, world!
          </div>
        </body>
      </html>
      ```

4. **解析 CSS**：
    - 浏览器在解析 HTML 的同时，也会解析 CSS。CSS 可以在 `<style>` 标签内，作为 `<link>` 标签指向的外部文件，或者嵌入在 HTML 标签的 `style` 属性中。
    - 解析 CSS 的过程会生成一棵 **CSSOM 树**（CSS Object Model），描述样式信息。

5. **合成渲染树**：
    - 浏览器将 DOM 树和 CSSOM 树结合起来，生成 **渲染树**。渲染树包含了每个需要在屏幕上显示的节点以及它们的样式信息。
    - 渲染树不包括那些不可见的元素（如 `<head>` 和 `display: none` 的元素）。

6. **布局（布局计算）**：
    - 一旦渲染树建立起来，浏览器就会进行布局计算（也称为回流）。这一步确定每个节点在屏幕上的确切位置和尺寸。
    - 浏览器从渲染树的根节点开始，遍历整个树并计算每个节点的几何信息。

7. **绘制（绘图）**：
    - 最后一步是将布局好的内容绘制到屏幕上。这一步称为绘图，浏览器将渲染树的每个节点转换为实际的像素并显示出来。

### 过程中的并行处理

- **异步请求**：HTML 中的外部资源（如 CSS、JavaScript、图像等）会通过新的 HTTP 请求异步获取。在 HTML 解析过程中，浏览器会并行下载这些资源，但 JavaScript 文件的处理会影响 HTML 解析，因为它们可能会修改 DOM。
- **JavaScript 解析和执行**：浏览器会解析和执行 `<script>` 标签中的 JavaScript 代码，JavaScript 可能会操作 DOM 和 CSSOM。这意味着 JavaScript 执行可能会暂停 HTML 的解析，直到脚本执行完成。

### 总结

从 HTML 文件到最终渲染页面的过程可以概括为以下步骤：
1. 浏览器请求并接收 HTML 文件。
2. 解析 HTML，生成 DOM 树。
3. 解析 CSS，生成 CSSOM 树。
4. 将 DOM 树和 CSSOM 树结合，生成渲染树。
5. 布局计算，确定每个节点的几何位置和尺寸。
6. 将布局好的内容绘制到屏幕上。

这个过程确保浏览器可以正确地显示网页内容，并响应用户的操作。



## React 与浏览器的工作流程

React 是一个用于构建用户界面的 JavaScript 库，通常与浏览器配合工作以渲染动态、交互式的网页内容。下面详细解释 React 与浏览器的工作流程，从编写 React 代码到在浏览器中渲染出页面的过程。

### React 与浏览器的工作流程

1. **编写 React 组件**：
    - 开发者用 JavaScript（或 TypeScript）和 JSX（JavaScript XML）编写 React 组件。组件是独立的、可重用的 UI 单元，例如：

      ```jsx
      import React from 'react';
      
      const Greet = ({ name }) => {
        return (
          <div>
            {name ? <h1>Hello, {name}!</h1> : <button>Login</button>}
          </div>
        );
      };
      
      export default Greet;
      ```

2. **React 编译和打包**：
    - React 代码通常使用工具（如 Babel 和 Webpack）进行编译和打包。Babel 将 JSX 转换为标准的 JavaScript，Webpack 将所有资源（JavaScript、CSS、图像等）打包成单个或多个文件，可以在浏览器中加载。
    - 例如，Babel 会将上面的 JSX 转换为：

      ```javascript
      import React from 'react';
      
      const Greet = ({ name }) => {
        return React.createElement(
          'div',
          null,
          name ? React.createElement('h1', null, `Hello, ${name}!`) : React.createElement('button', null, 'Login')
        );
      };
      
      export default Greet;
      ```

3. **加载 HTML 文件**：
    - 浏览器请求并加载包含基础 HTML 的文件。HTML 文件中通常包含一个根元素（如 `<div id="root"></div>`），用于挂载 React 应用。

      ```html
      <!DOCTYPE html>
      <html lang="en">
      <head>
        <meta charset="UTF-8">
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <title>React App</title>
      </head>
      <body>
        <div id="root"></div>
        <script src="/path/to/your/bundle.js"></script>
      </body>
      </html>
      ```

4. **挂载 React 应用**：
    - 加载的 JavaScript 文件包含 React 应用的代码。通过 `ReactDOM.render` 方法将 React 组件挂载到 HTML 文件中的根元素上。

      ```javascript
      import React from 'react';
      import ReactDOM from 'react-dom';
      import Greet from './Greet';
      
      ReactDOM.render(<Greet name="Mosh" />, document.getElementById('root'));
      ```

5. **虚拟 DOM 和真实 DOM**：
    - React 使用虚拟 DOM 来描述 UI 的结构。虚拟 DOM 是一个轻量级的 JavaScript 对象，与实际的 DOM 对象相比，操作起来更快。
    - 当状态或属性发生变化时，React 会生成新的虚拟 DOM 树，并与旧的虚拟 DOM 树进行比较（称为“调和”）。
    - React 只会将发生变化的部分更新到真实 DOM 中，最小化直接的 DOM 操作，提高性能。

6. **更新和重新渲染**：
    - 当组件的状态（state）或属性（props）发生变化时，React 会重新渲染相应的组件。
    - 例如，用户点击按钮会触发事件，事件处理程序更新组件的状态：

      ```javascript
      import React, { useState } from 'react';

      const Greet = () => {
        const [name, setName] = useState('');

        const handleLogin = () => {
          setName('Mosh');
        };

        return (
          <div>
            {name ? <h1>Hello, {name}!</h1> : <button onClick={handleLogin}>Login</button>}
          </div>
        );
      };

      export default Greet;
      ```

    - 状态变化后，React 会重新渲染 `Greet` 组件，并更新虚拟 DOM 树。然后，React 比较新的虚拟 DOM 树和旧的虚拟 DOM 树，找出差异，并将差异更新到真实 DOM。

### 总结

React 与浏览器的工作流程可以概括为以下几个步骤：

1. 开发者编写 React 组件。
2. 使用 Babel 编译 JSX，使用 Webpack 打包资源。
3. 浏览器加载基础 HTML 文件和打包好的 JavaScript 文件。
4. React 应用通过 `ReactDOM.render` 方法挂载到 HTML 文件中的根元素上。
5. React 使用虚拟 DOM 来描述和管理 UI。
6. 当组件的状态或属性变化时，React 更新虚拟 DOM 树，并将变化高效地应用到真实 DOM 中。

通过这个流程，React 和浏览器协同工作，使得开发者能够构建高效、动态的用户界面。







# 测试运行包

在使用Vitest对React组件进行测试时，以下三个包是非常有用的，它们各自有不同的功能和用途：

### 1. React Testing Library
**React Testing Library** 是一个专门为测试React组件而设计的库。它的核心理念是鼓励开发者编写以用户行为为导向的测试。这意味着你的测试应该尽量模拟用户实际会如何与应用进行交互，而不是测试实现细节。

- **功能和特点**：
  - 提供一组简单的工具来选择和操作DOM元素，比如`getByText`, `getByRole`, `getByLabelText`等。
  - 强调测试组件的公共API和用户交互，而不是组件的内部实现。
  - 使得测试代码更容易维护和理解，因为它们更接近于实际的用户行为。

- **用法示例**：
  ```javascript
  import { render, screen } from '@testing-library/react';
  import MyComponent from './MyComponent';
  
  test('renders the correct content', () => {
    render(<MyComponent />);
    expect(screen.getByText('Hello, World!')).toBeInTheDocument();
  });
  ```

### 2. jsdom
**jsdom** 是一个在Node.js环境下模拟浏览器DOM和BOM的库。它允许你在没有浏览器的情况下运行前端代码，特别是在测试环境中非常有用。

- **功能和特点**：
  - 提供一个类似于浏览器环境的API，使得在Node.js中运行的代码能够访问DOM。
  - 通常与测试框架（如Vitest或Jest）结合使用，为测试提供一个虚拟的浏览器环境。
  - 支持大部分现代浏览器的功能和API。

- **用法示例**：
  在使用React Testing Library时，jsdom通常会被自动配置为测试环境的一部分。你不需要显式地引入它，但可以在测试框架的配置文件中看到它的使用。
  ```javascript
  // 在Vitest或Jest配置文件中
  testEnvironment: 'jsdom'
  ```

### 3. jest-dom
**jest-dom** 是一组自定义匹配器，使得在使用Jest编写测试时，可以更方便地断言DOM节点的状态和属性。这些匹配器扩展了Jest的内置匹配器，为你提供了更具可读性和表达力的断言方式。

- **功能和特点**：
  - 提供了一组额外的匹配器，如`toBeInTheDocument`, `toHaveTextContent`, `toHaveAttribute`等。
  - 这些匹配器专门用于测试DOM元素，能使测试代码更加简洁和易读。
  - 与React Testing Library紧密集成，提升了编写UI测试的体验。

- **用法示例**：
  ```javascript
  import { render, screen } from '@testing-library/react';
  import '@testing-library/jest-dom/extend-expect';  // 引入jest-dom的扩展匹配器
  import MyComponent from './MyComponent';
  
  test('button has correct text', () => {
    render(<MyComponent />);
    expect(screen.getByRole('button')).toHaveTextContent('Submit');
  });
  ```

### 总结
- **React Testing Library** 提供了一组工具来测试React组件的用户交互和公共API。
- **jsdom** 模拟了浏览器的DOM环境，使得你可以在Node.js中运行和测试前端代码。
- **jest-dom** 提供了方便的自定义匹配器，用于断言DOM元素的状态和属性，使测试代码更具可读性。

这三个库常常一起使用，提供了一个强大而方便的工具集，用于测试React应用的不同方面。

 

# 测试React 组件

## 需要测试什么

1.测试组件的渲染

2.测试组件的交互

3.测试组件的行为（特定函数是否被调用）

## render 和screen函数

### `render(<Greet name="Mosh" />);`
这行代码的作用是使用 `@testing-library/react` 中的 `render` 函数渲染 `Greet` 组件。`render` 函数的具体作用如下：

1. **生成虚拟 DOM**：
    - `render` 会创建一个虚拟 DOM，其中包含 `Greet` 组件及其子组件的结构。在这个例子中，`Greet` 组件会接收一个 `name` 属性，其值为 `"Mosh"`。

2. **挂载到测试环境中**：
    - `render` 会将生成的虚拟 DOM 挂载到一个与真实 DOM 类似的环境中，这个环境是由 `jsdom`（JavaScript 实现的 DOM 和 HTML 标准）提供的。`jsdom` 模拟浏览器环境，使得在 Node.js 中也可以运行和测试前端代码。

### `const heading = screen.getByRole("heading");`
这行代码使用 `@testing-library/react` 提供的 `screen` 对象来查询渲染后的虚拟 DOM，并找到一个具有特定角色的元素。在这个例子中，`getByRole("heading")` 会查找一个具有 "heading" 角色的元素。具体作用如下：

1. **查询虚拟 DOM**：
    - `screen.getByRole("heading")` 会在已经渲染的虚拟 DOM 中查找第一个角色为 "heading" 的元素。如果找不到这样的元素，会抛出一个错误。

2. **获取元素**：
    - 如果找到了角色为 "heading" 的元素，它会被赋值给 `heading` 变量。此时，`heading` 变量包含这个元素的引用，可以进一步进行断言和操作。

### 代码中的逻辑和断言

#### 第一个测试用例

```javascript
it("如果提供参数name 应该渲染hello和name", () => {
  render(<Greet name="Mosh" />);
  const heading = screen.getByRole("heading");
  expect(heading).toBeInTheDocument();
  expect(heading).toHaveTextContent(/hello/i);
});
```

1. **渲染 `Greet` 组件**：传递 `name="Mosh"`。
2. **查找 "heading" 元素**：使用 `getByRole` 查找角色为 "heading" 的元素。
3. **断言元素存在**：检查是否找到了 "heading" 元素。
4. **断言文本内容**：检查 "heading" 元素的文本内容是否包含 "hello"。

#### 第二个测试用例

```javascript
it("如果不提供参数name 应该渲染login按钮", () => {
  render(<Greet />);
  const button = screen.getByRole("button");
  expect(button).toBeInTheDocument();
  expect(button).toHaveTextContent(/login/i);
});
```

1. **渲染 `Greet` 组件**：不传递 `name` 参数。
2. **查找 "button" 元素**：使用 `getByRole` 查找角色为 "button" 的元素。
3. **断言元素存在**：检查是否找到了 "button" 元素。
4. **断言文本内容**：检查 "button" 元素的文本内容是否包含 "login"。

### 总结

- **`render(<Greet name="Mosh" />);`**：在模拟的浏览器环境中渲染 `Greet` 组件。
- **`const heading = screen.getByRole("heading");`**：在渲染后的虚拟 DOM 中查找角色为 "heading" 的元素，如果找不到会抛出错误。

这样，通过渲染组件并在虚拟 DOM 中查找元素，你可以模拟用户交互并验证组件的行为是否符合预期。



### 细节

我们可以使用screen.debug();函数去查看渲染的虚拟dom结构





## 测试没有role属性的组件，queryByRole的使用

### 组件

```tsx
import { User } from "../entities";

const UserAccount = ({ user }: { user: User }) => {
  return (
    <>
      <h2>User Profile</h2>
      {user.isAdmin && <button>Edit</button>}
      <div>
        <strong>Name:</strong> {user.name}
      </div>
    </>
  );
};

export default UserAccount;

```

### 综合解释

以下是你的测试的综合解释：

1. **渲染用户姓名**

   ```javascript
   it('应该渲染name', () => {
       const user:User = {id:1,name:"mosh"};
       render(<UserAccount user={user}/>)
       expect(screen.getByText(user.name)).toBeInTheDocument();
   })
   ```

   这个测试检查组件是否正确渲染了用户的姓名。使用`getByText`方法查找包含用户姓名的元素，并检查该元素是否在文档中。

2. **渲染编辑按钮（用户是管理员）**

   ```javascript
   it('如果用户是admin,则渲染edit按钮', () => {
       const user:User = {id:1,name:"mosh",isAdmin:true};
       render(<UserAccount user={user}/>)
       const button = screen.getByRole("button")
       expect(button).toBeInTheDocument()
       expect(button).toHaveTextContent(/edit/i)
   })
   ```

   这个测试检查当用户是管理员时，是否渲染了一个带有“edit”文本的按钮。使用`getByRole`方法查找按钮元素，并检查该按钮是否存在及其文本内容。

3. **不渲染编辑按钮（用户不是管理员）**

   ```javascript
   it('如果用户不是admin,则不渲染edit按钮', () => {
       const user:User = {id:1,name:"mosh"};
       render(<UserAccount user={user}/>)
       const button = screen.queryByRole("button")
       expect(button).not.toBeInTheDocument()
   })
   ```

   这个测试检查当用户不是管理员时，是否没有渲染编辑按钮。使用`queryByRole`方法查找按钮元素，并检查该按钮是否不存在于文档中。

在你的测试代码中，使用了`screen.getByText`、`screen.getByRole`和`screen.queryByRole`方法。以下是对这些方法和相关断言的解释：

### `screen.getByText`

`screen.getByText`方法用于查找包含特定文本的元素。如果找到多个匹配的元素，测试将失败。该方法在找不到元素时会抛出错误。它的使用示例如下：

```javascript
expect(screen.getByText(user.name)).toBeInTheDocument();
```

这个断言检查是否存在一个包含用户姓名文本的元素。如果找到该元素，断言将通过；如果找不到，该方法会抛出一个错误，测试将失败。

### `screen.getByRole`

`screen.getByRole`方法用于通过角色（role）查找元素。ARIA角色定义了元素的用途，例如按钮、文本框等。如果找到多个匹配的元素，测试将失败。它的使用示例如下：

```javascript
const button = screen.getByRole("button")
expect(button).toBeInTheDocument()
expect(button).toHaveTextContent(/edit/i)
```

这个断言首先通过角色“button”找到按钮元素，然后检查该按钮是否存在于文档中，以及其文本内容是否包含“edit”。

### `screen.queryByRole`

`screen.queryByRole`方法与`screen.getByRole`类似，但在找不到元素时不会抛出错误，而是返回`null`。这在你希望检查某个元素是否**不存在**时非常有用。它的使用示例如下：

```javascript
const button = screen.queryByRole("button")
expect(button).not.toBeInTheDocument()
```

这个断言检查页面上是否不存在角色为“button”的元素。如果不存在，断言将通过；如果存在，测试将失败。

### `expect(element).not.toBeInTheDocument()`

这个断言用于检查某个元素是否不在文档中。它通常与`queryBy*`方法一起使用，因为这些方法在找不到元素时不会抛出错误。例如：

```javascript
const button = screen.queryByRole("button")
expect(button).not.toBeInTheDocument()
```

这个断言检查页面上是否没有角色为“button”的元素。如果确实没有，断言将通过；如果有，测试将失败。

1. 

通过这些测试，你可以确保组件根据用户的不同角色正确渲染相应的内容和控件。



## 测试列表

### 组件

```tsx
import { User } from "../entities";

const UserList = ({ users }: { users: User[] }) => {
  if (users.length === 0) return <p>No users available.</p>;

  return (
    <ul>
      {users.map((user) => (
        <li key={user.id}>
          <a href={`/users/${user.id}`}>{user.name}</a>
        </li>
      ))}
    </ul>
  );
};

export default UserList;

```

测试文件

```typescript
import { render, screen } from '@testing-library/react'
import UserList from '../../src/components/UserList';
import { User } from '../../src/entities';


describe('UserList', () => {
    it('如果没有用户数组，应该渲染一段文字', () => {
        render(<UserList users={[]}/>)
        expect(screen.getByText(/no users/i)).toBeInTheDocument();
    })
    it('应该渲染用户列表', () => {
        const users:User[] =[
            {id:1,name:"Mosh"},
            {id:2,name:"John"},
        ]
        render(<UserList users={users}/>)
        users.forEach(user =>{
            const link = screen.getByRole("link",{name:user.name});
            expect(link).toBeInTheDocument();
            expect(link).toHaveAttribute("href",`/users/${user.id}`)
        })
    })
})
```

这里需要注意的是 const link = screen.getByRole("link",{name:user.name});这里表示的一个特定link元素中有name的DOM，

## 测试特殊列表

### 组件

```tsx
const ProductImageGallery = ({ imageUrls }: { imageUrls: string[] }) => {
  if (imageUrls.length === 0) return null;

  return (
    <ul>
      {imageUrls.map((url) => (
        <li key={url}>
          <img src={url} />
        </li>
      ))}
    </ul>
  );
};

export default ProductImageGallery;

```

### 测试文件

```ts
import { render, screen } from "@testing-library/react";
import ProductImageGallery from "../../src/components/ProductImageGallery";

describe("ProductImageGallery", () => {
  it("如果给一个空数组,应该不渲染", () => {
    const { container } = render(<ProductImageGallery imageUrls={[]} />);
    expect(container).toBeEmptyDOMElement();
  });
  it("应该渲染图像列表", () => {
    const imageUrls = ["asgas", "sfasfa", "svdfsfd"];
    render(<ProductImageGallery imageUrls={imageUrls} />);
    const images = screen.getAllByRole("img");
    expect(images).toHaveLength(3);
    imageUrls.forEach((url,index) =>{
        expect(images[index]).toHaveAttribute("src",url)
    })
  });
});

```

对于这个组件而言，img组件无法包裹一个name，导致我们不可以通过普通遍历的方式去断言,所以以另外一种方式来测试

## getAllByRole与getByRole的区别

`getAllByRole`和`getByRole`都是React Testing Library中的查询方法，用于根据ARIA角色选择DOM元素。它们的主要区别在于返回结果的数量和行为方式：

### `getByRole`

- **返回结果**：返回匹配角色的**单个元素**。
- **行为**：如果找到多个匹配的元素，测试将失败，并抛出错误；如果找不到匹配的元素，也会抛出错误。
- **使用场景**：适用于预期只有一个匹配元素的情况。

### `getAllByRole`

- **返回结果**：返回匹配角色的**所有元素**，以数组形式。
- **行为**：如果找不到任何匹配的元素，测试将失败，并抛出错误。
- **使用场景**：适用于预期有多个匹配元素的情况，或者你需要遍历多个元素进行进一步检查。

### 选择方法的使用场景

- **`getByRole`**：当你知道页面上只有一个元素应该匹配时，例如一个唯一的提交按钮。
- **`getAllByRole`**：当你知道页面上有多个元素应该匹配时，例如一组按钮、列表项或其他重复的控件。

### 总结

- **`getByRole`**：用于选择唯一的匹配元素。找不到或找到多个匹配时会抛出错误。
- **`getAllByRole`**：用于选择多个匹配元素，返回一个数组。找不到任何匹配时会抛出错误。



## 测试用户交互

### 组件

```tsx
import { useState } from "react";

const TermsAndConditions = () => {
  const [isChecked, setIsChecked] = useState(false);

  return (
    <div>
      <h1>Terms & Conditions</h1>
      <p>
        Lorem ipsum dolor, sit amet consectetur adipisicing elit. Autem,
        delectus.
      </p>
      <div className="pb-3">
        <label htmlFor="agree">
          <input
            type="checkbox"
            id="agree"
            checked={isChecked}
            onChange={() => setIsChecked(!isChecked)}
            className="mr-1"
          />
          I accept the terms and conditions.
        </label>
      </div>
      <button disabled={!isChecked} className="btn">
        Submit
      </button>
    </div>
  );
};

export default TermsAndConditions;

```

### 测试

```ts
import { render, screen } from "@testing-library/react";
import TermsAndConditions from "../../src/components/TermsAndConditions";
import userEvent from "@testing-library/user-event";

describe("TermsAndConditions", () => {
  const renderComponent = () => {
    render(<TermsAndConditions />);
    return {
      heading: screen.getByRole("heading"),
      checkbox: screen.getByRole("checkbox"),
      button: screen.getByRole("button"),
    };
  };
  it("应呈现正确的文本和初始状态", () => {
    const { heading, checkbox, button } = renderComponent();

    expect(heading).toHaveTextContent("Terms & Conditions");
    expect(checkbox).not.toBeChecked();
    expect(button).toBeDisabled();
  });
  it("应在选中复选框时启用按钮", async () => {
    const { checkbox } = renderComponent();

    const user = userEvent.setup();
    await user.click(checkbox);

    expect(checkbox).toBeEnabled();
  });
});

```



### 新例子

组件

```tsx
import { useState } from "react";

const ExpandableText = ({ text }: { text: string }) => {
  const limit = 255;
  const [isExpanded, setExpanded] = useState(false);

  if (text.length <= limit) return <article>{text}</article>;

  return (
    <div>
      {isExpanded ? (
        <article>{text}</article>
      ) : (
        <article>{text.substring(0, limit)}...</article>
      )}
      <button className="btn" onClick={() => setExpanded(!isExpanded)}>
        {isExpanded ? "Show Less" : "Show More"}
      </button>
    </div>
  );
};

export default ExpandableText;

```

测试

```ts
import { render, screen } from "@testing-library/react";
import ExpandableText from "../../src/components/ExpandableText";
import userEvent from "@testing-library/user-event";

describe("ExpandableText", () => {
  const limit = 255;
  const longText = "a".repeat(limit + 1);
  const truncatedText = longText.substring(0, limit) + "...";

  it("如果文本少于 255 个字符，则应显示全文", () => {
    const text = "hello world";
    render(<ExpandableText text={text} />);

    expect(screen.getByText(text)).toBeInTheDocument();
  });
  it("如果文本大于255个字符, 则应呈现被截断的文本", () => {
    render(<ExpandableText text={longText} />);

    expect(screen.getByText(truncatedText)).toBeInTheDocument();
    const button = screen.getByRole("button");
    expect(button).toHaveTextContent(/more/i);
  });
  it("如果Show More按钮被点击, 则呈现扩展文本", async () => {
    render(<ExpandableText text={longText} />);

    const button = screen.getByRole("button");
    const user = userEvent.setup();
    await user.click(button);

    expect(screen.getByText(longText)).toBeInTheDocument();
    expect(button).toHaveTextContent(/less/i);
  });
  it("如果Show Less按钮被点击, 则呈现截断文本", async () => {
    render(<ExpandableText text={longText} />);

    const showMoreButton = screen.getByRole("button",{name:/more/i});
    const user = userEvent.setup();
    await user.click(showMoreButton);

    const showLessButton = screen.getByRole("button",{name:/less/i})
    await user.click(showLessButton);

    expect(screen.getByText(truncatedText)).toBeInTheDocument();
    expect(showMoreButton).toHaveTextContent(/more/i);
  });
});

```



## 测试输入框

### 组件

```tsx
import { useState } from "react";

interface Props {
  onChange: (text: string) => void;
}

const SearchBox = ({ onChange }: Props) => {
  const [searchTerm, setSearchTerm] = useState("");

  return (
    <div>
      <input
        type="text"
        placeholder="Search..."
        className="input"
        onChange={(e) => setSearchTerm(e.target.value)}
        onKeyDown={(e) => {
          if (e.key === "Enter" && searchTerm) onChange(searchTerm);
        }}
      />
    </div>
  );
};

export default SearchBox;

```

### 测试

```ts
import { render, screen } from "@testing-library/react";
import SearchBox from "../../src/components/SearchBox";
import userEvent from "@testing-library/user-event";

describe("SearchBox", () => {
  const renderSearchBox = () => {
    const onChange = vi.fn();
    render(<SearchBox onChange={onChange} />);
    return {
      input: screen.getByPlaceholderText(/search/i),
      user: userEvent.setup(),
      onChange,
    };
  };

  it("应呈现一个用于搜索的输入框", () => {
    const { input } = renderSearchBox();

    expect(input).toBeInTheDocument();
  });

  it("按回车键时应调用 onChange", async () => {
    const { input, user, onChange } = renderSearchBox();

    const searchTerm = "SearchTerm";
    await user.type(input, searchTerm + "{enter}");

    expect(onChange).toHaveBeenCalledWith(searchTerm);
  });

  it("如果输入框是空的 按回车键时不应调用 onChange", async () => {
    const { input, user, onChange } = renderSearchBox();

    await user.type(input, "{enter}");

    expect(onChange).not.toHaveBeenCalled();
  });
});

```

### 解释

```ts
await user.type(input, searchTerm + "{enter}");
```

1. **模拟用户输入文本**：
   - `searchTerm`是我们希望用户输入的文本。在测试中，我们定义了`searchTerm`，例如`const searchTerm = "SearchTerm";`。
   - `user.type(input, searchTerm)`模拟了用户在输入框中输入`SearchTerm`的过程。
2. **模拟用户按下回车键**：
   - `"{enter}"`是一个特殊字符串，用于模拟用户按下回车键。
   - `user.type(input, searchTerm + "{enter}")`将用户输入文本和按下回车键的操作结合在一起，模拟了用户输入完整的搜索词并按下回车键的实际操作。

## 测试异步代码

### 组件

```tsx
import delay from "delay";
import { useEffect, useState } from "react";

const TagList = () => {
  const [tags, setTags] = useState<string[]>([]);

  useEffect(() => {
    const fetchTags = async () => {
      await delay(500);
      setTags(["tag1", "tag2", "tag3"]);
    };
    fetchTags();
  });

  return (
    <ul>
      {tags.map((tag) => (
        <li key={tag}>{tag}</li>
      ))}
    </ul>
  );
};

export default TagList;

```

### 测试

```tsx
import { render, screen } from "@testing-library/react";
import TagList from "../../src/components/TagList";

describe("TagList", () => {
  it("应呈现Tags", async () => {
    render(<TagList />);

    // await waitFor(() =>{
    //     const listItems = screen.getAllByRole("listitem");
    //     expect(listItems.length).toBeGreaterThan(0);
    // })
    
    const listItems = await screen.findAllByRole("listitem");
    expect(listItems.length).toBeGreaterThan(0);

  });
});

```

**findBy系列函数可以用于异步查询DOM元素的。**

## `findBy`系列

​	在React Testing Library中，`findBy`系列函数（如`findByRole`、`findByText`等）是用于异步查询DOM元素的。这些函数返回一个Promise，在满足条件时解析该Promise，未满足条件时会等待元素出现或条件满足后再解析。**它们非常适合测试需要一定时间才能加载或渲染的元素，例如通过网络请求加载的数据。**

### `findBy`系列函数的主要用途

`findBy`系列函数的主要用途是处理异步操作和动态内容。在测试需要异步加载内容的组件时，它们比同步的`getBy`系列函数更合适。

### 常见的`findBy`函数

1. **findByRole**: 根据元素的角色查询，如按钮、链接等。
2. **findByText**: 根据元素的文本内容查询。
3. **findByLabelText**: 根据元素的关联标签文本查询，通常用于表单元素。
4. **findByPlaceholderText**: 根据元素的占位符文本查询，常用于输入框。
5. **findByAltText**: 根据元素的替代文本查询，常用于图像。
6. **findByTestId**: 根据元素的测试ID查询。



## 测试组件库

在测试组件库时，会遇到很多问题

**1.需要提供上下文组件**

**2.jsdom某一些都行没有配置**

**3.断言一个元素得看role属性**

**4.断言下拉框的选项**

如果是一个组件库下拉框，我们需要去寻找这个下拉框点击后显示的那个选项属性role去抓取这个DOM，所以操作应该先模拟用户点击，然后去screen.debug()查找选项的role属性(如果没有点击下拉框，这些选项都是隐藏的，所以需要点击)



**5.当你需要对动态添加到DOM中的元素进行断言时**，可以使用`findBy`或`findAllBy`方法。这些方法返回Promise，会等待指定的元素出现。在你的示例中，通过模拟用户点击`combobox`按钮后使用`findAllByRole("option")`来查找选项，并进行断言。这种方法确保即使初始DOM中没有这些元素，在交互后也可以找到并测试它们。

### 组件

```tsx
import { Select } from "@radix-ui/themes";

interface Props {
  onChange: (status: string) => void;
}

const OrderStatusSelector = ({ onChange }: Props) => {
  return (
    <Select.Root defaultValue="new" onValueChange={onChange}>
      <Select.Trigger />
      <Select.Content>
        <Select.Group>
          <Select.Label>Status</Select.Label>
          <Select.Item value="new">New</Select.Item>
          <Select.Item value="processed">Processed</Select.Item>
          <Select.Item value="fulfilled">Fulfilled</Select.Item>
        </Select.Group>
      </Select.Content>
    </Select.Root>
  );
};

export default OrderStatusSelector;

```

### 测试

```ts
import { render, screen } from "@testing-library/react";
import OrderStatusSelector from "../../src/components/OrderStatusSelector";
import { Theme } from "@radix-ui/themes";
import userEvent from "@testing-library/user-event";

describe("OrderStatusSelector", () => {
    const renderOrderStatusSelector = () =>{
        const onChange = vi.fn();
        render(
            <Theme>
              <OrderStatusSelector onChange={onChange} />
            </Theme>
          );
        return{
            trigger:screen.getByRole("combobox"),
            user:userEvent.setup(),
            getOptions:() =>screen.findAllByRole("option"),
            getOption:(label:RegExp) => screen.findByRole("option",{name:label}),
            onChange,
        }
    }

  it("作为默认值应呈现New", () => {
    const {trigger} = renderOrderStatusSelector();

    expect(trigger).toHaveTextContent(/new/i);
  });

  it("应呈现全部正确状态", async() => {
    const {trigger,user,getOptions} = renderOrderStatusSelector();

    await user.click(trigger);

    const options = await getOptions();
    expect(options).toHaveLength(3)

    const labels = options.map(option => option.textContent);
    expect(labels).toEqual(["New","Processed","Fulfilled"])
  });

  it('当选择Processed时 应调用processed的 onChange', async() => {
    const {user,trigger,onChange,getOption} = renderOrderStatusSelector();
    await user.click(trigger);

    const option = await getOption(/processed/i);
    await user.click(option);


    expect(onChange).toHaveBeenCalledWith("processed");
  })
  
  it('当选择Fulfilled时 应调用fulfilled的 onChange', async() => {
    const {user,trigger,onChange,getOption} = renderOrderStatusSelector();
    await user.click(trigger);

    const option = await getOption(/fulfilled/i);
    await user.click(option);


    expect(onChange).toHaveBeenCalledWith("fulfilled");
  })

  it('当选择New时 应调用new的 onChange', async() => {
    const {user,trigger,onChange,getOption} = renderOrderStatusSelector();
    
    await user.click(trigger);
    await user.click(await getOption(/fulfilled/i));

    await user.click(trigger)
    await user.click(await getOption(/new/i));


    expect(onChange).toHaveBeenCalledWith("new");
  })
  it('should', async() => {
    const {user,trigger} = renderOrderStatusSelector();
    
    await user.click(trigger);
    screen.debug()
  })
});

```

# 模拟APIs

## MSW

Mock Service Worker (MSW) 是一个用于拦截网络请求并提供模拟响应的工具，它特别适合于在前端应用程序开发和测试过程中模拟后台服务。使用MSW，你可以在不依赖实际后台服务的情况下测试和开发你的应用程序，这样可以提高开发效率，减少对外部依赖的需求，并且更容易进行测试。

### MSW的主要用途和优点

1. **模拟API响应**：
   - 在前端开发和测试过程中，可以用来模拟服务器的API响应，从而不需要实际的服务器或后端服务。
   - 可以模拟不同的API响应状态，例如成功、错误、延迟等，以测试前端应用的各种情况。
2. **隔离测试**：
   - 使前端开发者可以在完全隔离的环境中测试组件和逻辑，确保测试的稳定性和可重复性。
   - 避免因为后台服务不稳定或未实现而影响前端开发和测试。
3. **自动化测试**：
   - 在自动化测试中使用MSW，可以控制和模拟各种网络请求的场景，使测试更加全面和可靠。
   - 提供一致的测试环境，不受网络波动和服务不可用的影响。

### 总结

Mock Service Worker 是一个强大的工具，可以帮助前端开发者在开发和测试过程中模拟后台服务。它通过拦截网络请求并提供模拟响应，使得前端开发和测试变得更加独立、高效和可靠。通过合理配置和使用MSW，可以极大地提升开发体验和测试质量。

### 配置

1.创建一个文件 `src/mocks/handlers.js`，用于定义如何拦截和处理网络请求的处理器

2.定义server对象

3.在测试文件中最开始开启服务，测试结束时重置服务然后关闭服务



### 使用faker.js得到虚拟数据

`faker.js` 是一个用于生成各种假数据的 JavaScript 库。它广泛应用于开发和测试过程中，用于生成模拟数据，帮助开发者创建更加逼真的测试环境和样本数据。

### 主要功能

1. **生成不同类型的假数据**：
   - 生成随机的名字、地址、电话号码、电子邮件等个人信息。
   - 生成随机的日期、颜色、商品名称、公司名称等。
   - 支持多种语言和本地化设置。
2. **简化测试数据创建**：
   - 在编写测试时，可以快速生成大规模的测试数据。
   - 提供多种数据类型和格式，帮助模拟各种业务场景。
3. **提升开发效率**：
   - 在开发过程中，使用假数据填充应用，使得开发更加高效。
   - 避免了手动创建数据的繁琐过程。

### 使用@mswjs/data建模数据和查询

`@mswjs/data` 是一个与 Mock Service Worker (MSW) 搭配使用的库，用于在前端模拟数据层。它提供了一种简单而强大的方式来创建和操作模拟数据，使你可以在开发和测试过程中模拟复杂的数据交互，而无需依赖真实的后端服务。

### 主要功能

1. **定义数据模型**：
   - 通过定义数据模型，你可以模拟数据库或API的数据结构。
   - 提供便捷的方法来生成和管理模拟数据。
2. **操作数据**：
   - 提供CRUD（创建、读取、更新、删除）操作来管理模拟数据。
   - 可以在测试和开发过程中动态地调整数据，以模拟不同的场景和状态。
3. **集成MSW**：
   - 与MSW无缝集成，拦截网络请求并返回模拟数据。
   - 可以用来模拟复杂的数据交互和业务逻辑。