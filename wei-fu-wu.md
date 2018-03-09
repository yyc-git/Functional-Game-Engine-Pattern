参考资料

https://martinfowler.com/articles/microservices.html#DecentralizedDataManagement
https://www.jianshu.com/p/39c1e4ec0d63



# 模式名称

微服务

# 设计意图

阐明模式的设计目标

# 相关思想

面向数据来切分服务

将数据分层：
按照 数据粒度 来分层


数据与功能解耦合



函数即服务
( 
每个函数就是一个独立的服务，而不是每个.re文件(module)！
)


 
定义服务契约



# 设计动机

案例->editor:
使用前：
view,buss层与ui组件一一对应(与 功能?需求? 耦合)
区分了editor和engine(edit, oper, adapter)


使用后：
view,buss对应到api facade
edit, oper, adapter对应到service

数据与功能解耦合，调用方(
如引擎的job,editor的ui组件
)关注功能，service关注数据




# 组成结构

# 参与成员

# 协作关系


# 何时使用

## 适用条件

## 使用场景

## 优缺点
可参考 https://www.cnblogs.com/imyalost/p/6792724.html -> 八、优点和缺点

好处：
////service互不影响


数据与功能解耦合，调用方(
如引擎的job,editor的ui组件
)关注功能，service关注数据



显示定义了service api，明确了服务的概念:
Another consequence of using services as components is a more explicit component interface. Most languages do not have a good mechanism for defining an explicit Published Interface. Often it's only documentation and discipline that prevents clients breaking a component's encapsulation, leading to overly-tight coupling between components. Services make it easier to avoid this by using explicit remote call mechanisms.

不再所有逻辑都操作一个大的state，而是只关心与自己相关的数据
(结合分层 等来讨论)



这些好处都要结合案例来说明！


缺点：
Moving code is difficult across service boundaries, any interface changes need to be coordinated between participants, layers of backwards compatibility need to be added, and testing is made more complicated.



# 模式影响




# 具体实现

给出reason的伪代码

# 应用案例

引擎 案例

编辑器 案例

# 最佳实践


## 服务契约

TODO 研究三种契约

http://geek.csdn.net/news/detail/231684 -> 消费者驱动契约模式


## API Facade

/*
为了解决各个service之间需要相互调用的情况(如gameObject包含了component，因此gameObject服务需要对应操作component服务), 提出个模块(取名为Combiner?Linker?Connector?ServiceMesh?)(叫aggr service比较好，因为该模块就是负责组合多个service为一个大的service)来负责组合多个service的通用逻辑，但不属于service，应该属于service调用者所在的模块
调用者可依赖该模块，也可以直接调用service(相当于utils)
(e.g. GameObject->处理component的data的逻辑放在这里,而GameObject jobService只负责处理gameObjectData)

aggr service在新的层!和single service不在同一层!


////传入整个state到该模块？
把需要的各个service data传入？

*/


为了解决“调用者不需要知道state中各个service data存在”的问题，提出api facade层，即：
调用者->api facade->service

把该逻辑放到api facade中(参考编辑器)


如果调用者调用api facade，会降低一些性能（
可能会增加拼装state的次数
）


api facade类似于 微服务中的API Gateway :

https://www.cnblogs.com/savorboard/p/api-gateway.html





之所以引擎job直接使用service，而不使用api的原因：
1.这样性能更好
减少了组合state、从state中获得data的次数



之所以编辑器直接使用引擎的api，而不使用引擎的service的原因：
1.编辑器不关注性能

2.编辑器直接操作engine state，不操作engine state中的record


## 分层



为了解决service中重复代码，以及通用程度不同的问题，采用service分层:
可以往下跨层调用service
(这样子可以减少不必要的桥接代码)
(桥接是没有必要的，因为:
如果需要增加逻辑，则可以变为一个新的服务(操作同一个data的新的服务)
)
aggr service作为最上层service
(
all service module name should be XxxService.re instead of XxxAggrService.re, XxxCommonService
)


粗粒度层的服务可以互相调用
(操作state,record的service可以，操作单个数据的common/base service不行)






