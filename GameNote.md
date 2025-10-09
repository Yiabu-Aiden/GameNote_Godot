## 角色与怪物
### 层
角色位于1层,怪物则位于2层
### 角色属性
对角色和怪物同属一个类,即
```
class_name figure
```
而这个类应包含以下的全局量
```
#生命相关量
var max_health:float
var min_health:float
var current_health:float
``` 
经验变量只应用于角色(考虑不应用,目前游戏不考虑角色升级,而是武器熟练度)
```
#经验等级相关量
var level:int=1
var upgrade_init_experience:float
var upgrade_threshold_experience:float
var current_experience:float
```
防御值(结合函数进行生命扣除)
```
var defense:float
```

## 全局变量
除了一些信号外,考虑将武器的熟练度作为Array存于全局变量中,但关键还是本地存储数据

## 掉落物的实现
游戏的性质就是掉落物均为武器（武器能做武器也能作为配饰等），因此我们用一个资源$Info.res$存储信息，其属性如下
```
extend Resource

class_name item_info

var wp_id #作为武器时的id
var ac_id #作为配饰时的id
var eq_id #作为装甲时的id

#item纹理
var item_texture:texture2D

#掉落物等级
var rarity:int = 0

#描述
var wp_dsp 
var ac_dsp
var eq_dsp

#故事描述
var history

#Packedscene
var wp_control:Packedscene
var ac_control:Packedscene
var eq_control:Packedscene
```
当mob或者某种东西触发掉落信号时，发送带有编号的信号，信号通过全局场景连接到掉落物管理场景，实例化item.tscn,并将资源传入item，当item被拾时，通过全局场景将资源传入背包后端，同时当在手上时将实例化资源的打包场景。
即
```
items_throw->Game_Global_Event.gd->items_center.tscn->item.tscn->bag.tscn
```
### 掉落物中心
掉落物中心包括一个包含item_info的Array，以及一个item实例包
```
@export var item_info_pool:Array[iteminfo]
@export var item_scene:Packedscene #用于掉落物实例化 
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjExNjg2MjYxOSw0NTcxNDUzOTIsLTM1MT
UwNTYyNywxMDg2NDM0ODAsLTE3MzU1ODg4MThdfQ==
-->