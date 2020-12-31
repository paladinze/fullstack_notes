# Testing

## Types of tests

- unit test: testing one isolated function, or one React component

  - Enzyme’s shallow() is a unit test.

- integration test: testing an entire React component including children components.

  - Enzyme’s mount() is an integration test.

- Mock function: Redefining a function specifically for a test to generate a result. E.g.
  - prevent the hard-coded sum issue we were discussing earlier!
  - Mock functions can be defined in jest with jest.fn(() => { //function here });.

## test terminology

- Smoke test: Verifies that a component renders without throwing.
  - Utilising Enzyme’s shallow() is indeed a smoke test, as is mount().
- Shallow rendering: rendering a component with no children.
  - Enzyme’s shallow() is a form of shallow rendering, whereas mount() is not.
- Full rendering: Rendering a component and all of its children.
  - mount() is a full rendering method whereas shallow() is not.
- Static rendering: Rendering components to static HTML files and then analysing the results.
  - Enzyme’s render() method is used for static rendering.

## Approach
- TDD: test first testing
- BDD: function first testing

## 黑盒测试和白盒测试
- 黑盒测试：测试功能
- 白盒测试：测试内部逻辑


## 测试种类
- 单元测试
- 集成测试
- 契约测试：
    - 三方依赖多的项目
- 端到端测试：关注业务验收点
    - 业务场景多、复杂或经常回归的场景

## 为什么必须做单元测试

- 带来对软件正常运行的自信
- 避免加功能引入新 BUG
- 使开发者从调用者的角度观察和思考
- 可编译、可运行的文档，并且它保持最新，永远与代码同步。

## 不写单元测试的后果
- 每次发布都要通过人力测试
- 不敢随意重构
- 复杂度使得你的开发速度降低

## 单元测试的核心灵魂是TDD
- 使用TDD开发方法是得到可靠单元测试的唯一途径
- 由开发者写
- 内建的，而不是后补的

``` js
// production code
const computeTotalAmount = (products) => {
  return products.reduce((total, product) => total + product.price, 0); 
}

// testing code
it('should return summed up total amount 1000 when there are three products priced 200, 300, 500', () => {
  // given - 准备数据
  const products = [
    { name: 'nike', price: 200 },
    { name: 'adidas', price: 300 },
    { name: 'lining', price: 500 },
  ]

  // when - 调用被测函数
  const result = computeTotalAmount(products)

  // then - 断言结果
  expect(result).toBe(1000)
})
```

## 单元测试编写原则
- 只关注输入输出，不关注内部实现
- 只测一条分支
- 表达力极强
- 不包含逻辑
- 运行速度快


## 为什么需要单元测试
写代码之前需要用单元测试来驱动设计和开发。（自认为能用大脑驱动出来好代码的人可以不用考虑）
完成代码之后需要用单元测试是为了在多人开发的情况下能放心做refactor或者修改了功能代码。（自认为做了refactor和代码修改之后一定不会有side effect，并且前提是永远都是你来维护这些代码，并且你很久之后再来修改还要能保证没有side effect，那我觉得就没有必要写）
基于以上一个或者两个前提是yes的情况下，首先得到的结论是要做自动化单元测试。那么对于有了（功能和接口的）自动化测试，为什么要做Unit Test？
首先，自动化（功能和接口的）自动话测试很难做到很高的coverage（我在当前的纯API项目里面也只能把接口级别的自动化测试勉强做到AC Cover 50%左右，估计值），其次执行效率很慢。基于这两点，开发就很难在本地用（功能和接口的）自动化测试自查自纠自己代码修改后的side effect，首先coverage不够，所以不够放心，其次执行时间长，需要等待很多时间（小项目还好，越大的项目这个问题越严重）。所以为了增加信心，减少side effect，加快后期refactor和修改代码的开发效率，是需要写单元级别的自动化测试的。

Unit Test是完成小粒度单元级别的检查，举个例子来讲（当然如果能够在GovTech下找到个更好的符合业务的语境就更好）。在实际生活中，我要到某某部门办一个业务，而这个业务需要提交一系列的小表格，然后进行政府长达一周的审批，审批时候要求每个表格需要各种数字对上号，否则会被打回。试想，如果在提交表格之前没有一张一张的进行检查，直接填好了就上交，最后提交到政府的时候，会因为各种问题打回，而且还需要自己从头重新检查知道错误在哪里（类似集成测试或者E2E测试）。这样耽误的时间就非常的多，非常的低效。

那么更好的做法是把自己每填写一个表格，就进行反向计算（对应测试），确保每个小表格正确；更好的话还可以找个人一起做（Pair）。

反正我觉得，用生活中的例子来解释，会更容易理解。



如何用一个比喻来理解单元测试？
如果软件工程好像汽车制造的话，单元测试就好比对每个汽车零件做单独的测试。这么做的好处是确保每一个小的模块都按照预想的规格或规范在运行，从而确保软件的整体质量。

我们已经有QA对每次开发的新功能进行测试，那岂不是相当于模块测试，为什么还需要单元测试？    
在软件开发过程中，我们的代码库是共享的。并且在开发过程中，软件的设计会频繁的变更。这就意味着每个dev都有可能在开发自己模块的时候修改到别的模块。由开发人员负责编写的单元测试在这种场景下是一种保护机制。

我们的QA做回归测试是不是足够保障质量？我们的回归测试还可以自动化。
首先，回归测试想要覆盖所有的功能细节工作量是很大的，对于一个团队开发人员多于测试人员的配置情况下几乎不可能，即使编写自动化脚本其工作量也极大，且难以维护。单元测试由开发人员负责，是成本小，收益大的测试策略。
其次，单元测试是开发人员设计代码过程中的帮手，可以为开发人员重构代码，改善软件内部设计提供支持。


## React 测试策略
* action：一般不需要测
* reducer: 有逻辑的需要100% 覆盖
* selector：有逻辑的需要100% 覆盖
* saga（副作用）：参数，API，数据，业务分支逻辑，异常逻辑五个层面要求100%覆盖率
* utils 层的纯函数要求 100% 覆盖

### 组件层：
* 分支渲染逻辑必测
* 事件、交互调用要求100%覆盖；
* connect 过的高阶组件不测
* 纯 UI 一般不测

## Mobile testing
- install and uninstall
	- android
		- official tool: adb (android debugger bridge)
		- install and update test: cukeTest
	- iOS
		- idb
- stability test
	- android
		- monkey tool
			- simulate touch nav motion events at specified freqency
- app crawler
- unstable internet testing
	- tool: chalers
	- speed throttling
	- reconnect mechanism
	- prompt user to switch better network environment
- performance test
	- all-in-one tool (recommanded)
		- SoloPi (alipay)
		- PerfDog (tencent)
	- cpu: adb dumpsys
	- memory
		- shaking
		- memory keep increasing
		- frequent gc
	- network : tcpdump / wireshark
	- battery; adb Battry historian
	- rendering fps: adb
	- apk size
		- google apk analyzer
		- wechat Matrix
	- reference performance baseline: green software alliance (huowei)
	- compatbility test: testin


The goal for mocking is to replace something we don’t control with something we do
mock function 
	Capture calls
	Set return values
	Change the implementation


## React Testing library
getby
		get something that exists
	getByRole
		use element's default role as hint
	queryby
		asserting that an element isn't there
	findby
		aysnc query
test user event
	fireEvent / userEvent


