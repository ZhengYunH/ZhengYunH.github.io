# SunshineEditor script

##  *editor_main.py*

编辑器初始化入口

 **func**

+ `init(cmdArg)` : 初始化编辑器

  ```python
  random.seed(time.time())	#随机种子
  base.macro.declareVariables()	# 声明变量
  succ, ip, port, editorName = _checkArg(cmdArg)	# 检查参数
  
  ## 根据参数添加模块列表：moduleList
  moduleList = baseModule.moduleList
  for part in ("base", "editorSys", "prepare", editorName):
  		moduleList.extend(_collectModules(part))
  
  newModuleSystemStartup() #在开始moduleSystemStartup之前的逻辑
  
  ## 配置baseModule
  baseModule.moduleSystemStartup = newModuleSystemStartup
  baseModule.moduleList = moduleList
  
  baseModule.importGlobalModules() #导入所有需要的模块
  ```



## editor_base

### *editor_macro.py* 

一些公共接口，import过的模块，全部在全局空间了，其他地方不用重复import

**variable** 

+ `SUNSHINE_META` : dir,editor_base.SunshineClient.Meta	一些元信息的定义，例如：编辑器信息、类型信息
	 `SUNSHINE_PLUGIN` : dir,editor_base.SunshineClient.Plugin	相关的插件
+ `SUNSHINE_STORYLINE` : dir,editor_base.SunshineClient.Storyline 可视化脚本Storyline
+ `SunshineClient` : class,editor_tools.editor_base.SunshineClient.SunshineClient
+ `gSunshineClient = SunshineClient()` : class，编辑器客户端

**func**

+ `declareVariables(environ=None)`：将已经设置好的变量添加到environ中，import时候就调用
  + `setVariables(name,value)` : 判断变量类型，决定是否加入

### *editor_config_dict.py*

配置名字对应的模块，换个角度来看就是进行宏定义，将相应**宏名**和**模块**对应起来，这些模块会被放在`__builtin__`中

**variable**

+ moduleDict
  + base：编辑器基础逻辑
  + editorSys：base之后需要加载的模块
  + prepare：紧接着 editorSys之后需要加载的模块
  + camera：相应功能对应的宏
  + ...
  + softbone



## editor_base.SunshineClient.Plugin.Rainbow

### *RainbowPluginStruct.py*

提供键与实体之间的关系 TODO

**variable**

+ EditMode：nametuple，
+ CreateEntityData：nametuple，
+ IconName：nametuple，
+ ClassNameMap：dirt，模块名与类之间的映射关系（因为是Singleton）
+ Class2EditClass：dirt，

**func**

+ cls_register(cls)：在ClassNameMap中添加相应的映射关系
+ GetClass(clsName)：获得对应模块名的类
+ edit_component(targetCls)：建立 targetCls -> 被装饰的类（编辑控件类）这一映射关系
+ registerEditClass(targetCls, cls)：注册editComponent

**class**

+ *EditComponent*： 编辑控件
+ EntityEditComponent(EditComponent)：通用的实体编辑控件类，当没有实现某个实体相应的实体编辑控件类时，默认创建的该种对象
+ EntityManager：Singleton；管理键（key）和实体（entity）之间的映射关系
+ *EntitySetChangeListener*：实体集合改变监听；在EntityManager添加监听的时候用到，这里的**改变**包括：
  + 添加了一个实体
  + 删除了一个实体
  + 切换了当前编辑的实体

### *RainbowPluginClient.py*

Rainbow客户端

**class**

+ RainbowPluginClient(EditorPluginClient)：游戏端SDK接口，实现这些接口才能运行Rainbow，实际上实现上面的RainbowPluginClient类只需要实现一部分的接口，大部分由\_HandlerWrapper定义
+ \_HandlerWrapper：一些内置的接口逻辑

### *RainbowPluginServer.py*

Rainbow服务端

**class**

+ RainbowPluginServer(EditorPluginServer)
  + 实体修改API
  + 实体创建API



## editor_softbone

### entity

#### *softbone\_proxy.py*

描述当前面板中存在的属性

#### *softbone\_proxy\_manager.py*

负责通信，UI的具体操作

### meta

#### *EntityEditComponentMeta.py*

EditComponent信息

#### *softbone_proxy_meta.py*

软骨编辑器的的元信息：空气阻力，骨头...

### *context_switcher.py*

上下文切换，管理鼠标和键盘事件

### *dump_py_object.py*

将对象转换为字符串，用于输出

### *es_client.py*

```python
class ESClient(SoftboneEditorPluginClient, DISPATCHER.Dispatcher):
	__metaclass__ = METACLASS.Singleton	#单例模式
	def __init__(self):
		self.editorPluginServer = self.GetServer()	#设置服务器
		self.softboneProxyManager = SoftboneProxyManager()	#设置Manager
		self.listenMsg(E_SYNC, "SYNC_DIRECTORY", self.enterSoftboneEditor) #监听事件
        
	def enterSoftboneEditor(self):	#进入编辑器时触发的事件
		self.softboneProxyManager.loadModels()
		return True
    
	def leaveSoftboneEditor(self):	#离开编辑器时触发的事件
		self.softboneProxyManager.clear()
		return (True, False)

	def save(self):
		print "ESClient.save"
```

### *es_init.py*

编辑器初始化入口

### *es\_rainbow.py*

实现Sunshine编辑插件Rainbow接入；实现相应函数，并注册

### *key\_ctrl \\ mouse\_ctrl.py*

键盘和鼠标事件的逻辑



