# SunshineEditor

## Config

配置信息

### Projects

定义项目相关的配置信息

![1531970118450](C:\Users\zhengyunhui\Desktop\doc\ZhengYunH.github.io\netease\assets\1531970118450.png)

```xml
<g69TextEditor>	<!--项目名称-->
	<Engine>g69TextEditor</Engine>	<!--对应引擎,在Engine中配置-->
</g69TextEditor>
```

### Engine

设定相应项目的启动引擎

```xml
<g69TextEditor>
    <ResPath>res\</ResPath>	<!--资源路径-->
    <ScriptPath>script\</ScriptPath> <!--脚本路径-->
    <BinPath></BinPath>	<!--二进制文件路径-->
    <RemoteBootArgs>bin\win32\client.exe %s:%s:text</RemoteBootArgs>  <!--负责启动游戏,两个%s分别表示ip和port,第三个参数是对应编辑器名字,参考script中的editor_main.py-->
</g69TextEditor>
```

### Paths

记录项目的运行路径

![1531970136523](C:\Users\zhengyunhui\Desktop\doc\ZhengYunH.github.io\netease\assets\1531970136523.png)

```xml
<g69TextEditor>C:\Users\zhengyunhui\Desktop\demo\client\</g69TextEditor>
```

### Config

模板设置

![1531970230126](C:\Users\zhengyunhui\Desktop\doc\ZhengYunH.github.io\netease\assets\1531970230126.png)

```XML

```



## ExtPlugin

加入相应的插件

### Plugin.py

```python
class TextEditorPlugin(Plugin):
	NAME = "TextEditor"	#编辑器的名称,可以瞎改,不影响使用

	PROPERTIES = {	#一些基本信息
		"scriptEntry": "main",
		"editMenu": True,
		"isStarter": False,
		"windowTitle": "Sunshine",
		"requirePlugins": set(),
		"loadType": Sunshine.LOAD_TYPE_OPTIONAL,
	}

	def __init__(self):
		super(TextEditorPlugin, self).__init__()
		self.win = None

	def initStarter(self, args):
		pass

	def initPlugin(self):	#初始化插件
		self.rpc = RPCService.CreateRPCConnection(UUID)

	def createWindows(self, isStarter):	#显示界面
		self.win = TextEditorWidget(self.rpc)
		self.rpcHandler = self.win
		return [self.win]

def getPlugin():	
	return TextEditorPlugin()
```

### PluginProperty.py

定义插件的属性

![1531970810588](C:\Users\zhengyunhui\Desktop\doc\ZhengYunH.github.io\netease\assets\1531970810588.png)

```python
def getPluginProperty():
	return PluginProperty(
		name="TextEditor", 
		requirePlugins={"InnerSync"}, 
		contact="G69|郑运辉",
		)
```

### widget

定义一些相应的挂件,用于显示



