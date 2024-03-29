团队协作
====

几个核心点:    
强调PHP语言的基础能力；    
熟练掌握PHP的常用函数库；   
基础语言能力之外，需要深度理解Unix/Linux操作系统，IO/进程，Socket/TCP/UDP等基础知识。  


关于TinyPHP Framework的敏捷开发理念
-----
-----

### 几个认识
* 不可只依赖框架：
    * 框架是工程项目开发中的辅助工具和规范约束性团队协作工具，编码者应当加强语言基础的学习，和对PHP手册的精通掌握。 
* 框架只是工具:
    * 喜欢就用，不喜欢就弃。
* 不可强调某个框架的全天候作业能力：
    * 什么都会的框架意味着什么都做不好，根据需要选择语言工具和语言框架，无需拘泥于某个语言和某个框架。


### 适用场景
* 客户端应用(IOS/Android/H5/小程序)的API接口开发：
    * 高性能，大并发。
    * 快速开发
    
*  Web管理后台：
    * 适用于全栈或不具备设计工程师和前端工程师的研发团队。
    * 集成了tinyphp-ui前端框架，只需少量的JS前端代码。 
    
* 大规模团队协作：
    * 10-100+人以上的研发团队。
    * 创业团队，产品快速成型，可在较少的研发人力成本下进行高效的敏捷开发。
    * 适用于具备在大规模的高性能应用场景下，通过PHP解决大多数复杂业务的架构。
    * 可将大规模复杂应用的后端语言有效控制为PHP一种后端开发语言，有效降低项目维护成本和团队管理难度。

### 基于MVC/MVVC的敏捷开发

* 遵守严格的面向对象编码规范，禁止全局变量穿透对象/高耦合/低内聚等不健康编码方式的滥用。
* 模型层（Model）
    * 专注于各种业务数据源的处理
    * 模型层次划分清晰；
    * 高度内聚；
    * 面向外部调用的公共接口调用严格遵守确定性的输入输出，以兼容各种运行环境下的数据处理；
* 视图层(View)：
    * 保持轻量级
    * 不加载复杂的模板工具去极大的损耗性能；
    * 在面向客户端应用/API接口编码的情况下，完全省去视图层处理；
    * 推荐JSON数据交互进行接口输出
* 控制层(Controller)：
    * 专注于业务流程和逻辑控制。
    * 保持各种运行环境下的分布式处理和与模型层的低度耦合。

系统设计原则
-----
-----


###  保持健壮与鲁棒性

少即是多，不做过多封装。
不依赖框架，通过框架的约束和扩展性，处理复杂业务。
多花心思提高性能

### 防止重复造轮子

每个功能应当只有一个函数/类/接口/实例/命名空间。   
成员之间通过协调和沟通，由一人/一个小组负责一个具体模块的所有功能编写。   
示例： 按业务模块划分，高度内聚相关模块和功能性接口:   

```php
//该命名空间下规划所有用户相关内的子命名空间和类，处理用户所有数据
// application/models/User/
App\Model\User;

// 该命名空间与其他业务的模型交互数据的用户相关数，应规划到命名空间第一层级，统一在该类中开放对外接口，而不是分散在所有的类中
// application/models/UserOrder.php
Class UserOrder 
{
    //根据订单ID获取用户信息
    public function getUserInfoByOrderId($orderId)
    {
         // 调用订单模型获取订单数据
        $orders =  $this->OrdersModel->getOrdersByOrderId($orderId);
           
    }
}

// 该命名空间处理用户中的后台管理员的所有数据
// application/models/User/Admin/ 
App\Model\User\Admin;

// 处理用户中后台管理员的登录事项
// application/models/User/Admin/Login.php
Class App\Model\User\Admin\Login 
{
    ...
}
```

一个顶层的命名空间可代表一个业务模块，通过子命名空间和类组合处理分支模块。   

### 抽象原则

通过抽象减少重复代码。      
重点功能由负责该模块的主程负责编写，并为其他团队成员提供通用的扩展接口，其他成员继承或扩展，在该模块满足不了实际需求时，应推动负责该模块的主程扩展和优化，无需自己重复写一套。      
 
