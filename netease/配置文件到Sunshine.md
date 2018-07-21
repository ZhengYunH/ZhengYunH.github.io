# 配置文件到Sunshine

**es_client** enterSoftboneEditor

​	**softbone_proxy_manager**	loadModels

​		**softbone_proxy_manager**	loadInfo	从本地导入数据

​									createModelUI	UI界面初始化

​			**softbone_proxy_manager**	self._addModelProxy 

​					**RainbowPlugin**	*EntityManager*	AddEntity

​						RegisterClass	注册实体对应的 Class

​						entitySetChangeListener.AddEntity	调用实体对应监听器的AddEntity	

​							**es_rainbow**	*RainbowEntitySetChangeListener*	rainbowServer.AddEntity\

​							***RainbowPluginServer*** CallServer

​								***EditorPlugin***	_callServerFunc

```sequence
title: 配置文件到Sunshine

participant es_client as ESC
participant softbone_proxy_manager as SPM
participant RainbowPlugin as RP

ESC->SPM:loadModels()
SPM-->SPM:loadInfo() 
SPM-->SPM:createModelUI()
SPM->RP:对每一个角色 AddEntity(readId,modelProxy)




```



