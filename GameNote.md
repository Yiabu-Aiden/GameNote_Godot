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
经验变量只应用于角色
```
#经验等级相关量
var level:int=1
var upgrade_init_experience:float
var upgrade_threshold_experience:float
var current_experience:float
```
```
#攻击相关的变量
var attack_value:float
var atta
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYyMTEzMzg0OCw1MDI0OTA2MTNdfQ==
-->