
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