/*
什么逻辑放到下一层service中(如common service)?
1.本层service中重复使用的逻辑
2.操作更小的数据
(e.g.
camera->dirtyArray逻辑
)

如果函数是操作更小数据，但不是重复逻辑，则可作为私有函数
*/

如何判断service在哪层？
根据操作的数据粒度来判断
如：
操作多个state或者操作多个不同state的数据的service在一层
->
操作一个state或者一个state中多个数据的service在一层
->
操作state中某个数据的service在一层

e.g.
editor
要完成“dispose current gameObject”这个逻辑，需要操作(editorState, engineState)(
let editorState = editorState |> disposeCurrentGameObjectEditorService;
let enginenState = engineState |> disposeCurrentGameObjectEngineService;
)，这个逻辑应该放在state tuple这层，而不是分别调用state层这两个service



(
操作一个state并不意味者函数形参只有这一个数据，只是说函数只会改变这一个state。

"操作state中某个数据"同理
)





对于service分层
为什么同层service可以互相调用？

service内部为什么可以跨层调用?
因为针对的是不同粒度的数据



外部为什么可以跨层调用service?
因为对于外部来说，都是service(因此就没有aggr service, single service等区别)


为什么只允许上层调用下层service?
因为上层service才有下层service的数据， 而下层service没有上层service的数据

具体举例



具体案例是什么?
如record层的服务，针对同一个record操作的service之间可以互相调用






将数据分层：
按照 数据 粒度 来分层

tuple(state tuple) -> state -> record -> primitive -> atom

service的分层与数据分层一一对应



### 命名

////在不同的层，service的名字的抽象程度也不一样:

不同的层，service加上对应角色的后缀（不加数据类型的后缀！）

e.g.
在record层->gameObject record: XXXGameObjectService(不是XXXGameObjectRecordService!)
在state层->engine state(editor)，XXXEngineService(不是XXXEngineStateService!)



明确 角色、数据类型 的概念！



### 聚合服务与分层

本质上是因为数据之间有依赖关系，所以需要聚合服务。
e.g.
engine state中的gameObjectRecord 与 basicMaterialRecord之间有依赖关系，因此对应这两个record的service也有依赖关系，因此需要GameObject聚合服务(如dispose gameObject)
(需要进一步说明！)



聚合服务 参考：


https://www.cnblogs.com/savorboard/p/api-gateway.html -> 聚合服务

http://geek.csdn.net/news/detail/231684 -> 微服务的分解和组合模式




## 测试
测试代码如何写？
直接调用api facade，不调用service

测试的tool：
只需要API facade tool(不需要service tool)


每个测试文件(针对功能feature区分)的重复代码放到哪？:
////也微服务化？
////还是说保留 每个测试文件/功能 tool
(
对于editor:
测试分成：
1.ui component tool
////2.api facade tool
2. service tool


对于engine:
测试分成：
////1.api facade tool
1. service tool
)



## 反模式?







# 相关模式

与ECS, job的关系：
1.从数据的角度来看
service是从数据的角度来看，将数据分成多层
ECS是站在record层的抽象
job是站在record及以上层
(需要进一步分析!!!)


compare with:
component(ecs)
layer(editor)




# 模式变体

给出同位素的模式

说明变体的使用场景、何时使用等？
给出案例介绍？




# 扩展

推广(移到三级模式->job + microservice？)：
增加新的引擎(e.g. 物理引擎)， 有什么影响?
并行开发(job+api+service)
////每个引擎提供自己的(aggr service, )
不影响其它引擎开发
新引擎->共享/依赖其它引擎的service

针对此问题的解决方法：
////开发新引擎时，除了增加自己的service，其它依赖的service保持不变(就算他们更新了，也保持不变)
其它引擎的service的修改需要随时通知新引擎(持续集成)
(可以把新引擎与其它引擎都放在同一个project下)
(
或者新引擎为一个project A,其它引擎的service为一个project B;
A每天持续更新依赖的B的npm包
)



集成到主引擎中时成本很小:
只影响"新引擎->共享/依赖其它引擎的service"这部分






    
# 问答

问题相关的应用领域不限于游戏引擎，可推广至编辑器、前端等领域

# 总结





////# 设计空间(EDP模式专有)


# 更多资料推荐


# 习题


