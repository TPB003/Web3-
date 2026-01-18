# Remix 使用教程

# Remix IDE 全图解

欢迎来到 Remix！这里是你编写第一个智能合约的地方。

请在浏览器打开：https://remix.ethereum.org，也可以直接下载客户端

*(初次打开如果弹出欢迎窗口，直接点击 "Accept" 或 "Next" 关闭即可)*

## 🧭 第一部分：熟悉你的“驾驶舱”

Remix 的界面看起来按钮很多，但作为新手，你只需要关注 **三个核心区域**：

### 1. 左侧工具栏 (核心操作区)

这是最左边那细长的一排图标，我们只用前三个：

![image-20260118170928995](C:\Users\99350\AppData\Roaming\Typora\typora-user-images\image-20260118170928995.png)

- 📂 **File Explorers (文件管理器)**：第一排图标。用来新建文件、管理文件夹。

![image-20260118171005487](C:\Users\99350\AppData\Roaming\Typora\typora-user-images\image-20260118171005487.png)

- 🔌 **Solidity Compiler (编译器)**：第三排图标（像个 S 形插头）。用来检查代码有没有写错，并翻译成机器语言。

![image-20260118171031185](C:\Users\99350\AppData\Roaming\Typora\typora-user-images\image-20260118171031185.png)

- 🚀 **Deploy & Run (部署与运行)**：第四排图标（以太坊 Logo + 播放键）。用来把合约发到链上，并进行交互。

### 2. 中间代码区 (案板)

![image-20260118171248195](C:\Users\99350\AppData\Roaming\Typora\typora-user-images\image-20260118171248195.png)

这里是你写代码的地方。

### 3. 底部控制台 (日志区)

最下面的一小条黑框。这里会显示系统给你的反馈。

![image-20260118171326009](C:\Users\99350\AppData\Roaming\Typora\typora-user-images\image-20260118171326009.png)

- **绿色对钩** ✅：成功了！
- **红色叉叉** ❌：报错了，需要修改。

## 🛠️ 第二部分：四步走完一生 (编写-编译-部署-交互)

让我们通过一个真实的流程，来体验智能合约的生命周期。

### 第 1 步：新建文件 (Create)

![image-20260118171546706](C:\Users\99350\AppData\Roaming\Typora\typora-user-images\image-20260118171546706.png)

1. 点击左侧第一个图标 **📂 (文件管理器)**。
2. 点击 `contracts` 文件夹。
3. 点击上方的小白纸图标 **(Create New File)**。
4. 输入文件名：`Storage.sol`，回车。

### 第 2 步：编写代码 (Code)

将以下代码复制粘贴到中间的编辑器里。这是一个最简单的“存钱罐”合约：

Solidity

`// SPDX-License-Identifier: MIT pragma solidity ^0.8.0;

contract SimpleStorage { // 这个变量用来存一个数字 uint256 public myNumber;

```
// 写入函数：把数字存进去 (要花 Gas)
function store(uint256 _num) public {
    myNumber = _num;
}

// 读取函数：把数字读出来 (免费)
function retrieve() public view returns (uint256) {
    return myNumber;
}
```

}`

### 第 3 步：编译代码 (Compile)

代码是给人看的，我们要把它变成机器能懂的 Bytecode。

![image-20260118171646269](C:\Users\99350\AppData\Roaming\Typora\typora-user-images\image-20260118171646269.png)

1. 点击左侧第三个图标 **🔌 (Solidity Compiler)**。

2. 关键设置

   ：

   - `Compiler`: 只要版本号（比如 0.8.26）大于等于代码里的 `0.8.0` 就可以。通常默认即可。
   - `Auto compile`: **强烈建议勾选**。这样你每敲一个字，它都会自动检查错误。

3. 点击蓝色的 **Compile Storage.sol** 按钮。

4. **成功标志**：左侧图标上出现了一个绿色的对钩 ✅。

### 第 4 步：部署与交互 (Deploy & Interact) —— **最重要的一步**

点击左侧第四个图标 **🚀 (Deploy & Run)**。这里的信息量有点大，我们逐一拆解：

![image-20260118171728785](C:\Users\99350\AppData\Roaming\Typora\typora-user-images\image-20260118171728785.png)

### A. 部署面板设置

- Environment (环境)

  : 选择 

  ```
  Remix VM (Cancun)
  ```

   或 

  ```
  London
  ```

  。

  - *解释*：这是一个在浏览器内存里跑的“假区块链”。速度极快，不需要真钱。

- Account (账户)

  : Remix 送了你 15 个测试账号，每个里面有 100 ETH。

  - *解释*：你可以随意切换账号，假装自己是不同的用户。

- **Contract (合约)**: 确保这里选中的是 `SimpleStorage`。

### B. 点击部署

