> # 选题报告

标签（空格分隔）： functional_3d_engine_pattern

---

# 申报选题名称
《函数式游戏引擎模式》


# 预计交稿时间和预计字数
2018.09

15w-20w

400页以内


# 关键字
游戏引擎 3d 函数式编程 模式





# 技术背景

- reason语言
- webgl环境




# 本书特色
## 开创新的领域
目前市面上只有关于游戏编程模式的书，还没有关于游戏引擎模式的书，更没有使用函数式编程的游戏引擎的相关书籍。

这是世界上该领域的第一本书！

## 聚焦在设计模式、架构，不涉及具体功能实现
设计和架构一直作者关注的重点，作者在这方面有很多经验。


## 每个章节相互独立，用户可以选择性的阅读，降低学习成本


## 实用性高
全部来自wonder.js引擎实战经验


## web版本完全免费


# 是否有相应的图书营销计划
试读online

众筹

自费出版


# 发布版本

## 免费
web版

## 收费
电子版
pdf版
纸质版(供收藏)(定位高端用户)





# 目标读者群

web or native developer(especially for web)

engine developer

game developer

architect

functional programming fans


# 读者能通过本书学到的内容：
学习游戏引擎的设计模式
学习函数式编程在游戏引擎中的应用




# 内容简介

本书介绍了使用函数式编程范式的游戏引擎中使用的各种设计模式


# 章节结构

- 目的
- 动机
- 模式思想
- 使用场景
- 模式实现方案
    - 方案1
    - 方案2
    - ...
- 比较各个方案优缺点，给出推荐的方案
- 案例
推荐方案的实际案例
使用基于reason的伪代码来说明
来源于wonder.js中的实际应用
- 总结
- 读者问答
- 更多资料推荐
- 读者评论


# 目录


1.介绍
fp vs oo
2.基础知识

- fp
- reason(only for example code knowledge, not whole knowledge!)
- webgl
references
(e.g.
https://reasonml.github.io/docs/en/quickstart-javascript.html
)


3.函数式编程模式

- 函数是第一公民
high order function

no variable, use function to get variable

- 组合

- 柯西化
application:
unity function interface( by curry different param)
cache data(e.g. glsl draw, location...)

- 递归
尾递归优化

application:
editor->scene tree recurive instead of mutable operation


- 模式匹配
switch



- 不可变数据
    - state
use record as state
immutable state
mutable state data for optimize
application:
redo_undo(immutable, mutable(copy))
    - 数据为中心
    
    关注数据流
    管道处理






- cps(remove ???)
https://www.ibm.com/developerworks/cn/java/j-contin.html





- 综合应用







4.数据驱动模式

- 配置数据

store in json

application:
shaders

shader libs

job



- 管道数据
extract pipeline data to json



application:
refer to function->compose

data driven render:
custom pipeline for pc, mobile, pbr, ...



- scene graph

converter

.wd, .gltf


- 综合应用








5.稳定性模式

- 回退
need detect environment

application:
instance(fallback to batch)
fallback to webgl1(if webgl2 not avaiable)
multi thread fallback(directly not use it?)
more...



- 测试

unit test

integration test

e2e test


application:
performance test
render test
integration with ci



- 契约设计




- 综合应用










6.异步模式


- 流
frp


application:
event: support pc event and mobile event




- 多线程
worker: frp + job + data driven


application:
multi thread render:

render command




application:
multi thread logic:
collider,
...




- 综合应用

    - 基于frp的多线程







7.调试模式

- 通过log而不是断点调试
debug info
debug panel

组合debug:
如果在 debug 组合的时候遇到了困难，那么可以使用下面这个实用的，但是不纯的 trace 函数来追踪代码的执行情况。

debug tool(remove)
webgl inspector
spector
...


- 日志分级

- 根据线上state json 恢复出错现场


- hot
hot change

hot load

hot ...




- 综合应用











8.模块模式

- es6 module


- module functor




- glsl module
glsl compiler:
support import glsl






- 综合应用
package size
build different package


rollup

compare es6 module, cmd/amd, namespace











9.扩展模式

- script component
- custom job
- custom material
- custom glsl

more...


- 综合应用







10.解耦模式

- 数据、逻辑分离

- job

- service

- Entity Component System

use int for gameObject,component instead of object





11.优化模式

- mutable operation
cache
share data(refer to state)



- batch(move into data oriented?)

application:
batch dispose


references:
batch draw(instance)
merge





application:
merge geometery
merge gameObject


- simd ?

- data oriented(move out from optimize to be single module?)
application:
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


- 综合应用











12.其他模式(remove?)

- clone
share material/geometry





////## integration with editor(move to editor book)




- ui(remove?)

2d ui

3d ui



- 综合应用








13.综合应用

- wonder.js架构原型
    - data driven+decouple(service, job, ...)+optimize(data oriented)

    - 基于data driven + frp 的多线程
