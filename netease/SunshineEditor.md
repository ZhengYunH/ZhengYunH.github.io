# SunshineEditor editor_tools

##  *editor_main.py*

编辑器初始化入口

 **func**

+ `init(cmdArg)` : 初始化编辑器

  ```python
  random.seed(time.time())	#随机种子
  base.macro.declareVariables()	# 声明变量
  succ, ip, port, editorName = _checkArg(cmdArg)	# 检查参数
  
  ## 根据编辑器的名字添加模块List：moduleList
  moduleList = baseModule.moduleList
  for part in ("base", "editorSys", "prepare", editorName):
  		moduleList.extend(_collectModules(part))
          
  newModuleSystemStartup()：
  ```



## editor_base

### *editor_macro.py* 

一些公共接口，import过的模块，全部在全局空间了，其他地方不用重复import

**variable**

+ `SUNSHINE_META` : dir,editor_base.SunshineClient.Meta	
+ `SUNSHINE_PLUGIN` : dir,editor_base.SunshineClient.Plugin	相关的插件
+ `SUNSHINE_STORYLINE` : dir,editor_base.SunshineClient.Storyline
+ `SunshineClient` : class,editor_tools.editor_base.SunshineClient.SunshineClient
+ `gSunshineClient = SunshineClient()` : class，编辑器客户端

**func**

+ `declareVariables(environ=None)`：将已经设置好的变量添加到environ中，import时候就调用
  + `setVariables(name,value)` : 判断变量类型，决定是否加入

### *editor_config_dict.py*

配置名字对应的模块，换个角度来看就是进行宏定义，将相应的宏名和模块对应起来，这些模块会被放在`__builtin__`中

**variable**

+ moduleDict
  + base：编辑器基础逻辑
  + editorSys：base之后需要加载的模块
  + prepare：紧接着 editorSys之后需要加载的模块
  + camera：相应功能对应的宏
  + ...
  + softbone

