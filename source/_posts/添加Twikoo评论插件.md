---
title: 添加Twikoo评论插件
date: 2023-02-16 14:10:07
tags: hexo
comments:
  enable: true
  type: twikoo
type: "categories"
categories:
  - 工具
---

### 前言

添加评论模块不仅仅是添加一个组件那么简单，简言之就是涉及到与后端的交互，当然如今的网站评论系统已经做得非常成熟了，搭配一台云服务器，即可自动生成。

通过对比不同的评论系统，发现 twikoo 支持自动拉取 QQ 头像、图文评论、点赞回复、匿名评论等等功能，样式上也简单美观，所以本站选用 twikoo

- [Twikoo 文档](https://twikoo.js.org/)

### 腾讯云部署

#### 1.进入活动专区

- [腾讯云](https://cloud.tencent.com/act) 或 [云开发 CloudBase](https://cloud.tencent.com/act/free)

![1](1.png)

#### 2.选择云开发

![2](2.png)

#### 3.进入云开发控制台

![4](4.png)

#### 4.新建环境

- 地域最好选择上海，如果选择广州的话，需要在`twikoo.init()`时额外指定环境 `region: "ap-guangzhou"`
- 环境名称无所谓，符合要求即可

  ![3](3.png)

#### 5.环境初始化

- 进入刚刚创建的环境，选择环境-->登录授权，启用“匿名登录”
- 选择环境-->安全配置，将网站域名添加到“WEB 安全域名”

  ![5](5.png)

- 选择环境-->环境总览，复制环境 ID（用于 fluid 配置）

#### 6.开始手动部署 twikoo

- [Twikoo 部署文档](https://twikoo.js.org/quick-start.html#%E6%89%8B%E5%8A%A8%E9%83%A8%E7%BD%B2)
- 选择基础服务-->云函数，新建云函数，按如图所示配置基础信息

  ![6](6.png)

  - 下一步，函数配置，将函数代码替换为`exports.main = require('twikoo-func').main`
  - 创建完成后，点击“twikoo"进入云函数详情页，进入“函数代码”标签，点击“文件 - 新建文件”，输入 `package.json`，回车
  - 将代码`{ "dependencies": { "twikoo-func": "1.6.10" } }`粘贴到代码框中，点击“保存并安装依赖”（注：此处的依赖版本需与官方最新版本保持一致）
  - 点击测试，将模板替换为请求对象（可保存模板）

  ```bash
  {
    "event": "COMMENT_SUBMIT",
    "accessToken": "b45b2e4c9ec943b884eb4cd9c044c4cd",
    "nick": "云景",
    "mail": "2289350377@qq.com",
    "link": "",
    "ua": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/110.0.0.0 Safari/537.36",
    "url": "/api.html",
    "href": "https://twikoo.js.org/api.html#example-3",
    "comment": "<p>414</p>\n"
    }
  ```

### hexo fluid 配置

打开`_config.fluid.yml` 文件

- 开启评论需要在主题配置中开启并指定评论模块：

```bash
post:
  comments:
    enable: true
    type: twikoo
```

- 然后在下方设置对应评论模块的参数：

```bash
twikoo:
  enable: true
  visitor: true
  envId: yby-7glx8ltu7f9c49a0
  region: ap-shanghai
  path: window.location.pathname
```

### 参考

> [为 Hexo 博客添加 Twikoo 评论](https://weilong98.com/post/Twikoo/)

> [Hexo 添加 Twikoo 评论插件](https://cloud.tencent.com/developer/article/2063344)
