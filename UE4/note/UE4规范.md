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
| Static Mesh (01)         | SM_Rock_01        |
| Static Mesh (02)         | SM_Rock_02        |
| Material                 | M_Rock            |
| Material Instance (Snow) | MI_Rock_Snow      |

### 资源类型表 

#### 通用类型 Most Common

| 资源类型 Asset Type | 前缀 Prefix | 后缀 Suffix | 备注 Notes                     |
| ------------------- | ----------- | ----------- | ------------------------------ |
| Level / Map         |             |             | 所有地图应该放在Maps目录下     |
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