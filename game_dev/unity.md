# Unity

## questions
- what is draw calls
- how to measure framerates

## game challenges
- 超级坦克大战
- block breaker
  - revive the block breaker game
- tower defense
  - reverse engineer the bought package and build a TD game
- rocket booster
- tetris
- racing
- pong
- snake
- flappy bird
- t-rex runner
- 别踩白块儿
- 微信飞机大战
- 扫雷游戏
- 打地鼠游戏
- 青蛙过河游戏
- 激光圈
- 超级马里奥 (super mario)
- 吃豆人
- 宝石迷阵
- 植物大战僵尸
- 塔防游戏
- missle commander
- 找Asset Store上面的完整工程，找自己感兴趣的开始复刻

## Prequisites
- 数学知识
  - 向量，欧拉角，四元数，矩阵，
  - 向量的加减法点乘差乘
  - 空间解析几何
  - 线性代数
  - 数学分析微积分部分
  - 数值逼近解法
- 物理知识
  - 刚体力学
  - 运动学定律
  - 数理方程
- C#语言基础
  - 基本数据类型, 语法
  - 委托与事件
  - 常用设计模式
  - 单例模式
  - 泛型
  - 线程
  - 网络编程

## Unity Learning Pathway
- 熟悉Unity的界面 (user Interface)
  - 层次视图 (hierachy view)
  - 项目视图 (project view)
  - 属性视图 (inspector view)
- 熟悉Unity的目录结构 (directory structure)
  - Sprite, Scripts, Prefabs
  - 资源管理
    - 模型，网格，材质，贴图，动画，数据表，配置表
    - 编辑器扩展，AssetBundle
- 创建场景的一些基本概念 (Scene)
  - 游戏对象 (game object)
    - 预制体 (prefab)
    - 标签 (tag)
    - 层面 (layer)
    - 时间
  - 组件 (component)
  - 脚本 (script)
    - Mono Behaviour生命周期
      - Start
      - Update
  - 坐标系统
    - 向量概念
    - 世界坐标 vs 局部坐标
    - 移动，缩放，旋转
  - 输入系统
- 引擎系统的基本组件 (game engine)
  - 渲染 (rendering)
    - shader
    - 渲染管道
    - 粒子系统
  - 摄像机
  - 灯光
  - 地形
  - 物理 (physics)
    - 碰撞 (collision)
  - AI (AI)
    - 寻路 (path finding)
    - 行为树 (decision tree)
  - 音频 (audio)
  - 动画 (animation)
  - 加载和IO (IO)
  - 网络通信
  - 文件系统 (file system)
  - 内存管理 (memory management)
  - 多线程架构 (thread management)
- 游戏逻辑 (gameplay)
  - UI
  - FSM
  - 全局玩法流程逻辑
  - 技能系统
  - 武器
  - 升级
  - 装备
- 工具
  - 流程化插件
  - 编辑器功能
  - 便利性需求
  - 自动化构建版本工具
- Unity packages
  - UGUI, Lua，NGUI
  - odin
  - playmaker

## design steps
- core
  - set up camera
    - aspect ratio
    - canvas resolution
  - player
    - movement
    - shooting
    - health
  - enemy
    - movement
    - sqawn waves
    - health
- secondary
  - score
  - shooting
- polish
  - visual effects
  - sound effects
  - menu / screen
  - content / tuning



## data structures in games

- 堆栈的应用：
  - 比如进入设置菜单时候把新菜单压栈操作
  - 返回时候出栈销毁即可。
  - 在游戏场景进入到一个房间时候可以把当前游戏场景暂停然后把新的房间场景压栈。

- 队列的应用
  - 在一些需要缓冲输入时候（比如格斗游戏）可以使用队列来控制输入操作。
  - 在一些技能系统比如一回合有8个体力槽玩家来组合攻击。
  - 在制作回放系统时候也可以使用队列来制作。

- 树的应用：
  - 基本是当你需要面对分支而且每个分支都有分支时候需要考虑。
  - 典型的比如剧情或者对话树，在节点下有很多子物体，子物体又可以有很多子物体时候

- 图的应用：
  - 在可视化流程控制，有限状态机和导航系统都可以找到它的影子

## Concepts
- Actors
- Controllers
- Characters
- Game Modes
- Game States
- Levels
- Collisions
- Animation sequences
- Static meshes
- Skeletel meshes
- rigid body
- collision detection

## gameplay and engine books
* 游戏编程算法与技巧
* 游戏编程模式
* 游戏引擎架构
* realtime rendering 3rd
* Fundations of physically based modelling

## game engines
- AAA game: unreal
- indie 3D: unity
- indie 2D: unity / godot
- indie 2D with no dev: rpgmaker

## art tools
- Autodesk Sketchbook
- 2D art: KRITA
- 2D vector art: Inkscape
- SFX: LMMS
- UDM Paint (64 bit version)
  - License Key / Serial Number: UPLN91-8VK8HA-C72YUL-XA2LRY-8CYYOK
- Corel Painter Essentials 7
  - License Key / Serial Number: PE07B22-WZT96G3-TZPLCKY-XDWCJAE

## music tools
- audacity
- pond5
- turbosquid
- freesound
- musicbed
- envato

## game design resources
- Theory of Fun for Game Design
- The Design of Everyday Things: Revised and Expanded Edition
- The Laws of Simplicity
- The Art of Game Design: A Book of Lenses, Third Edition
- Game Feel
- Level Up! The Guide to Great Video Game Design
- 龙与地下城城主手册
- Blood Sweat and Pixels
- 战旗类经典的资料

## people
- 叶劲峰 
- 西门孟

## feature based challenges
- 精灵的显示如何分清楚哪个先渲染哪个后渲染（渲染层次）
- 如何播放帧动画
- 如何控制两个物体碰撞
- 两个物体碰撞时候销毁其中一个同时生成一个物体播放帧动画特效然后播放完成之后销毁
- 如何播放音乐音效
- 背景层滚动效果怎么做
- 每次播放特效都生成一个物体然后销毁是不是有点浪费内存，可不可以一次生成多个重复利用（引入了对象池）
- 如何处理存档（数据持久化）
- 存档时候如果 A 写入存档还没结束时候 B 又写入存档会不会出问题（引入了文件系统使用单例）