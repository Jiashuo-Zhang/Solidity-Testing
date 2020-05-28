# Testing for Ethereum Smart Contract: An Empirical Study 

**张家硕**

## 研究问题

1. 以太坊智能合约测试的发展现状
2. 以太坊智能合约的测试与通用高级语言的测试的异同
3. 以太坊智能合约测试存在的不足

## 研究过程

本研究选取了：

* 10个popular DApp：Aave, Bancor, Compound, DyDx, IDEX, Kyber, MakerDao, TokenMarket, Uniswap, bZx
* 3个区块链相关的通用高级语言编写的项目：Mythrill (in python), Truffle (in javascript), MakerDao-Market-Keeper (in python)

本研究对10个DApp中的Aave, Bancor, Compound, DyDx, Kyber以及3个高级语言编写的项目进行了定量分析，收集了各项目的测试覆盖度（包括Stmt Coverage, Branch Coverage, Function Coverage等）与代码复杂度（包括Cyclomatic complexity，Loc, SLoc等）等。本研究对所有的项目进行了定性分析，收集了各项目使用的CI、测试工具、是否进行代码审计、是否使用自动生成测试用例工具、是否使用形式化验证等信息。

本repo将会持续更新，追踪各个项目的进展与变化。

## 研究结果

### 智能合约测试发展现状

* 学术研究方面：
  * 程序测试方面，出现了一些针对智能合约与DApp的测试框架，Solidity IDE(如remix)与测试工具(truffle) 均被提出。
  * 程序分析方面，对于智能合约的各类安全漏洞的检测工具渐趋完备，相应的静态分析、动态分析、形式化方法和工具(如Oyente, Securify,EVM*等)均被提出，智能合约的安全问题得到初步的解决方案。
* 应用方面：
  * 已有的javascript测试工具正在被迁移到Solidity智能合约的测试中。通常的智能合约测试采用的是部署合约-发送交易-执行交易、验证结果的流程。其中部署合约、发送交易、验证结果都可以通过js脚本完成。其中，上述10个DApp程序分别使用：
    * Truffle：
    * Mocha：
    * builder：...
  * 对于测试充分度的评估，目前已有工具：solidity-coverage，其可集成到truffle和builder中，目前绝大多数的智能合约均使用solidity-coverage进行测试充分性评估。但是，solidity-coverage目前只有语句覆盖和分支覆盖的接口，更多更复杂的测试充分度还没有被实现。
  * 对于软件复杂度的评估，目前唯一的工具为solidity-metrics，其为VSCode中的插件，可以给出solidity代码的行数等统计信息，和控制流图、函数调用图等信息。其提供complex score为智能合约的复杂度打分，但是其没有实现通用的软件复杂度，不能给出类似Mccabe复杂度等的评价指标。

### 测试覆盖度

表格

### 代码复杂度

#### 代码复杂度的度量方式

智能合约的内生性的复杂导致常用的mccabe并不能很好的度量复杂度xxxxx

#### 代码复杂度表格

xxx

### 代码审计

提供代码审计的主要公司

代码审计的主要方面

10个DApp的定性分析

### 高级程序分析/测试技术

fuzzing

形式化。。。。



## 讨论

### 以太坊智能合约测试与常见高级语言测试的异同

* 对于测试覆盖度的要求
* 对于代码负责度的评估
* 代码审计
* 程序分析技术的应用

### 以太坊智能合约测试的不足

* 测试覆盖度评估工具与已有测试工具耦合性差，测试覆盖度准则单一
* 软件复杂度的定义与评估需要改进
* 前沿技术的应用滞后
* xxxxx