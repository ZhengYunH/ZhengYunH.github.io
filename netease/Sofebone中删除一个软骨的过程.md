# Sofebone中删除一个软骨的过程

## Client

***e_connect*** SCHEDULE.schedule(_updateSunshineClient)	定时更新

​	***SunshineClient*** Update

​		***SunshineClient*** _UpdateConnection	更新连接

​			***es_rainbow（RainbowClient）***  ModifyEditEntity	return: Response(UUID, 'ModifyEntityOver')

> 根据包的(uuid,method)确定要执行的操作为es的ModifyEditEntity，ModifyEditEntity根据opt决定执行del
>
> ​	包格式：{method:str, params:[uuid,key,path,val]}，其中path为"opt/..."，opt为选择的操作，包括mod,add,del
>
> 由于es_rainbow继承了RainbowPluginClient，__HandlerWrapper中传入的plugin为es_rainbow，但es_rainbow没有重写ModifyEditEntity ，因此调用的是RainbowPluginClient实现的ModifyEditEntity ，而DelEntityProperty函数则调用的是es_rainbow重写的DelEntityProperty函数

​				***es_rainbow***	DelEntityProperty 删除实体信息  

​					***TypeMeta***	DelEntityProperty

​						***TypeMeta***	GetObjectMetaByPath	利用path[1:-1]的信息来确定部件的父部件

​						***TypeMeta***	DelChildObject	利用父部件根据path[-1]删除相应的部件

>  也就是删除相应父对象的对象数组中的某个值，接着就在setattr中利用删除后的对象信息更新存储在本地_entityManager中的对象信息

​					setattr

​						***softbone_proxy***	bones.setter		更新bones[]信息

​						***softbone_proxy***	_updateModel		更新模型

​							***softbone_proxy_manager***	 changeInfo	改变信息

​							***softbone_proxy_manager***	_modelUI.updateSoftBone()	更新软骨信息

​			***SunshineClient***  CallServer		对信息打包

​				***SunshineClient***  SendData		将要发送的信息放到_sendParts中

> 将所有要发送的包放在self._sendParts中，处理完毕所有接收到的包后就可以在\_UpdataConnection中发送



## Sunshine Editor 

