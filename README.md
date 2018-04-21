# Web 应用基础 Project 2: Alice 的艺术品网站设计（续）

## 1 背景介绍

前略，Alice 已经完成了艺术品网站的前端设计部分，然而此时该网站只是一个空壳，并不能提供任何实际功能。于是她邀请擅长后端的 Ayaya 来帮她完成后台的设计。

![ayaya](screenshots/ayaya.png)

于是 Ayaya 给出了如下的要求，并表示：

> 才...才不是特别为你做的呢！
>
> 哼，就算你帮我实现我也不会高兴的！

接下来该怎么做，我想各位心里有数（笑

## 2 本文档的正确使用方法

先仔细阅读[项目需求](#项目需求)了解本 PJ 的大体要求，然后对照着[功能点详情](#功能点详情)一步步完成 PJ，最后根据[详细评分点](#详细评分点)估算出自己的分数并采取相应的行动。

## 3 项目需求

### 3.1 前端视觉效果

普通玩家：这是 PJ1 已经完成的部分，PJ2 不做额外要求，直接复用即可。

高级玩家：PJ2 不再限制前端框架的使用，请自由发挥，制作出令人耳目一新的显示效果吧。

### 3.2 多语言支持

所有页面与数据统一使用 UTF-8 编码，能够正确支持多语言的显示与输入（一般情况下用中文进行测试即可）。

### 3.3 浏览器兼容性

普通玩家：在最新版 Chrome 下正常显示与使用即可。

高级玩家：在力所能及的范围内尽可能多地兼容各主流浏览器。

### 3.4 代码风格

* 做到页面、样式、脚本的分离，不允许把一个页面的所有代码都写在一个文件内。
* 代码有适当的注释及缩进。
* 外部资源的引用使用相对路径而不是绝对路径。

### 3.5 后端技术选择

普通玩家：使用 PHP 实现后端逻辑，本 PJ 的要求不必使用任何第三方框架就可以轻松实现。

高级玩家：使用任何你喜欢的后端语言与框架，但需在面试时简述你选择该语言/框架的原因并回答 TA 的一些问题。**严禁无脑拷贝各种地方找来的代码，TA 会详细询问功能实现的原理**。

### 3.6 数据库选择

普通玩家：使用 MySQL 免费版数据库。本文档会提供该 PJ 基于 MySQL 的数据库框架与初始填充数据，无需自己设计数据库，只需理解已有的数据库设计并对其存储的内容进行相应的增删改查即可。

高级玩家：使用任何你喜欢的数据库（包括非关系型数据库），但需自己完成数据库的设计与初始数据填充，同时在面试时简述你选择该数据库的原因以及你的设计思路并回答 TA 的一些问题。

### 3.7 网站质量

* 任何页面在所要求的浏览器控制台中不得出现报错。
* 任何本地加载的页面均应迅速显示（原则上在 1 秒内完成加载）。
* 能够对普通用户的非法操作进行正确的响应与提示（不用考虑恶意用户精心构造的攻击），不得直接任其崩溃报错。

### 3.8 网站安全

普通玩家：不要求。

高级玩家：尽可能地防范各类针对网站的网络安全攻击（如 SQL 注入、XSS 攻击、CSRF 攻击、文件上传木马等），并着力提高网站数据的安全性（如数据库中密码的单向加盐哈希存储等）。

### 3.9 部署

普通玩家：在本地环境正常运行即可。

高级玩家：将你的网站部署到任何你喜欢的云服务器，从而可以像真正的网站那样直接通过 IP 地址或域名进行访问。

### 3.10 其他

**严禁抄袭**，不然你会被 Ayaya 柴刀（被 TA 打零分。某些复杂功能可以参考一些既有的优秀代码，但需完全理解后再使用，TA 在面试时会比较关注这些复杂功能的实现，不要存在侥幸心理。

### 3.11 提交

将所有的源代码文件打包上传至学院课程 FTP，压缩包请以 `学号-姓名` 这样的格式来命名。**本 PJ 无需使用 Git 来提交**，但推荐在本地使用 Git 进行版本管理。

## 4 功能点详情

### 4.1 功能概述

这里通过一名用户对该网站的典型使用流程来对网站的功能做一总体概述。

用户首先进入网站主页，此时他可以自由搜索、浏览网站内的各艺术品信息，但不能进行购买、发布等操作。用户进入注册页面，注册登录成功后即成为网站的正式用户，可以使用网站的全部功能。一旦注册，此后用户再次访问该网站时只需登录即可。

已登录的用户在浏览艺术品时可将其添加到自己的购物车，之后在购物车页面完成正式的下单购买。当然，用户首先应在个人页面对其余额进行充值，只有余额足够才能购买成功。

除了购买艺术品，已登录的用户也可以前往发布页面发布新的艺术品，新的艺术品一经发布即可在网站上被任何用户搜索/查看到，并可以被其他用户购买。其他用户成功购买该艺术品后，购买人所支付的费用会直接转入发布人的余额中，没有中间商赚差价。

### 4.2 导航栏

导航栏包含用户栏、Logo/标语栏与足迹栏三部分，需显示在所有页面的最上方（在不同页面下的呈现内容与效果可自行调整），具体样式在 PJ1 中已作阐述，这里不再赘述，PJ2 重点考察足迹栏的实现与登出功能。以下是详细功能点：

* 足迹栏应完整地呈现用户访问网站的足迹。如：用户从首页进入搜索页面，则足迹栏显示“首页 -> 搜索”；之后用户点击某一搜索结果进入商品详情页，此时足迹栏应显示“首页 -> 搜索 -> 详情”；之后用户返回到搜索页面，此时足迹栏应显示“首页 -> 搜索”，以此类推。足迹栏中的条目应可以点击并进入相应页面。
* 已登录用户可以通过导航栏上的“登出”按钮登出为未登录状态。

### 4.3 登录页面/悬浮框

登录页面为用户提供登录入口。由于其功能简单，因此可以用单独的页面也可以用悬浮框的形式来呈现。以下是详细功能点：

* 用户输入用户名与密码之后，点击登录，前端检查用户是否输入了用户名与密码，若有任意一项为空就不允许提交并提示用户。成功提交后，后端对用户名和密码进行校验并经由前端返回登录成功或失败的相关信息。
* 登录成功后，应相应地改变导航栏呈现的内容（如将“登录”按钮变为“登出”按钮并显示当前已登录的用户名等）。如果登录是一个单独页面，则应在提示登录成功后跳转到登录前的页面；如果登录以悬浮框形式呈现，则应在提示登录成功后移除该悬浮框。

### 4.4 注册页面

注册页面提供注册新用户的功能。以下是详细功能点：

* 注册项必须至少包含用户名、邮箱、密码、重复输入密码、电话、地址这六项。
* 关于输入项的具体限制（需在前端进行检查）如下：
  * 所有输入项不得为空
  * 邮箱必须符合邮箱命名规则
  * 密码长度必须大于等于 6 位，且不得为纯数字
  * 用户两次输入的密码应相同，否则不允许提交
* 如果系统中已存在同用户名的用户，则应提示选取新的用户名。
* 提交成功后，系统将创建一个新用户并存入数据库，同时自动以该用户身份登录。

### 4.5 首页页面

首页页面是用户直接访问该网站时呈现的第一个页面，提供展示最热、最新艺术品的功能。以下是详细功能点：

* 热门艺术品展示：显示访问量最多的艺术品信息（至少 3 个），使用 PJ1 中的轮播样式呈现，需展示出相应艺术品的名称、简介与图片，点击即可进入相应艺术品的详情页面。
* 最新艺术品展示：显示最新发布的艺术品信息（至少 3 个），呈现样式不限，需展示出相应艺术品的名称、简介与图片，点击即可进入相应艺术品的详情页面。

### 4.6 艺术品详情页面

艺术品详情页面详细地展示了艺术品的所有信息，并提供将该艺术品加入购物车的功能。以下是详细功能点：

* 参照 PJ1 的样式展示出具体艺术品的所有信息。不允许为每个艺术品单独写一个页面，而应写一个通用的艺术品详情页面，并根据请求参数从数据库中读取相应数据填充至该页面内。
* 每访问一次某艺术品的详情页面，该艺术品的访问量加一，访问量也应随艺术品的其他信息一并展示在该页面。
* 该页面应提供将该艺术品加入当前用户购物车的功能，但需遵循以下限制：
  * 未登录用户不得执行加入购物车的操作
  * 如果该艺术品已在当前用户的购物车中，则不能重复加入购物车
  * 已售出的艺术品需显示“已售出”并不能被任何用户加入购物车
  * 已加入其他用户购物车但尚未成功下单购买的艺术品仍可以被当前用户加入购物车

### 4.7 搜索与搜索结果页面

搜索入口可以以搜索框的形式集成在导航栏中，也可单独制作搜索页面。用户执行搜索后会进入相应的搜索结果页面。以下是详细功能点：

* 搜索选项：用户可选择根据艺术品的名称、简介或作者名中的一项或多项进行关键词搜索。若有余力也可添加更多选项。
* 排序：用户可选择根据艺术品的价格或点击量进行搜索结果的排序。若有余力也可添加更多选项。
* 分页：搜索结果较多时需分页显示，每一页至少显示 5 个结果；需要显示总页面数与当前页并提供翻页/跳转功能，具体样式不限，但要求翻页/跳转使用 AJAX 实现，不要刷新整个页面。

### 4.8 艺术品发布/信息修改页面

艺术品发布页面为已登录的用户提供发布新艺术品或修改已发布的艺术品信息的功能。以下是详细功能点：

* 发布/修改表单应至少包含艺术品名称、作者、简介、年份、流派、尺寸（包括长度与宽度）、价格与图片这八项。如果是修改原有的艺术品，则原有艺术品的信息应被预填充到相应的表单项中（包括原图片的预览）。
* 关于输入项的限制（需在前端进行检查）如下：
  * 所有输入项不得为空
  * 年份必须为整数
  * 长度与宽度必须为正数
  * 价格必须为正整数
* 图片上传使用文件上传控件实现，用户选择文件后应在本地显示该图片的预览。
* 发布/修改成功后，系统将创建一个新艺术品并将其存入数据库（同时将图片保存在服务器中）/修改数据库中原有艺术品的信息（同时用新图片替换服务器中原有的图片），并返回发布/修改成功的信息。

### 4.9 购物车页面

购物车页面展示当前用户购物车中的艺术品，并提供下单功能。以下是详细功能点：

* 显示当前用户已加入购物车的艺术品列表，呈现样式不限，需展示出艺术品的名称、简介、图片与当前价格（不存在数量，因为每件艺术品都是唯一的）。
* 购物车中的艺术品可以被移出购物车。
* 购物车应计算出其中所有艺术品当前的总价。
* 用户点击下单后，系统应检查当前用户的余额是否足够支付，若不足则应拒绝下单并提示用户，同时还要检查在下单前购物车内的艺术品是否发生过变动（如被删除、被其他用户买走或价格等信息被修改），并作出相应的提示，不得产生成功购买不存在或已售出的艺术品这类异常行为。
* 下单成功后，系统扣除用户的余额并在数据库中建立相应的订单，该订单可以在个人页面查看。被成功购买的艺术品不应再出现在搜索结果中，也不应在首页展示，但仍可以通过详情链接访问到。

### 4.10 个人页面

个人页面包含了已登录用户的所有个人相关信息。以下是详细功能点：

* 个人基本信息（注册时所提供的信息）展示。
* 个人余额展示与充值功能：新注册用户的初始余额为零，可通过一个输入框和按钮进行余额充值，充值金额必须为正整数，一旦充值成功系统即更新数据库中的余额值同时反映在余额展示中。
* 我的艺术品列表：该列表显示当前用户发布的所有艺术品，呈现样式不限，需展示出艺术品的名称与上传日期，并附有修改与删除按钮。点击艺术品名称可跳转到相应艺术品的详情页面；点击修改跳转到相应艺术品信息修改页面；点击删除会弹框确认是否删除，确认后系统将该艺术品从数据库中删除（同时删除该艺术品对应的图片文件）。注意：已售出的艺术品不得进行修改或删除操作。
* 我的订单列表：该列表显示当前用户的所有购买订单，呈现样式不限，需展示出订单编号、订单中包含的艺术品信息（包括艺术品的名称及相应的详情页链接）、订单时间与订单总金额。
* 我的卖出列表：该列表显示当前用户的所有已卖出艺术品，呈现样式不限，需展示出艺术品名称及相应的详情页链接、卖出时间、卖出时的价格与购买人基本信息（包括用户名、邮箱、电话与地址）。

### 4.11 页面权限要求

不为未登录用户提供进入个人页面、购物车页面、艺术品发布/信息修改页面的入口。当未登录用户强行通过 URL 直接访问这些页面时应提示登录。

## 5 详细评分点

关于本 PJ 的评分原则：**本 PJ 仅按功能点评分**，即只关注实现的功能而不关注实现的途径和方法（当然抄袭是不行的！）。**本 PJ 基础分 100 分，满分也是 100 分**，即高级功能的分数仅用于弥补基础部分的不足，而不会另外加分。下表列出了详细评分点（其中的“总体功能”指页面总体设计合理、逻辑正确，~~基本是送分的~~）：

<table>
        <thead>
        <tr>
            <th>页面/模块</th>
            <th>功能点</th>
            <th>分值</th>
        </tr>
        </thead>
        <tbody>
        <tr>
            <td rowspan="3">导航栏</td>
            <td>足迹栏</td>
            <td>3</td>
        </tr>
        <tr>
            <td>登出功能</td>
            <td>1</td>
        </tr>
        <tr>
            <td>总体功能</td>
            <td>5</td>
        </tr>
        <tr>
            <td rowspan="3">登录页面</td>
            <td>输入合法性检查</td>
            <td>2</td>
        </tr>
        <tr>
            <td>登录结果提示</td>
            <td>2</td>
        </tr>
        <tr>
            <td>总体功能</td>
            <td>2</td>
        </tr>
        <tr>
            <td rowspan="3">注册页面</td>
            <td>输入合法性检查</td>
            <td>2</td>
        </tr>
        <tr>
            <td>用户名已存在的提示</td>
            <td>2</td>
        </tr>
        <tr>
            <td>总体功能</td>
            <td>2</td>
        </tr>
        <tr>
            <td rowspan="3">首页页面</td>
            <td>热门艺术品展示</td>
            <td>3</td>
        </tr>
        <tr>
            <td>最新艺术品展示</td>
            <td>3</td>
        </tr>
        <tr>
            <td>总体功能</td>
            <td>3</td>
        </tr>
        <tr>
            <td rowspan="3">艺术品详情页面</td>
            <td>艺术品信息展示</td>
            <td>3</td>
        </tr>
        <tr>
            <td>访问量更新</td>
            <td>1</td>
        </tr>
        <tr>
            <td>加入购物车功能</td>
            <td>3</td>
        </tr>
        <tr>
            <td rowspan="4">搜索模块</td>
            <td>搜索选项的正确实现</td>
            <td>6</td>
        </tr>
        <tr>
            <td>搜索结果的正确排序</td>
            <td>2</td>
        </tr>
        <tr>
            <td>分页功能</td>
            <td>4</td>
        </tr>
        <tr>
            <td>总体功能</td>
            <td>4</td>
        </tr>
        <tr>
            <td rowspan="3">艺术品发布/信息修改页面</td>
            <td>输入合法性检查</td>
            <td>2</td>
        </tr>
        <tr>
            <td>图片预览</td>
            <td>2</td>
        </tr>
        <tr>
            <td>总体功能</td>
            <td>3</td>
        </tr>
        <tr>
            <td rowspan="3">购物车页面</td>
            <td>购物车列表展示与总价计算</td>
            <td>4</td>
        </tr>
        <tr>
            <td>从购物车中移除艺术品的功能</td>
            <td>1</td>
        </tr>
        <tr>
            <td>正确的下单功能</td>
            <td>8</td>
        </tr>
        <tr>
            <td rowspan="5">个人页面</td>
            <td>个人信息展示</td>
            <td>1</td>
        </tr>
        <tr>
            <td>余额展示与充值</td>
            <td>2</td>
        </tr>
        <tr>
            <td>我的艺术品列表</td>
            <td>4</td>
        </tr>
        <tr>
            <td>我的订单列表</td>
            <td>4</td>
        </tr>
        <tr>
            <td>我的卖出列表</td>
            <td>4</td>
        </tr>
        <tr>
            <td>权限模块</td>
            <td>未登录时某些页面拒绝访问并提示登录</td>
            <td>2</td>
        </tr>
        <tr>
            <td rowspan="4">总体要求</td>
            <td>在所要求的浏览器下无报错正常工作</td>
            <td>4</td>
        </tr>
        <tr>
            <td>多语言支持</td>
            <td>2</td>
        </tr>
        <tr>
            <td>代码风格良好</td>
            <td>2</td>
        </tr>
        <tr>
            <td>性能良好</td>
            <td>2</td>
        </tr>
        <tr>
            <td rowspan="9">高级功能</td>
            <td>兼容各大主流浏览器</td>
            <td>3</td>
        </tr>
        <tr>
            <td>网站安全</td>
            <td>5</td>
        </tr>
        <tr>
            <td>云端部署</td>
            <td>2</td>
        </tr>
        <tr>
            <td>表单验证码功能</td>
            <td>2</td>
        </tr>
        <tr>
            <td>上传图片时的在线裁剪调整功能</td>
            <td>2</td>
        </tr>
        <tr>
            <td>站内信功能，用户之间可发送站内信，且应区分已读与未读的站内信</td>
            <td>5</td>
        </tr>
        <tr>
            <td>（基于站内信）用户可以订阅/取消订阅另一名用户的发布行为，当已订阅的用户发布新艺术品时系统会发送站内信进行提醒</td>
            <td>5</td>
        </tr>
        <tr>
            <td>在线多人聊天室功能，在线用户可进入聊天室进行实时聊天</td>
            <td>4</td>
        </tr>
        <tr>
            <td>其他没有提到的功能</td>
            <td>酌情给分</td>
        </tr>
        </tbody>
</table>

## 附

### 关于随附资源的使用说明

本 PJ 为普通玩家准备了已设计好的 MySQL 数据库表构建语句与初始的艺术品数据。其中位于 [resources/sql](resources/sql/) 文件夹下的几个 .sql 文件（其实就是纯文本文件）包含了本 PJ 基础功能中所需的各个表的构建语句及初始数据，你只需在 MySQL 中先创建一个数据库，之后直接在该数据库中执行这些文件中的语句即可（具体方法可查阅网上资料或在 lab 课时请教任意一位 TA）；而 [resources/img](resources/img/) 文件夹则包含了与刚才所新建立的数据库中的初始数据所对应的图片。

请注意：如果你使用了所提供的构建语句，请务必完全理解这些表的结构及其字段的含义。当然，你完全可以根据自己的理解与需要自由地修改这些表的结构。

### 问题与解决

遇到任何技术问题，请先 [Google](https://www.google.com/)（最好使用英文来表述你的问题，这样你可以得到更多有用的信息）；如果不能解决，可以请教任何一位 TA 或直接在课程群中提问。

对本文档有任何问题，请微信联系 TA 朱子秋。

### Deadline

2018.06.21 夏至日

![debug](screenshots/debug.png)