- 点击橙色的 **Deploy** 按钮。
- **观察底部控制台**：会出现一行绿色的字，说明部署成功。
- **观察左侧下方**：`Deployed Contracts` 栏目下，会出现一个新的条目 `SimpleStorage`。

### C. 开始玩耍 (交互)

![image-20260118171819813](C:\Users\99350\AppData\Roaming\Typora\typora-user-images\image-20260118171819813.png)

点击 `SimpleStorage` 左边的小箭头 `>` 展开它，你会看到两个按钮：

1. store (橙色按钮)：
   - 在旁边的框里输入一个数字，比如 `888`。
   - 点击按钮。
   - *解释*：这是一个**写操作**。你会看到控制台有日志滚动，这是模拟了一次“交易”。
2. retrieve (蓝色按钮)：
   - 直接点击按钮。
   - 下方会显示：`0: uint256: 888`。
   - *解释*：这是一个**读操作**。它瞬间就返回了结果。

## 🎨 第三部分：小白必知的“颜色密码”

在 Remix 的交互面板里，按钮的颜色代表了极重要的含义，这能帮你理解以太坊的计费逻辑：

| **按钮颜色** | **含义**      | **专业术语**    | **是否花钱(Gas)?** | **是否需要确认?**      |
| ------------ | ------------- | --------------- | ------------------ | ---------------------- |
| **🔵 蓝色**   | **查** (只读) | `view` / `pure` | **免费** 🆓         | 瞬间返回，不用等       |
| **🟠 橙色**   | **改** (写入) | Transaction     | **付费** 💸         | 需要矿工打包，需要等   |
| **🔴 红色**   | **付** (转账) | `payable`       | **付费+转账** 💰    | 既执行代码，又接收 ETH |

> 给小白的记忆口诀：
>
> 蓝色随便点，橙色要花钱，红色是打钱。

## ⚠️ 第四部分：常见坑点与急救包

在使用 Remix 时，实习生 100% 会遇到以下问题：

**Q1: 我刷新了一下网页，代码全没了！**

- **真相**：Remix 默认把代码存在浏览器的缓存里。如果清理缓存，代码就丢了。
- **解法**：养成好习惯，重要的代码要复制保存到本地电脑，或者使用 Remix 里的 "Connect to Localhost" 功能（进阶）。

**Q2: 部署按钮是灰色的，点不动？**

- **原因**：通常是因为编译没通过（代码有红色的报错），或者右边正在编译中。
- **解法**：回到 Compiler 页面，看看有没有红色的错误提示。修好 bug 才能部署。

**Q3: 我想把合约部署到测试网（比如 Sepolia）甚至主网，怎么做？**

- **解法**：在 `Environment` 里，把 `Remix VM` 切换成 **`Injected Provider - MetaMask`**。这时 Remix 就会连接你浏览器里的小狐狸钱包，用你钱包里的真（测试）币来部署。

## 🎓 课后小挑战

为了确认你已经上手了，请完成以下任务：

1. **修改代码**：在 `SimpleStorage` 合约里增加一个函数，能够把存进去的数字 `+1`。

```solidity
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SimpleStorage {
    // 这个变量用来存一个数字
    uint256 public myNumber;

    // 写入函数：把数字存进去 (要花 Gas)
    function store(uint256 _num) public {
        myNumber = _num;
    }
    // 新增函数：在原有基础上 +1
    function increment() public {
        myNumber = myNumber + 1;
    }
    // 读取函数：把数字读出来 (免费)
    function retrieve() public view returns (uint256) {
        return myNumber;
    }
}
```



1. **重新部署**：别忘了，改了代码必须**重新编译**并**重新部署**。旧的合约是不会自动更新的！

2. 多账号互动：

   ![image-20260118172235454](C:\Users\99350\AppData\Roaming\Typora\typora-user-images\image-20260118172235454.png)

   ![image-20260118172329250](C:\Users\99350\AppData\Roaming\Typora\typora-user-images\image-20260118172329250.png)

   - 用 **Account A** 部署合约。
     - 部署者是谁不重要
     - 合约地址一旦生成，**对全世界公开**
   - 用 **Account A** 存入数字 `100`。（store(100)）
     - 一笔交易被发到链上
     - `myNumber` 被写进合约的存储区
     - 状态被所有节点同步
   - 在左侧上方切换到 **Account B**。
     - 只发生的变化：**交易的发送者地址变了**。合约地址没变，合约状态没变。
   - 用 **Account B** 读取数字。（retrieve()）
     - myNumber` 从 `100` 变成 `101
     - Gas 由 Account B 支付
     - Account A 再读，看到的也是 `101`
   - *思考：为什么 Account B 能读到 A 存的数据？（因为数据在链上，是公共的）*

   其实就是：**合约状态属于合约，不属于某个账户。**

