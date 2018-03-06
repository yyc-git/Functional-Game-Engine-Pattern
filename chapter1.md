一、基础知识


1. 介绍

介绍本书使用的模式推导思路
介绍《元素模式》中的思想和方法

函数式编程 与 面向对象编程 比较:
思维层面
应用场景
游戏引擎中(各自的优缺点)



引擎中的主要模式介绍

如何既确保架构优雅，又确保高性能

为了性能，进行取舍(即允许mutable):
允许非纯函数(但鼓励纯函数，禁止外部变量)
不使用容器




/*
本书定位层面：
(参考《我的架构思想》->序1)
聚焦在l1,l2，用l0应用

即聚焦在科学方法(模式)(l1)和方法论(原则)(l2);
然后给出案例，展示在实践(l0）中的应用
*/





函数式编程思想分析(简单说下就行了)：

定义函数:
    输入数据＋逻辑＋输出数据
函数是最基本的数据类型，可推出其它数据类型（number, string...)

分析函数式编程的组成结构：
信息?(
数据 和 逻辑 的本质可以统一为信息？
需要进一步研究和描述！！！
)->数据+逻辑->函数->各种数据类型(number, string...,  高阶函数)->语句(各种数据类型+控制逻辑(
控制逻辑就是函数

为什么？

控制逻辑=输入的数据+逻辑+输出数据=函数
))
-> 段落(花括号{}包含的区域) -> 大函数
(
大函数＝形参(输入数据)+段落(逻辑)+输出数据=函数
)

-> 模块(module)

-> 系统

-> 软件(更好的名字?)(多个系统集合)

-> 多个软件(可以以分布式来组织=互联网)

-> ...



/* 还是不要涉及的太广了，本书需要聚焦在游戏引擎上！


给出程序的等式：

算法 + 数据结构 = 程序
算法对应逻辑，数据结构对应数据？需要进一步思考！


函数式的视角来看:
程序 ＝ 信息 = 数据 + 逻辑 = 函数 ?

程序 = 数据 + 流动?(结合"数据流"原则？)




*/




////给出游戏引擎的等式:

游戏引擎 = 主循环 + job + service + pipeline?(再抽象一点？)

(在 综合应用 中，证明该等式？
即给出该等式在案例(引擎)中具体的对应？
)






////预测游戏引擎的发展趋势：
函数式编程是一个可行的方向！





2. 本书名词定义





3. 思想

提炼出模式之上的思想


数据、逻辑分离
数据流
管道处理(pipeline)
允许mutable
组合







4. fp基础
5. reason(only for example code knowledge, not whole knowledge!)基础
6. webgl基础

references
(e.g.
https://reasonml.github.io/docs/en/quickstart-javascript.html
)






二、基本模式

1. 提炼元素、设计空间

(只有具体实现，没有案例?)(没有模式变体???)

根据 对象相似度、对象类型相似度、方法相似度 来定义函数式编程中的EDP?
(这里 对象=module? 对象类型 = module 类型? 方法 = 函数?)

考虑module functor？



函数式编程的实体/元素：
数据 函数 模块 类型
(remove模块?)

