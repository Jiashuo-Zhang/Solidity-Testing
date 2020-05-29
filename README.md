# Testing for Ethereum Smart Contract: An Empirical Study 

**张家硕 PKU2020春 软件测试导论课程大作业**

## 研究问题

1. 以太坊智能合约测试的发展现状
2. 以太坊智能合约测试与通用高级语言测试的不同
3. 以太坊智能合约测试存在的不足

## 研究背景

* 以太坊：以太坊是目前最为流行的支持智能合约的区块链平台，其市场总额已达到200亿美元以上。
* 智能合约：智能合约本质上是一个程序，智能合约通常在区块链平台上，在特定的虚拟机中运行，以完成复杂的功能（如数字资产的转移等）。
* Solidity：Solidity是以太坊智能合约采用的编程语言，是目前最为流行的智能合约编程语言之一，目前针对Solidity有很多安全方面的研究。
* DApp：DApp是Decentralized Application的简称，以太坊上的DApp通常以以太坊上智能合约为后端，以web为前端，与用户进行交互。
* 智能合约安全问题：
  * 以太坊上智能合约曾经发生过许多次严重的安全问题，造成了巨大的损失。如2016年6月，The DAO合约遭到重入攻击，损失约5000万美元，最终导致以太坊硬分叉。2017年7月parity钱包合约漏洞遭到攻击，导致损失近3000万美元。2018年4月，BeautyChain智能合约遭到整数溢出攻击，约10亿美元市值蒸发。
* 智能合约分析与测试：
  * 由于智能合约安全问题频发，智能合约的分析与测试受到广泛重视，研究中，许多漏洞检测工具与测试框架被提出。

## 研究过程

**本研究选取了**：

* 10 popular DApps：Aave, Bancor, Compound, DyDx, IDEX, Kyber, MakerDao, TokenMarketNet, Uniswap, bZx (本研究使用的是这些DApp的链上智能合约部分)
* 3个区块链相关的通用高级语言编写的项目：Mythrill (python), Truffle (javascript), MakerDao-Market-Keeper (python)

**本研究主要使用以下测试工具**：

* Truffle：A world class development environment, testing framework and asset pipeline for blockchains 
* Builder： A task runner for Ethereum smart contract developers
* Solidity-coverage：Code coverage for Solidity smart-contracts
* Solidity-metrics：Generate Solidity Source Code Metrics, Complexity and Risk profile reports for Solidity smart-contracts
* Pytest: A mature Python testing tool
* Radon:  A Python tool that computes various metrics from the source code
* Mocha: A JavaScript Testing Framework
* Jest:  AJavaScript Testing Framework
* Complexity-Report:  Software complexity analysis for JavaScript projects.

本研究对上述大部分项目进行了定量分析，收集了各项目的测试覆盖度（包括Stmt Coverage, Branch Coverage, Function Coverage等）与代码复杂度（包括Cyclomatic complexity，Loc, SLoc等）等，由于各项目所使用的测试工具等对于测试覆盖度评估的支持不同，不同项目可能使用不同的测试覆盖度准则进行评估。本研究对所有的项目进行了定性分析，收集了各项目使用的CI、测试工具、是否进行代码审计、是否使用自动生成测试用例工具、是否使用形式化验证等信息。

本repo将会持续更新，追踪各个项目的进展与变化。

## 研究结果

### 智能合约测试发展现状

* 学术研究方面：
  * 程序测试方面，出现了一些针对智能合约与DApp的测试框架，如remix(solidity ide), Truffle(solidity 测试框架)
  * 程序分析方面，对于智能合约的各类安全漏洞的检测工具渐趋完备，相应的静态分析、动态分析、形式化方法和工具(如Oyente, Securify,EVM*等)均被提出，智能合约的安全问题得到初步的解决方案。
* 应用方面：
  * 通常的智能合约测试采用的是部署合约-发送交易-执行交易、验证结果的流程。其中部署合约、发送交易、验证结果都可以通过js脚本完成。其中，上述10个DApp程序分别主要使用以下测试工具：
    * Truffle：Aave, Bancor, DyDx, bZx
    * Mocha：Uniswap
    * Builder：Kyber
    * Jest: Compound
    * pytest: TokenMarketNet
    * Unknown: IDEX, MakerDao
  * 对于测试充分度的评估，目前已有工具：solidity-coverage，其可集成到truffle和builder中，目前绝大多数的智能合约均使用solidity-coverage进行测试充分性评估。但是，solidity-coverage目前只有语句覆盖和分支覆盖的接口，更多更复杂的测试充分度还没有被实现。
  * 对于软件复杂度的评估，目前唯一的工具为solidity-metrics，其为VSCode中的插件，可以给出solidity代码的行数等统计信息，和控制流图、函数调用图等信息。其提供complex score为智能合约的复杂度打分，但是其没有实现通用的软件复杂度，不能给出类似Mccabe复杂度等的评价指标。

### 测试充分性

#### 各项目测试充分性

