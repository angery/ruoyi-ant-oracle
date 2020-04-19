<h1 align="center">RuoYi Ant ORACLE</h1>

文档：http://doc.rycloud.zmrit.com

- 预览: http://ruoyi.ant.zmrit.com
- 独有的字典用法
- 独有的自定义默认排序
- 监控类外链不宜对外暴露，可以设置白名单，故不在演示系统展示，可以参看 [ruoyi-ant redi监控](http://redis.ant.zmrit.com/)



本项目fork自ant design vue pro，有兴趣直接[传送](https://pro.loacg.com/)
----



运行项目需要启动后端ruoyi-cloud-oracle，[传送门](https://github.com/angery/ruoyi-cloud-oracle.git)
源码地址:
- [Github](https://github.com/angery/ruoyi-ant-oracle)
- [Gitee](https://gitee.com/angery/ruoyi-ant-oracle)

Overview
----

![工作台-多标签模式](https://static-2.loacg.com/open/static/github/20190224163345.jpg)

![工作台+设置菜单](https://static-2.loacg.com/open/static/github/20181126112124.png)

![个人设置](https://static-2.loacg.com/open/static/github/20180916-134251.png)


项目下载和运行
----

- 拉取项目代码
```bash
git clone https://github.com/angery/ruoyi-ant-oracle.git
cd ruoyi-ant-oracle
```

- 安装依赖
```
yarn install
```

- 开发模式运行
```
yarn run serve
```

- 编译项目
```
yarn run build
```

- Lints and fixes files
```
yarn run lint
```
## 平台简介
来自 https://github.com/zhangmrit/ruoyi-cloud MySQL改造成oracle
### 文档 http://doc.rycloud.zmrit.com

### 源码
- [Github](https://github.com/angery/ruoyi-cloud-oracle)
- [Gitee](https://gitee.com/angery/ruoyi-cloud-oracle.git)

#### 分支说明

- **master** spring原生方式，使用eureka做注册中心和spring config做配置中心
- **nacos** 集成spring-cloud-alibaba 使用nacos做注册中心和配置中心

本项目FORK自  [zhangmrit/ruoyi-cloud](https://github.com/zhangmrit/ruoyi-cloud)

依次绑定host：

127.0.0.1 eureka7001.com

127.0.0.1 gateway.com

如果要使用eureka集群，请依次绑定eureka7002.com,eureka7003.com后修改各项目中的注释部分

```
ruoyi-cloud
|
├──ruoyi-common --通用包
|  |
|  ├──ruoyi-common-core --核心工具包
|  |
|  ├──ruoyi-common-redis --redis工具包
|  |
|  ├──ruoyi-common-log --日志工具包
|  |
|  ├──ruoyi-common-auth --权限工具包
|
├──ruoyi-config --cloud统一配置中心
|
├──ruoyi-eureka --注册中心
|
├──ruoyi-gateway --网关
|
├──ruoyi-service-api --服务api模块
|  |
|  ├──ruoyi-system-api --系统业务api
|
├──ruoyi-service --微服务
|  |
|  ├──ruoyi-system --系统业务
|  |
|  ├──ruoyi-auth --授权中心
|  |
|  ├──ruoyi-gen --代码生成
|  |
|  ├──ruoyi-dfs --文件
|
├──ruoyi-tool --工具
|  |
|  ├──ruoyi-monitor --监控中心
|
├──ruoyi-ant --前端 使用ant design框架

```



启动顺序：
- eureka
- config
- gateway
- system
- auth
- gen 可选
- dfs 可选

菜单sql有增加字段，以上传到sql文件
该分支是ant分支，前端使用ant-design-vue 项目地址 [ruoyi-ant-oracle](https://gitee.com/angery/ruoyi-ant-oracle)

monitor使用springadmin完成,目前只是最简单的用法,[详戳](http://doc.rycloud.zmrit.com/#/extra?id=%e7%9b%91%e6%8e%a7)

欢迎pr或者加入，给个star是最好的鞭策

##  请作者喝杯咖啡


![](https://images.gitee.com/uploads/images/2020/0215/113629_1cea6917_364035.png)