游戏引擎相关的实体/元素：
时间 空间(////硬件)(CPU/GPU, 内存)(remove?) 

(可以给出 推出 这些元素 的思维过程. e.g. 先列出游戏引擎相关的实体概念，然后从中提炼出 时间、空间 元素)




依赖关系:
?


遍历每个依赖关系，在设计空间中识别出 本书需要用到的EDP



EDP = 实体 + 关系???

EDP(more!):
核心EDP(需要从实体之间的关系来推导):
提出"组合"EDP(对应"继承"EDP)?
or 提出"functor"EDP?(对应"继承"EDP)?
"Signature"EDP对应"抽象接口"EDP?


先看“函数调用”:

////分析 函数 与 模块 的相似度(不考虑 模块 类型?)
分析 函数 与 模块 与 模块 类型 的相似度


得出 "组合","递归","委托","内聚"等EDP?

////函数(未知)-模块(未知)




2. 推导EDP

EDP要分类
(参考 对象元素、类型关系、方法调用 三大类)



推出与下面类似的EDP?

- 函数是第一公民

high order function

no variable, use function to get variable

- 组合

- 柯西化

example:
unity function interface( by curry different param)
cache data(e.g. glsl draw, location...)

- 递归

尾递归优化

example:
editor->scene tree recurive instead of mutable operation


- 模式匹配

switch



- 不可变数据
- state
use record as state
immutable state
mutable state data for optimize
example:
redo_undo(immutable, mutable(copy))
- 数据为中心
关注数据流
管道处理


- 数据结构

tuple
record
list
array
more?



给出每个数据结构在引擎中的应用案例
(
e.g.
tuple: 将函数相关的形参放在一起成为一个tuple
)


- cps(remove ???)

https://www.ibm.com/developerworks/cn/java/j-contin.html



- module functor










三、一级模式

使用EDP来描述该模式


(只有具体实现，没有案例?)(没有或有很少的模式变体)

四、二级模式

使用EDP+一级模式来描述该模式

引擎中的EDP模式
(这个才有案例!!!???)(有多个模式变体及在引擎中的相关案例!!!)



## 推出下面类似的模式?

4.数据驱动相关模式

- 配置数据

store in json

example:
shaders

shader libs

////job



- 管道数据

extract pipeline data to json



example:
refer to function->compose














5.稳定性相关模式

- 回退

need detect environment

example:
instance(fallback to batch)
fallback to webgl1(if webgl2 not avaiable)
multi thread fallback(directly not use it?)
more...



- 测试

unit test

integration test

e2e test


example:
performance test
render test
integration with ci



- 契约设计















6.异步相关模式


- 流

frp


example:
event: support pc event and mobile event
load asset






7.调试相关模式

- 通过log而不是断点调试


组合debug

- 日志分级

- 根据线上state json 恢复出错现场(提出模式)


- hot

运行时修改/加载

hot change

hot load

热更新资源:

example:
hot update asset(游戏中热更新美术资源?)

...
















8.模块相关模式

- es6 module




- glsl module

glsl compiler:
support import glsl








package size
build different package



rollup

compare es6 module, cmd/amd, namespace
















10.解耦相关模式

- job

- microservice

https://martinfowler.com/articles/microservices.html#DecentralizedDataManagement
https://www.jianshu.com/p/39c1e4ec0d63



service->logic, data 分离

multi layer service


面向数据来切分服务

各个service相互独立，只操作自己的数据

each service logic should not duplicate



提出问题，给出答案


结合案例，采用迭代的方式来展现模式的演化，展示是如何一步步完善模式的！



为了解决各个service之间需要相互调用的情况(如gameObject包含了component，因此gameObject服务需要对应操作component服务), 提出个模块(取名为Combiner?Linker?Connector?ServiceMesh?)(叫composite service比较好，因为该模块就是负责组合多个service为一个大的service)来负责组合多个service的通用逻辑，但不属于service，应该属于service调用者所在的模块
调用者可依赖该模块，也可以直接调用service(相当于utils)
(e.g. GameObject->处理component的data的逻辑放在这里,而GameObjectJobService只负责处理gameObjectData)

////传入整个state到该模块？
把需要的各个service data传入？



为了解决“调用者不需要知道state中各个service data存在”的问题，提出facade层，即：
调用者->facade->service

把该逻辑放到facade中(参考编辑器)


如果调用者调用facade，会降低一些性能（
可能会增加拼装state的次数
）




为了解决service中重复代码，以及通用程度不同的问题，采用service分层




compare with:
component(ecs)
layer(editor)



好处：
service互不影响

显示定义定义了service api，明确了服务的概念:
Another consequence of using services as components is a more explicit component interface. Most languages do not have a good mechanism for defining an explicit Published Interface. Often it's only documentation and discipline that prevents clients breaking a component's encapsulation, leading to overly-tight coupling between components. Services make it easier to avoid this by using explicit remote call mechanisms.

数据相互独立(不再依赖整个state)



这些好处都要结合案例来说明！


缺点：
Moving code is difficult across service boundaries, any interface changes need to be coordinated between participants, layers of backwards compatibility need to be added, and testing is made more complicated.



- Entity Component System

use int for gameObject,component instead of object





11.优化相关模式

- mutable operation

cache
share data(refer to state)

- pre compute


example:
1.texture cache
use texture for cache pre-computed data

light map
normal map
render to texture


- use gpu to compute instead of cpu


- 局部刷新(remove?)

any example?


- 差异化刷新(换个名字？)

example:
Set RenderTargetTexture->renderRate(render target update fps !== game loop fps)
shadow map update fps < game loop fps






- lod(remove?)


example:
billboard
swap geometry
swap gameObject



- defer


example:
defer shading
defer update transform
defer create vbo(e.g. if colors not be used, not create its vbo)
more?



- 多次剔除(这个名字不好，需要修改！)

先使用计算量小的方法来剔除大量数据，再使用计算量大的方法来剔除剩余数据


example:
cull
collider(先用aabb检测碰撞，再用多边形精确检测碰撞)


- batch(move into data oriented?no???)

example:
batch dispose
batch draw(instance)
merge
sort
last send buffer
vao
merge geometry
merge gameObject


- ref data or copy data

example:
transfer data between workers




- 集群模式?

map reduce?
https://www.zhihu.com/question/23345991

将一个任务分散为多个子任务执行(并行？串行？异步？)，最后汇总结果


案例：
1.多线程

多线程的多个模型(每帧同步/不同步/...)
refer to https://www.gamasutra.com/view/feature/130247/multithreaded_game_engine_.php

more?




- simd ?

- data oriented



example:
shared array buffer for worker
skin animation
cull(use array instead of octree?)
particle
more...
- memory manage
dispose:
cpu memory (e.g. for gameObject)

(if move from arraybuffer, use mappedIndex?)



swap dispose






create:
create after dispose








- pool



example:
typearray pool
buffer pool







- tiled(提炼更抽象的模式？)





13.其他所有模式

- game loop(remove?)

duplicate with http://gameprogrammingpatterns.com/game-loop.html ?


- clone

share material/geometry



- 扩展
插入用户的逻辑到主循环中的各个阶段(job)中   



example:
script component
custom job
custom material
custom glsl

more...





- 多次变换(抽象出模式名！)



example:
transform->compute localToWorld matrix(multiply parent matrix)
model * view * project matrix transform
skeleton animation->compute position(multiply parent matrix)










- 切换gpu后端(webgl1, webgl2)(这是什么模式？提取出模式！)







## 参考下面类似的案例

- scene graph(需要提炼模式)

converter

.wd, .gltf



- 多线程

////worker: frp + job + data driven
(only use worker)


example:
multi thread render

multi thread logic:
collider,
...






    - 基于frp的多线程


- procedural(remove???提取出模式？)

procedural texture


voxel(remove from here?提取出模式？)
voxel terrain
voxel+polygon texture



12.渲染相关模式


- render command


- multi pass


example:
post processing
defer shading
shadow map
















五、三级模式

使用EDP+一级模式+二级模式来描述该模式

引擎中综合应用的模式
e.g. data driven render pipeline, frp+job的多线程, ...


推出下面类似的模式?

在引擎实际的架构设计中，应用多个引擎模式(二级模式)，展示模式应用场景的全貌

- data driven+decouple(service, job, ...)+optimize(data oriented)
- job架构实现

job + extend(custom job) + data driven
- 基于data driven + frp 的多线程
- data driven render:

custom pipeline for pc, mobile, pbr, ...
- more...
    



六、 附录
所有模式的PIN箱图
所有模式的p演算(remove?)