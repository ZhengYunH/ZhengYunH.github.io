# UE规范

> + https://github.com/Allar/ue5-style-guide / https://github.com/skylens-inc/ue4-style-guide/blob/master/README.md 中文
> + https://nerivec.github.io/old-ue4-wiki/pages/assets-naming-convention.html
> + https://docs.unrealengine.com/4.27/zh-CN/ProductionPipelines/DevelopmentSetup/CodingStandard/



## 资源命名规范 Asset Naming Conventions

命名规范：`Prefix_BaseAssetName_Variant_Suffix`

+ `Prefix`（前缀）、`Suffix`（后缀）由资源类型决定，参照下面的资源类型表。
+ `BaseAssetName`（基本资源名）：所有资源都应该拥有这个基础资源名，任何属于该逻辑组的资源都应该遵守同样的命名规范。
  + 使用简短而便于识别的词汇：例如一个关于萤的所有资源的`BaseAssetName`都应该叫做`Ying`
+ `Variant`（扩展名）：用于标记所属资源组的子集，是用于变换的词条，不仅限于一个。例如萤的存在一个名为Evil的皮肤，那该皮肤资源的`BaseAssetName + Variant`为 `Ying_Evil`。在实际生产中，为了保证资源ID的唯一性，`Variant`可以从 01 开始的两位数字表示。例如制作了一堆石头，那么就应该命名为`Rock_01`, `Rock_02`, `Rock_03`。
  + 使用简短而便于识别的词汇：在实际生产中请不要给Variant起名为A、B、C
  + 除非特殊需要，不要让数字超过三位数，如果超过了，应该考虑使用多个 `BaseAssetName`
  + 可以把多个`Variant`组合起来，例如：`Ying_Evil_01`

### 示例

| 资源类型 Asset Type      | 资源名 Asset Name |
| ------------------------ | ----------------- |
| Skeletal Mesh            | SK_Bob            |
| Texture (Diffuse/Albedo) | T_Bob_D           |
| Texture (Evil Diffuse)   | T_Bob_Evil_D      |
| Static Mesh (01)         | S_Rock_01         |
| Static Mesh (02)         | S_Rock_02         |
| Material                 | M_Rock            |
| Material Instance (Snow) | MI_Rock_Snow      |

### 资源类型表 

#### 通用类型 Most Common

| 资源类型 Asset Type | 前缀 Prefix | 后缀 Suffix | 备注 Notes                     |
| ------------------- | ----------- | ----------- | ------------------------------ |
| Level / Map         |             |             | [所有地图应该放在Maps目录下]() |
| Level (Persistent)  |             | _P          |                                |
| Level (Audio)       |             | _Audio      |                                |
| Level (Lighting)    |             | _Lighting   |                                |
| Level (Geometry)    |             | _Geo        |                                |
| Level (Gameplay)    |             | _Gameplay   |                                |
| Blueprint           | BP_         |             |                                |
| Material            | M_          |             |                                |
| Static Mesh         | SM_         |             |                                |
| Skeletal Mesh       | SK_         |             |                                |
| Texture             | T_          | _?          | 后缀部分参照下面的[纹理]()章节 |
| Particle System     | PS_         |             |                                |
| Widget Blueprint    | WBP         |             |                                |

#### 动作 Animations

| 资源类型 Asset Type | 前缀 Prefix | 后缀 Suffix | 备注 Notes |
| ------------------- | ----------- | ----------- | ---------- |
| Aim Offset          | AO_         |             |            |
| Aim Offset 1D       | AO_         |             |            |
| Animation Blueprint | ABP_        |             |            |
| Animation Composite | AC_         |             |            |
| Animation Montage   | AM_         |             |            |
| Animation Sequence  | AS_         |             |            |
| Blend Space         | BS_         |             |            |
| Blend Space 1D      | BS_         |             |            |
| Level Sequence      | LS_         |             |            |
| Morph Target        | MT_         |             |            |
| Paper Flipbook      | PFB_        |             |            |
| Rig                 | Rig_        |             |            |
| Skeletal Mesh       | SK_         |             |            |
| Skeleton            | SKEL_       |             |            |

#### AI

| 资源类型 Asset Type | 前缀 Prefix  | 后缀 Suffix | 备注 Notes |
| ------------------- | ------------ | ----------- | ---------- |
| AI Controller       | AIC_         |             |            |
| Behavior Tree       | BT_          |             |            |
| Blackboard          | BB_          |             |            |
| Decorator           | BTDecorator_ |             |            |
| Service             | BTService_   |             |            |
| Task                | BTTask_      |             |            |

#### 蓝图 Blueprints

| 资源类型 Asset Type        | 前缀 Prefix | 后缀 Suffix | 备注 Notes                 |
| -------------------------- | ----------- | ----------- | -------------------------- |
| Blueprint                  | BP_         |             |                            |
| Blueprint Function Library | BPFL_       |             |                            |
| Blueprint Interface        | BPI_        |             |                            |
| Blueprint Macro Library    | BPML_       |             | 可能的话尽量不要使用蓝图宏 |
| Enumeration                | E           |             | 没有下划线                 |
| Structure                  | F or S      |             | 没有下划线                 |
| Widget Blueprint           | WBP_        |             |                            |

