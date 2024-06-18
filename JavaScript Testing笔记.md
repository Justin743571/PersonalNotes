# 正面测试和负面测试

在JavaScript（以及其他编程语言）的测试过程中，正面测试（Positive Testing）和负面测试（Negative Testing）是两种常用的方法。它们分别用于验证代码在预期条件下和非预期条件下的表现。以下是对这两种测试方法的介绍：

### 正面测试（Positive Testing）

**定义**：正面测试，也称为阳性测试或积极测试，是指在理想情况下进行的测试，目的是确保应用程序在提供正确的输入时能够按预期工作。

**特点**：

- 关注应用程序在正常情况下的功能是否正确。
- 使用有效和预期的输入数据进行测试。
- 确认系统按预期的逻辑和要求工作。

# 负面测试（Negative Testing）

**定义**：负面测试，也称为阴性测试或消极测试，是指故意使用无效或意外的输入来测试应用程序，目的是确保系统能够正确处理错误和异常情况。

**特点**：

- 关注系统在异常情况下的行为。
- 使用无效、边界或非预期的输入数据进行测试。
- 确认系统能够适当地处理错误和异常，不会崩溃或产生未定义的行为。



# 边界测试

### 边界测试（Boundary Testing）

**定义**：边界测试是软件测试中的一种技术，专注于测试输入数据的边界值。边界值是指输入范围的极限值，包括最小值、最大值、刚好超过最小值和最大值的值等。其目的是确保系统在处理边界条件时能正常工作，因为边界条件往往是错误和缺陷的高发区。

**特点**：

- 关注输入范围的极限值及其附近的值。
- 主要测试系统在边界条件下的行为。
- 边界测试通常用于发现由于极值而引起的错误。





## 参数化测试

ChatGPT

参数化测试（Parameterized Testing）是一种测试方法，通过将一组不同的输入数据传递给同一个测试用例，来验证代码在各种条件下的行为。它使得测试用例更加简洁、易读和可维护，并且能够高效地覆盖多个测试场景。

### 参数化测试的优点

1. **减少冗余**：避免为每组测试数据编写单独的测试用例，通过参数化可以复用相同的测试逻辑。
2. **提高覆盖率**：能够更容易地覆盖多个输入场景，包括边界值和异常情况。
3. **增强可维护性**：当需要添加或修改测试数据时，只需修改参数而无需调整测试用例逻辑。





# Mock Function

Mock Functions 在单元测试中非常有用，因为它们允许你模拟和控制函数的行为，从而更好地隔离和测试代码的各个部分。以下是 Vitest 中 Mock Functions 的介绍及其使用方法。

### 什么是 Mock Function

Mock Function 是一种模拟函数的工具，它可以替代真实的函数，使你可以控制其输入和输出。在测试中，Mock Function 允许你：
- 跟踪函数的调用次数和参数。
- 控制函数的返回值或抛出的错误。
- 验证代码在不同情况下的行为。



## 例题一

这段代码展示了如何使用 Vitest 进行单元测试，特别是如何通过模拟（mock）一个依赖函数来控制其返回值。下面我将逐行解释代码的作用：

### 生产代码
```javascript
// 定义一个函数，用于将价格转换为特定货币
export function getPriceInCurrency(price, currency) {
  // 获取 USD 到目标货币的汇率
  const rate = getExchangeRate('USD', currency);
  // 返回转换后的价格
  return price * rate;
}

// 定义一个获取汇率的函数
export const getExchangeRate = (from, to) => {
  console.log(`Getting the exchange rate ${from}-${to}...`);
  // 返回一个随机的汇率
  return Math.random();
};
```

### 测试代码
```javascript
// 从 Vitest 导入所需的函数
import { vi, it, expect, describe } from "vitest";
// 导入需要测试的函数
import { getPriceInCurrency } from "../src/mocking";
// 导入需要模拟的函数
import { getExchangeRate } from "../src/libs/currency";

// 模拟 "../src/libs/currency" 模块
vi.mock("../src/libs/currency")

// 定义一个测试套件
describe('getPriceInCurrency', () => {
  // 定义一个测试用例
  it('输入目标货币 应该返回price', () => {
    // 模拟 getExchangeRate 函数，使其返回 1.5
    vi.mocked(getExchangeRate).mockReturnValue(1.5)
    // 调用待测试的函数
    const price = getPriceInCurrency(10,"AUD");
    // 断言函数返回的价格是 15
    expect(price).toBe(15)
  }) 
})
```

### 详细解释

1. **生产代码部分**：
   - `getPriceInCurrency(price, currency)`：这个函数接受两个参数，一个是价格（`price`），另一个是目标货币（`currency`）。它首先调用 `getExchangeRate('USD', currency)` 获取汇率，然后返回转换后的价格。
   - `getExchangeRate(from, to)`：这个函数模拟了获取汇率的过程，它打印出一条消息并返回一个随机数作为汇率。

2. **测试代码部分**：
   - 从 Vitest 中导入了一些必要的函数（`vi`, `it`, `expect`, `describe`）。
   - 导入了需要测试的 `getPriceInCurrency` 函数和需要模拟的 `getExchangeRate` 函数。
   - 使用 `vi.mock` 函数模拟 `../src/libs/currency` 模块，以便在测试中控制其行为。
   - `describe` 定义了一个测试套件，`it` 定义了一个测试用例。
   - 在测试用例中，使用 `vi.mocked(getExchangeRate).mockReturnValue(1.5)` 来模拟 `getExchangeRate` 函数，使其返回固定的汇率 1.5。
   - 调用 `getPriceInCurrency(10, "AUD")`，预期返回的结果是 `10 * 1.5 = 15`。
   - 使用 `expect(price).toBe(15)` 断言返回的价格是 15。

### 总结
通过模拟 `getExchangeRate` 函数，测试代码能够控制其返回值，从而确保 `getPriceInCurrency` 函数在已知条件下运行。这使得测试更加可靠和可重复，而不受实际汇率或随机数生成的影响。



