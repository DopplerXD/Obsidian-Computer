## 项目介绍

基于鱼皮OJ [https://www.codefather.cn/course/1790980707917017089](https://www.codefather.cn/course/1790980707917017089) 和开源社区系统技术派 [https://github.com/itwanger/paicoding](https://github.com/itwanger/paicoding) 的算法学习平台。在线代码评测和博客系统（类似 Luogu）。

![Screenshot 2025-02-16 at 15.20.28.png](attachment:e8d9071b-76dd-4287-9c85-aff483864596:Screenshot_2025-02-16_at_15.20.28.png)

![Screenshot 2025-02-16 at 15.19.50.png](attachment:fa50b816-2070-4496-a14c-beda8a1ca13a:Screenshot_2025-02-16_at_15.19.50.png)

![Screenshot 2025-02-16 at 15.19.18.png](attachment:d2e1b7f7-0b97-49df-8e20-02e8617799f1:Screenshot_2025-02-16_at_15.19.18.png)

## 项目架构

[https://paicoding.com/article/detail/208](https://paicoding.com/article/detail/208)

![image.png](attachment:2d1d8899-a8ee-4764-be8f-af9f940e2235:image.png)

![image.png](attachment:c1f60e7a-82ee-418c-944b-8aa470c2acf1:image.png)

整个系统的后端分为：

- 用户服务：提供用户登录、用户的增删改查等管理功能
- 题目服务：提供题目的增删改查管理、题目提交功能
- 判题服务：提供判题功能，调用代码沙箱并比对判题结果
- 代码沙箱：提供编译执行代码、返回结果的功能
- 公共模块：提供公共代码，比如数据模型、全局请求响应封装、全局异常处理、工具类等
- 网关服务：提供统一的 API 转发、聚合文档、全局跨域解决等功能
- 题解服务：提供题解发布功能、支持用户评论、点赞、收藏等功能

各模块之间的关系，3 个核心：

1. 由网关服务集中接受前端的请求，并转发到对应的业务服务。
2. 判题服务需要调用题目服务获取题目信息和测试用例、调用代码沙箱完成代码的编译和执行并比对结果，服务间通过 Open Feign 相互调用。
3. 所有服务都需要引入公共模块。