#### 材质 Materials

| 资源类型 Asset Type           | 前缀 Prefix | 后缀 Suffix | 备注 Notes |
| ----------------------------- | ----------- | ----------- | ---------- |
| Material                      | M_          |             |            |
| Material (Post Process)       | PP_         |             |            |
| Material Function             | MF_         |             |            |
| Material Instance             | MI_         |             |            |
| Material Parameter Collection | MPC_        |             |            |
| Subsurface Profile            | SP_         |             |            |
| Physical Materials            | PM_         |             |            |

#### 纹理 Textures

| 资源类型 Asset Type                 | 前缀 Prefix | 后缀 Suffix | 备注 Notes         |
| ----------------------------------- | ----------- | ----------- | ------------------ |
| Texture                             | T_          |             |                    |
| Texture (Diffuse/Albedo/Base Color) | T_          | _D          |                    |
| Texture (Normal)                    | T_          | _N          |                    |
| Texture (Roughness)                 | T_          | _R          |                    |
| Texture (Alpha/Opacity)             | T_          | _A          |                    |
| Texture (Ambient Occlusion)         | T_          | _O          |                    |
| Texture (Bump)                      | T_          | _B          |                    |
| Texture (Emissive)                  | T_          | _E          |                    |
| Texture (Mask)                      | T_          | _M          |                    |
| Texture (Specular)                  | T_          | _S          |                    |
| Texture (Packed)                    | T_          | _*          | 参见下面的纹理合并 |
| Texture Cube                        | TC_         |             |                    |
| Media Texture                       | MT_         |             |                    |
| Render Target                       | RT_         |             |                    |
| Cube Render Target                  | RTC_        |             |                    |
| Texture Light Profile               | TLP         |             |                    |

##### 纹理合并

多张纹理存储到一个纹理文件时，按RGB顺序记录于文件后缀中。例如存储了 Emissive \ Roughness \ Ambient Occlusion 的纹理文件后缀为 _ERO

#### 杂项 Miscellaneous

| 资源类型 Asset Type   | 前缀 Prefix | 后缀 Suffix | 备注 Notes             |
| --------------------- | ----------- | ----------- | ---------------------- |
| Data Asset            | *_          |             | 前缀取决于何种类型资源 |
| Camera Anim           | CA_         |             |                        |
| Float Curve           | Curve_      | _Float      |                        |
| Color Curve           | Curve_      | _Color      |                        |
| Vector Curve          | Curve_      | _Vector     |                        |
| Curve Table           | Curve_      | _Table      |                        |
| Data Table            | DT_         |             |                        |
| Animated Vector Field | VFA_        |             |                        |
| Foliage Type          | FT_         |             |                        |
| Force Feedback Effect | FFE_        |             |                        |
| Landscape Grass Type  | LG_         |             |                        |
| Landscape Layer       | LL_         |             |                        |
| Matinee Data          | Matinee_    |             |                        |
| Media Player          | MP_         |             |                        |
| Object Library        | OL_         |             |                        |
| Redirector            | Re_         |             |                        |
| Sprite Sheet          | SS_         |             |                        |
| Static Vector Field   | VF_         |             |                        |
| Touch Interface Setup | TI_         |             |                        |

#### Paper 2D

| 资源类型 Asset Type | 前缀 Prefix | 后缀 Suffix | 备注 Notes |
| ------------------- | ----------- | ----------- | ---------- |
| Paper Flipbook      | PFB_        |             |            |
| Sprite              | SPR_        |             |            |
| Sprite Atlas Group  | SPRG_       |             |            |
| Tile Map            | TM_         |             |            |
| Tile Set            | TS_         |             |            |

#### 物理 Physics

| 资源类型 Asset Type | 前缀 Prefix | 后缀 Suffix | 备注 Notes |
| ------------------- | ----------- | ----------- | ---------- |
| Physical Material   | PM_         |             |            |
| Physical Asset      | PHYS_       |             |            |
| Destructible Mesh   | DM_         |             |            |

#### 声音 Sound

| 资源类型 Asset Type | 前缀 Prefix | 后缀 Suffix | 备注 Notes                                         |
| ------------------- | ----------- | ----------- | -------------------------------------------------- |
| Dialogue Voice      | DV_         |             |                                                    |
| Dialogue Wave       | DW_         |             |                                                    |
| Media Sound Wave    | MSW_        |             |                                                    |
| Reverb Effect       | Reverb_     |             |                                                    |
| Sound Attenuation   | ATT_        |             |                                                    |
| Sound Class         |             |             | 没有前缀和后缀，这些资源应该放在SoundClasses目录中 |
| Sound Concurrency   |             | _SC         | 在SoundClass之后命名                               |
| Sound Cue           | A_          | _Cue        |                                                    |
| Sound Mix           | Mix_        |             |                                                    |
| Sound Wave          | A_          |             |                                                    |