```php
// 该命名空间处理用户中的后台管理员的所有数据
// application/models/User/Admin/ 
App\Model\User\Admin;

// 处理用户中后台管理员的登录事项
// application/models/User/Admin/Login.php
// author: tom
Class Login 
{
    ...
}

//提供通用接口，扩展其他登录方式
// author:tom
Interface ILogin 
{
    ...
}

// 快捷登录实现，应继承Login类的基础上，调用其实现方式，满足通用接口ILogin, 实现登录的数据交互和持久化
// author: tony
class QucikLogin extend Login implement ILogin 
{
    ...
}
```

### 保持简洁优雅

简单是编程的目标。     

简单的代码花费时间少，漏洞少，性能高，易于修改。     

简单代码需要实现过程清晰一目了然，命名规范，不做过多的封装和分层，更能体现程序员自身的功底。   

编码时不需绕来绕去，为了靠近某些流行的前言概念和设计模式，进行各种抽象分层，这种代码看似优雅和专业，其实严重损耗性能，增加他人阅读理解和维护的困难。   

流行的东西，总是流行地快，去地也快。   

唯有能通过适当少量代码解决复杂业务的方式，才能真正体现算法上的思考和巧妙设计的优雅。   

简单的示例：

```php

/**
* 接口的简单化
* 给使用者符合期望的输入输出保持确定性
*/ 
public function getUserInfoById(int $id) : array 
{
    ...
}

/**
* 错误的简单化接口
* 不确定的可自定义的返回字段
* 不确定的获取条件
*/
public function getUserInfo($field = '*', $where)
{
   ...
}

```

### 避免创建冗余的代码

除非必要，不要创建新功能。
示例： 不必要的一些冗余代码
    * 穿透类和示例的全局常量和函数，全局类。   
    * 过多的抽象和封装。   
    * 在简单的MVC外部集成各种工具类和便捷操作的静态类。   
    * 在模型层和控制器层的顶部添加巨大的业务配置数组，将应该放在配置文件夹里的配置数据。   
    * 在控制器层和模型层顶层，集成过多的抽象基类和工具类。   

### 只做可运行的最简单的事

尽可能做可运行的最简单的事。   

保持简单原则。   

重构代码时，应该朝不断简化代码的目标优化。   

### 傻瓜式

编写的代码一定要易于读和理解，这样别人才会欣赏，给你提出合理化的建议。     

相反，若是繁杂难解的程序，其他人总是会避而远之。   

代码里优雅的命名规范，就是最好的注释。   

代码结构体间必要的详细注释是最好的编程文档。  

针对每一次代码修改留下详细的时间日期索引和注释是必要的。   

完整的编码文档和标准接口文档，是团队协作最基础的需求。   

### 开放接口和继承

团队协作中，为方便他人扩展自己的代码，留下足够的Interface类和基类是必须的方式。   
在维护他人的代码时，优先考虑继承和扩展，切忌直接动手修改。      
针对团队成员的代码，应该首先沟通使其修改满足需求。   
针对项目中的开源代码尤其是框架代码，禁止直接修改源码，而应该扩展或者继承实现自己的意图，维护其版权和后续升级更新的必要。   

### 有利于维护

保持简单，易于理解，详细注释。   
文件注释，函数注释，类注释严格安装编码规范。   
代码仓库每次提交，commit message要详细说明，不要敷衍。   
团队协作时，需要团队成员每周专门抽两个小时，review自己近一周内所写的代码，并定下优化计划，快速解决一周内的严重问题，简化自己不太优雅的实现方式。   

### 最小化原则

只写需求所需的最小化功能，别炫技，写太多本来不需要但看起来好像很牛逼的东西。

### 单一化原则 

某个代码的功能，应该保证只有单一的明确的执行任务。   

简单的示例：

```php

/**
* 接口的简单化
* 给使用者符合期望的输入输出保持确定性
*/ 
public function getUserInfoById(int $id) : array 
{
    ...
}

/**
* 错误的简单化接口
* 不确定的可自定义的返回字段
* 不确定的获取条件
*/
public function getUserInfo($field = '*', $where)
{
   ...
}

```

