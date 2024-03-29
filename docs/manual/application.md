Application 应用程序
====

Application 通过 Tiny\Runtime\Runtime的唯一实例上创建和销毁，管理整个MVC流程的功能组件的按需加载。 


### 基于Runtime创建

Application的构建顺序是: `Tiny\Runtime` →  `Tiny\ApplicationBase` → `Tiny\MVC\WebApplication|Tiny\MVC\ConsoleApplication`;   
Tiny\Runtime会根据运行环境自动创建`WebApplication` 或`ConsoleApplication`的实例   
    * `RpcApplication`是`WebApplication`的子类，做为RPC分布式服务的服务端提供对外服务。     
    * `WebApplication`的生命周期服从PHP-FPM的FastCGI协议, 即在用户每次访问的开始/结束会创建/销毁`WebApplication`实例。  
    * `ConsoleApplication`持续整个应用程序的生命周期，除非完成执行或主动中断。    

### Application的实例化


##### 配置文件

profile.php是Application的主配置文件，Application通过Tiny\MVC\Application\Properties将其实例化。        
可参考配置手册 [Proptrites/Application配置文件:application/config/profile.php](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/profile.md)

##### 目录规划

功能文件夹一律小写,_分隔，并以复数形式规范命名。   

存放类文件的命名空间文件夹一律依照命名规范创建。   

需要写权限的文件一律放置于runtime下，仅在runtime设置写权限。  


##### 不同运行环境的Application实例


`ApplicationBase`    
可参考标准库 [Tiny/MVC/Application](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/mvc.md)

`WebApplication`    
可参考标准库 [Tiny/MVC/WebApplication](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/mvc.md)

`ConsoleApplication`   
可参考标准库 [Tiny/MVC/ConsoleApplication](https://github.com/tinyphporg/tinyphp-dcos/blob/master/docs/lib/mvc.md)


##### Application的完整MVC生命周期

Application中贯穿着整个应用的完整MVC流程实现，   
Application的生命周期由MVC流程和事件两部分组成。

```php
Tiny\Runtime → createAppliation → Tiny\MVC\ApplicationBase::__construct;
创建 Properties 基于profile.php
↓   
创建: Request   
↓   
创建: Response   
↓   
事件: MvcEvent::EVENT_BEGIN_REQUEST   
↓   
运行: Application::run(); 
↓
引导: Application::bootstrap();
↓
事件: MvcEvent::EVENT_BOOTSTRAP
↓
路由: Application::route();
↓
事件: MvcEvent::EVENT_ROUTER_STARTUP
↓
事件: MvcEvent::EVENT_ROUTER_SHUTDOWN
↓
事件: MvcEvent::EVENT_PRE_DISPATCH;
↓
派发 Application::dispatch();
↓
事件: MvcEvent::EVENT_POST_DISPATCH;
↓
事件: MvcEvent::EVENT_END_REQUEST
↓
结束 Response::output() → Response::end();
```

参考标准库
-----
-----

[Tiny/MVC/Request](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/mvc.md)   
[Tiny/MVC/Response](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/mvc.md)  
[Tiny/MVC/Bootstrap](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/mvc.md)  
[Tiny/MVC/Router](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/mvc.md)  
[Tiny/MVC/Dispatch](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/mvc.md)  
[Tiny/MVC/Controller](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/mvc.md)    
[Tiny/MVC/Model](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/mvc.md)   
[Tiny/MVC/Viewer](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/mvc.md)   

