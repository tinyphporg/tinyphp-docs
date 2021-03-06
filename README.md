Tinyphp-framework
====

tinyphp的适用场景与理念
---- 
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

中文手册
---- 
> 本框架的编码规范基本遵守PSR规范标准，仅少数细节做灵活调整。
* [入门](#入门)
   * 环境搭建 [lnmp-utils: http://github.com/tinyphporg/lnmp-utils.git](http://github.com/tinyphporg/lnmp-utils.git)
   * Demo [tinyphp: http://github.com/tinyphporg/tinyphp.git](http://github.com/tinyphporg/tinyphp.git)
    
* [语言基础规范](https://github.com/tinyphporg/tinyphp-docs/tree/master/docs/coding)
    + [文件结构](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/coding/file_001.md)   
    + [程序的排版](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/coding/program_typesetting_002.md)    
    + [命名规则](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/coding/rules_003.md)  
    + [表达式和基本语句](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/coding/expression_004.md)  
    + [常量](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/coding/constant_005.md)  
    + [函数设计](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/coding/function_006.md)  
    + [IDE的选择](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/coding/ide_007.md)  
    + [编码规范的一些示例](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/coding/example_008.md)  

* [数据库设计和操作查询规范](https://github.com/tinyphporg/tinyphp-docs/tree/master/docs/sql)
    + [查询规范](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/sql/select_001.md)
    + [库和表的规范](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/sql/dbtable_002.md)
    + [数据库设计原则](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/sql/design_003.md)
    + [数据库的配置优化](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/sql/optimization_004.md)
* [团队编码规范](https://github.com/tinyphporg/tinyphp-docs/tree/master/docs/team)
    + [核心点](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/team/README.md#%E6%A0%B8%E5%BF%83%E7%82%B9)
    + [对于tinyphp的几个清醒认识](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/team/README.md#%E5%AF%B9%E4%BA%8E%E6%A1%86%E6%9E%B6%E7%9A%84%E5%87%A0%E4%B8%AA%E6%B8%85%E9%86%92%E8%AE%A4%E8%AF%86)
    + [tinyphp的适用场景与理念](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/team/README.md#tinyphp%E7%9A%84%E9%80%82%E7%94%A8%E5%9C%BA%E6%99%AF%E4%B8%8E%E7%90%86%E5%BF%B5)
    + [MVC的协作规范](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/team/README.md#mvc%E7%9A%84%E5%8D%8F%E4%BD%9C%E8%A7%84%E8%8C%83)
    + [tinyphp的系统设计原则](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/team/README.md#tinyphp%E7%9A%84%E7%B3%BB%E7%BB%9F%E8%AE%BE%E8%AE%A1%E5%8E%9F%E5%88%99)
* [框架配置手册](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/) 
    * [Index/入口文件:    public/index.php](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/index.md)
    * [Application/应用程序: application/](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/application.md)    
    * [Runtime/运行时环境: runtime/](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/runtime.md)    
        * [Environment/运行时环境参数](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/runtime_env.md)  
        * [ExceptionHandler/异常处理](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/runtime_exception.md)   
        * [Autoloader/自动加载](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/runtime_autoloader.md)   
        * [Container/容器](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/runtime_container.md)   
        * [EventManager/事件管理](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/runtime_event.md)   
    * [Proptrites/应用的属性配置文件:application/config/profile.php](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/profile.md)
        * [Debug/调试模式配置](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/debug.md)
        * [Bootstrap/引导程序配置:application/events/Bootstrap.php](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/bootstrap.md)
        * [Lang/语言包配置:application/lang](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/lang.md)
        * [Data/数据源配置:/application/data](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/data.md)
        * [Cache/缓存配置:runtime/cache](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/cache.md)
        * [Router/路由器配置](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/mvc_router.md)
        * [Logger/日志收集配置:runtime/log](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/logger.md)
        * [Configuration/配置类配置](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/configuration.md)
        * [Builder/打包单文件的配置](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/builder.md)
        * [Daemon/守护进程配置](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/daemon.md)
        * [Filter/过滤器配置](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/filter.md)
        * [Event/MVC事件配置](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/mvc_event.md)
        * [Controller/控制器配置:application/controllers/](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/mvc_controller.md)
        * [Model/模型配置:application/models/](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/mvc_model.md)
        * [Viewer/视图配置:application/views/](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/mvc_viewer.md)
        * [Dispatcher/派发器配置:application/views/](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/mvc_dispatcher.md)
        * [Request/请求配置:HttpRequest](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/mvc_request.md)
        * [Response/响应配置:HttpResponse](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/manual/mvc_response.md)
    
* [框架标准库参考](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/)
    * [Tiny：工具包](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/tiny.md)
    * [Tiny\Runtime：运行时](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/runtime.md)
    * [Tiny\Build：打包](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/build.md)
    * [Tiny\Cache：缓存](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/cache.md)
    * [Tiny\Config：配置](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/config.md)
    * [Tiny\Console：命令行](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/console.md)
    * [Tiny\Data：数据层](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/data.md)
    * [Tiny\Filter：过滤器](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/filter.md)   
    * [Tiny\Image：图片处理](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/image.md)
    * [Tiny\Lang：语言包](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/lang.md)
    * [Tiny\Log：日志处理](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/log.md)
    * [Tiny\MVC：MVC](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/mvc.md)
    * [Tiny\Net：网络](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/net.md)
    * [Tiny\String：字符处理](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/lib/string.md) 
   
* [UI库参考](https://github.com/tinyphporg/tinyphp-docs/blob/master/docs/ui/)                     