### 低耦合原则

代码的任何一个部分应该减少对其他区域代码的依赖关系。  
尽量不要使用共享参数和可变参数。  
低耦合往往是完美结构系统和优秀设计的标志。  
错误示例中，Model的SQL字段在控制器中被耦合，这也是通常导致SQL注入攻击后果的主要原因

```php

// application/models/User/Info.php
class Info extends Db 
{
    /**
    * 不确定的可自定义的返回字段
    * 不确定的获取条件
    */
    public function getUserInfo($field = '*', $where)
    {
        ...
    }

    ...
}

// application/controller/User.php
class User extends Controller
{
    /**
    * 不确定的可自定义的返回字段
    * 不确定的获取条件
    */
    public function  indexAction()
    {
        $uid = $this->get['uid'];
        $userinfos = $this->userInfoModel->getUserInfo($uid);
    }

    ...
}
```

### 高内聚原则

相似的业务和功能代码应尽量放在一个部分。   
良好的文件夹和文件命名规范，用来高度内聚相关的业务模块和功能   

```php

// application/models/User 该命名空间存放所有用户相关的业务数据处理
// application/models/User/Admin 该子命名空间存放所有跟用户后台管理相关的业务数据处理
// application/controllers/User 该命名空间存放所有用户相关的业务逻辑处理
// appliaction/views/zh_cn/User 该文件夹存放所有用户相关的视图模板
// 

```

### 隐藏实现细节（Hide Implementation Details）

接口设计需要隐藏实现细节原则。   
当其他部分发生变化时，能够尽可能降低对其他组件的影响。   

```php

/**
* 接口的简单化
* 给使用者符合期望的输入输出保持确定性
*/ 
public function getUserInfoById(int $id) : array 
{
    return $this->getUserInfoFromCache($id);
}

/**
* 对调用公共接口的成员可隐藏具体实现的细节，并通过私有标识防止调用。
*/
private function getUserInfoFromCache(int $id) 
{
   ...
}

```

### 最少化原则

代码只和与其有直接关系的部分连接。     
比如类的接口设计，传递的参数。   
 
```php

/**
* 公共接口开放，设计尽量简单，具有符合预期的稳定
* 给使用者符合期望的输入输出保持确定性
*/ 
public function getUserInfoById(int $id) : array 
{
    return $this->getUserInfoFromCache($id);
}

/**
* 对调用公共接口的成员可隐藏具体实现的细节，并通过私有标识防止调用。
*/
private function getUserInfoFromCache(int $id) 
{
   ...
}

```

### 避免过早优化

除非代码性能比预估要慢，否则别去优化。   
假如真的想优化，就必须先测算数据证明速度真的变快。   
商业化项目中，因为过早优化多花费的时间和人力，都是成本的巨大浪费，切忌追求不必要的完美。   
这也是PHP有诸多不完美之处，仍具有顽强生命力的原因所在，`敏捷开发，节省时间就是节省金钱，可以低成本的快速验证业务模式判断可行性。`

### 代码重用原则

提高代码的可读性，缩短开发时间。   
与15有些区别的地方，在前期架构和系统设计，代码重用性等方面多花功夫，可以避免后面推到重来浪费更多时间延误项目顺利上线的严重后果。   
简而言之，无数惨痛的经验教训告诉程序员们： 磨刀不误砍柴工。   

### 分布式与离散原则

不同类型的模块和功能，应该由不同的代码和最小重迭的模块组成。   

### 拥抱改变

积极面对变化，灵活运用以上规范和约束，善于取舍。     
编程语言，编程框架，以至于IDE，编程硬件等等，都只是我们实现自己项目的辅助工具，如果其中任何一种不适应我们的项目需求，应该快速舍弃，换成更适应我们工作的工具。     
老鸟都会多学几种语言，才会融会贯通，举一反三。   
最后的忠告，不要抱残守缺，墨守成规，然后发现自己在时代的潮流中，落后了。   