|        Project         |  Language  | Stmt Coverage | Branch Coverage |
| :--------------------: | :--------: | :-----------: | :-------------: |
|          Aave          |  Solidity  |     93.8%     |      76.6%      |
|         Bancor         |  Solidity  |     95.9%     |      83.3%      |
|          DyDx          |  Solidity  |    100.0%     |     100.0%      |
|         Kyber          |  Solidity  |    100.0%     |      95.4%      |
| MakerDao-Market-Keeper |   Python   |     14.0%     |      2.6%       |
|        Mythrill        |   Python   |     65.0%     |      85.2%      |
|        Truffle         | Javascript |     76.2%     |      65.3%      |

可以看到，智能合约项目的覆盖度是都处在较高水平。这主要是由于智能合约与数字资产的转移等密切相关，因此社区对智能合约测试充分性的重视程度较高。

#### 测试覆盖度度量工具单一

目前solidity只有一个成熟的测试覆盖度评估工具：solidity-coverage, 其官方只支持作为truffle与builder的插件。这导致已有的各种测试框架难以有效对solidity智能合约的测试覆盖度进行度量。

#### 测试充分性准则单一

同时，测试solidity-coverage的给出的覆盖度仅仅有语句覆盖与分支覆盖，大多数的DApp在测试过程中只关注语句覆盖这一个测试充分性准则，这种测试充分性准则的单一不利于提高测试充分性。

### 代码复杂度

#### 代码复杂度的度量方式

目前，没有工具实现Solidity项目中的Mccabe复杂度等复杂度度量，这主要有以下2个原因：

* 目前Solidity还在发展初期，各种工具还有很大发展空间
* Solidity语言的复杂性更多的来自于其内生的复杂性（如其transfer, send, delegate call等指令），传统的mccabe复杂度度量等并不能直接应用于Solidity语言的度量。

目前，在Solidity的度量方面，只有一个可用的度量工具：solidity-metrics，作为VSCode的插件使用。其提供LOC，SLOC等较为基础的复杂度评估，以及提供一个初步的complexity score（基本原理为给各个语句赋权重），以反映Solidity的复杂性。

#### 代码复杂度评估

**本项目选择的所有10个DApp在开发过程中，都没有进行代码复杂度的度量。**

以下是本项目使用solidity-metrics与radon对各项目进行度量的结果，None代表工具不能给出相应的代码复杂度。

| Project               | Language | Loc   | SLoc  | Complexity Score(Sum) | Cyclomatic complexity(per file) |
| --------------------- | :------: | ----- | ----- | :-------------------: | :-----------------------------: |
| Aave                  | Solidity | 6948  | 6285  |         2094          |              None               |
| Bancor                | Solidity | 6197  | 5593  |         2482          |              None               |
| Compound              | Solidity | 7641  | 7258  |         2868          |              None               |
| DyDx                  | Solidity | 13520 | 10825 |         3165          |              None               |
| Kyber                 | Solidity | 7116  | 6043  |         3712          |              None               |
| MakerDao-Maket-Keeper |  Python  | 10081 | 6495  |         None          |              9.65               |
| Mythrill              |  Python  | 17724 | 11105 |         None          |              9.82               |

### 代码审计

在Solidity项目的整个开发流程中，有一项独特的流程，即代码审计。通常在一个版本发布前，开发团队会寻找一个或多个第三方机构进行代码审计。代码审计的主要内容包括评估代码安全性与正确性、提出安全漏洞，代码规范、缺陷处理过程的追踪等。

在我们选择的10个DApp中，Aave, Compound, DyDx, MakerDao, Kyber, Uniswap 6个DApp使用了代码审计。他们分别使用的代码审计团队为：

* Trails of Bits: Aave, Compound, MakerDao
* Zeppelin: Aave, Compound, DyDx
* Bramah Systems: DyDx
* BlockchainLabs: Kyber
* ChainSecurity: Kyber
* Sai: MakerDao
* PeckShield: MakerDao
* DApp.org: Uniswap

### 高级程序分析/测试技术

目前在DApp测试的过程中，高级程序分析/测试技术没有得到很好的应用。在测试阶段，绝大多数DApp没有使用（或没有显式的使用）已有的fuzzing、符号执行等分析工具。

值得一提的是，在代码审计阶段，在10个DApp中，Compound，Uniswap使用了形式化验证技术。同时，代码审计机构Trails of Bits在审计过程中，使用了Fuzzing工具。

## 总结

### 以太坊智能合约测试与常见高级语言测试的不同

* 对于测试充分性的要求不同。
  * 由于智能合约涉及到数字资产的转移等操作，智能合约的安全性受到广泛重视，测试覆盖度成为重要的指标。
* 对于代码复杂度的评估不同。
  * 这主要是Solidity语言内生的复杂性导致的。也是由于智能合约还在初级阶段导致的。
* 代码审计得到广泛应用。
  * 专业安全团队的审计成为DApp安全的最后一道防线。

### 以太坊智能合约测试的不足

* 测试充分性评估

  * 评估工具与已有测试工具耦合性差
  * 测试充分性准则单一

* 软件复杂度评估

  * 软件复杂度需要更加准确的评估方法
  * 软件复杂度度量没有得到应用

* 测试过程复杂，测试工具功能有限

  * 测试过程需要部署合约-发送交易-执行交易-验证结果等流程，通常需要部署测试链，导致测试环境的搭建过程非常繁琐，缺乏有效的测试工具来减少这一困难。

* 前沿技术的应用滞后

  * 测试的主要环节依旧是最为基础的单元测试，前沿的安全与测试工作很少得到使用。

  