#### 界面 User Interface

| 资源类型 Asset Type | 前缀 Prefix | 后缀 Suffix | 备注 Notes |
| ------------------- | ----------- | ----------- | ---------- |
| Font                | Font_       |             |            |
| Slate Brush         | Brush_      |             |            |
| Slate Widget Style  | Style_      |             |            |
| Widget Blueprint    | WBP_        |             |            |

#### 特效 Effects

| 资源类型 Asset Type     | 前缀 Prefix | 后缀 Suffix | 备注 Notes |
| ----------------------- | ----------- | ----------- | ---------- |
| Particle System         | PS_         |             |            |
| Material (Post Process) | PP_         |             |            |



## 目录结构

> 每个子目录下是否再进行具体的分类：以资源文件名进行划分 or 以文件夹的名字用于划分
>
> ​	例如：角色c拥有材质M_c，应该组织为 content/character/c/material/mat 还是 content/character/c/M_c



```
|-- Content
	|-- YY62
	|	|-- Character
	|	|	|-- Player
	|	|	|-- NPC
	|	|-- Core
	|	|	|-- Characters
	|	|	|-- Engine
    |   |   |-- GameModes
    |   |   |-- Interactables
    |   |   |-- Pickups
	|	|-- Effects
	|	|-- Environment
	|	|	|-- Background
	|	|	|-- Buildings
	|	|	|-- Foliage
	|	|	|-- Props
	|	|	|-- Sky
	|	|	|-- Landscape
	|	|	|-- Water
	|	|-- Gameplay
	|	|-- Maps
	|	|	|-- Episode(_Number)
	|	|-- MaterialLibrary
	|	|-- PostProcess
	|	|-- Sound
	|	|-- UI
	|	|-- Vehicles
	|-- Developers
	|	|-- User1
	|	|-- User2

```



### 文件夹命名

+ PascalCase大小写规范：所有首字母大写，中间没有任何连接符 `_`。例如 `DesertEagle`, `RocketPistol` , `ASeriesOfWords`
+ 不要使用空格

+ 不要使用Unicode语言字符或奇怪的符号：也就是只使用`a-z`，`A-Z`， `0-9` 这些符号；不要用`@`, `-`, `_`, `,`, `#`, `*`这种字符，更不要用中文。

### 使用一个顶级目录来保存所有工程资源

+ 所有的工程资源都保存在一个以工程名命名的目录中（例如 `Content / YY62` 目录中）
+ 对于临时资源，可以使用`开发者目录 Developers`，参照下面的 **用来做临时测试的开发者** 章节中的说明
+ 范例、模板和商城中的资源都不会污染到项目工程
+ 便于子版本资源的管理和补丁包

### 用来做临时测试的开发者目录

建立一个`Developers`目录用于个人资源维护，其它人不需使用其中的资源内容。当存在于`Developers`目录中的资源正式准备好时，美术人员将其迁移至正式的工程目录，并修复引用关系

### 所有的地图文件应该保存在一个名为`Maps`的目录中 

通过子目录的方法去组织地图资源，例如建立 `Maps/Campaign1/` 或 `Maps/Arenas`，但最重要的是一定要都放在 `/Content/Project/Maps`。这也有助于产品的打版本工作，把地图放在一个地方，做版本时就很难漏掉某个地图，对于烘培光照贴图或者质量检查都有利。

### 使用`Core`目录存储系统蓝图资源以及其他系统资源

使用`/Content/Project/Core`这个目录用来保存一个工程中最为核心的资源。例如，非常基础的`GameMode`, `Character`, `PlayerController`, `GameState`, `PlayerState`，以及如此相关的一些资源也应该放在这里。

非程序员很少有理由去碰这个目录，如果工程目录结构合理，那么游戏设计师只需要使用子类提供的功能就可以工作，负责场景编辑的员工只需要使用专用的的蓝图就可以，而不用碰到这些基础类。

### 不要创建名为`Assets`或者`AssetTypes`的目录

+ 创建名为`Assets`的目录是多余的
+ 创建名为`Meshes` 、`Textures`或者`Materials`的目录是多余的：因为资源文件名本身就提供了这些信息，而且使用资源浏览器的过滤功能能够更好的处理这个问题

### 超大资源要有自己的目录结构

对于公用的并且数量巨大的文件，应该被放在同一个文件夹中。当有超过15个以上的资源是同一类型（例如动画和声音资源），就应该新增一个子文件夹用于管理所有的动画文件。

另外，对于角色公用的动画资源应该放在`Characters/Common/Animations`，并且其中应该还有诸如`Locomotion` 或者`Cinematic`的子目录。

### 材质库`MaterialLibrary`

对于任何基础材质，可以被重复使用而不属于特定模型的材质和纹理，应该放在材质库目录下 `Content/Project/MaterialLibrary`



## 蓝图









## 代码规范（TODO）

