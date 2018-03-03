1.介绍

函数式编程 与 面向对象编程 比较

引擎中的主要模式介绍

如何既确保架构优雅，又确保高性能


2.基础知识

- fp
- reason(only for example code knowledge, not whole knowledge!)
- webgl
references
(e.g.
https://reasonml.github.io/docs/en/quickstart-javascript.html
)


3.函数式编程相关模式

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







4.数据驱动相关模式

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








5.稳定性相关模式

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










6.异步相关模式


- 流
frp


application:
event: support pc event and mobile event
load asset




- 多线程
worker: frp + job + data driven


application:
multi thread render

multi thread logic:
collider,
...




- 综合应用

    - 基于frp的多线程







7.调试相关模式

- 通过log而不是断点调试


组合debug

- 日志分级

- 根据线上state json 恢复出错现场


- hot
hot change

hot load

...




- 综合应用











8.模块相关模式

- es6 module




- glsl module
glsl compiler:
support import glsl






- 综合应用
package size
build different package



rollup

compare es6 module, cmd/amd, namespace











9.扩展相关模式

- script component
- custom job
- custom material
- custom glsl

more...


- 综合应用







10.解耦相关模式

- 数据、逻辑分离

- job

- service

service->logic, data 分离

multi layer service




- Entity Component System

use int for gameObject,component instead of object





11.优化相关模式

- mutable operation
cache
share data(refer to state)

- texture cache
use texture for cache pre-computed data


application:
light map
normal map


- use gpu to compute instead of cpu


- 局部刷新(remove?)

any application?


- 差异化刷新(换个名字？)

application:
Set RenderTargetTexture->renderRate(render target update fps !== game loop fps)
shadow map update fps < game loop fps






- lod(remove?)


application:
billboard
swap geometry
swap gameObject



- defer


application:
defer shading
defer update transform
defer create vbo(e.g. if colors not be used, not create its vbo)
more?



- 多次剔除(这个名字不好，需要修改！)
先使用计算量小的方法来剔除大量数据，再使用计算量大的方法来剔除剩余数据


application:
cull
collider(先用aabb检测碰撞，再用多边形精确检测碰撞)


- batch(move into data oriented?no???)

application:
batch dispose
batch draw(instance)
merge
sort
last send buffer
vao
merge geometry
merge gameObject


- simd ?

- data oriented



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



application:
typearray pool
buffer pool


- 综合应用







12.渲染相关模式


- render command


- multi pass


application:
post processing
defer shading
shadow map






13.其他所有模式

- clone
share material/geometry






- procedural(remove???)
procedural texture 


voxel(remove from here?)
voxel terrain
voxel+polygon texture







- 综合应用








14.综合应用

- wonder.js架构原型
    - data driven+decouple(service, job, ...)+optimize(data oriented)

    - 基于data driven + frp 的多线程
