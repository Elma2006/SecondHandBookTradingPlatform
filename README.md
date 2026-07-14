# 校园二手书交易平台
## 项目简介
校园二手书交易平台是一个基于 Spring Boot + Vue.js 构建的二手书在线交易系统，旨在为高校学生提供便捷的二手书买卖服务，促进图书资源的循环利用。

该系统实现了图书信息查询、图书发布、购物车管理、订单交易、用户反馈等完整功能，采用关系型数据库 MySQL 进行数据存储，具备良好的安全性和可操作性。

## 技术栈
### 后端技术
技术 版本 说明 Java 1.8 编程语言 Spring Boot 2.2.2.RELEASE 后端框架 MyBatis Plus 2.3 ORM 框架 MySQL 8.0+ 数据库 Apache Shiro 1.3.2 安全框架 FastJSON 1.2.8 JSON 处理 Hutool 4.0.12 工具类库 Apache POI 3.9 Excel 处理 Baidu AI SDK 4.4.1 百度人工智能服务

### 前端技术
技术 说明 Vue.js 前端框架 LayUI UI 组件库 ElementUI UI 组件库 Bootstrap CSS 框架 jQuery JavaScript 库 Tinymce 富文本编辑器

## 项目结构
## 数据库设计
### 数据库信息
- 数据库名称 ：t283
- 字符集 ：utf8mb3
- 存储引擎 ：InnoDB
### 数据表清单
表名 说明 关键字段 users 管理员表 id, username, password, role yonghu 用户表 id, username, password, yonghu_name, yonghu_phone tushu 图书表 id, tushu_name, tushu_photo, tushu_zuozhe, tushu_new_money tushu_order 订单表 id, tushu_order_uuid_number, tushu_id, yonghu_id, tushu_order_types cart 购物车表 id, yonghu_id, tushu_id, buy_number tushuqiugou 图书求购表 id, tushuqiugou_name, yonghu_id, tushuqiugou_types tushu_liuyan 图书留言表 id, tushu_id, yonghu_id, tushu_liuyan_text, reply_text address 收货地址表 id, yonghu_id, address_name, address_phone, address_dizhi chat 用户反馈表 id, yonghu_id, chat_issue, chat_reply, zhuangtai_types news 公告信息表 id, news_name, news_content, news_types dictionary 字典表 id, dic_code, dic_name, code_index, index_name token Token 表 id, userid, username, token, expiratedtime

### 数据库关系图
## 功能模块
### 1. 用户模块
- 用户注册/登录
- 用户信息管理
- 密码重置
- 余额充值
- 个人中心
### 2. 图书模块
- 图书列表展示
- 图书搜索/筛选
- 图书详情查看
- 图书发布/编辑
- 图书上下架管理
### 3. 购物车模块
- 添加商品到购物车
- 修改购买数量
- 删除购物车商品
- 批量结算
### 4. 订单模块
- 订单创建
- 订单支付
- 订单发货
- 订单收货
- 订单退款
### 5. 留言模块
- 图书留言
- 留言回复
### 6. 求购模块
- 发布求购信息
- 求购列表查看
- 求购状态管理
### 7. 反馈模块
- 用户反馈提交
- 管理员回复
- 反馈状态管理
### 8. 公告模块
- 公告列表展示
- 公告详情查看
- 公告管理（管理员）
### 9. 系统管理
- 字典管理
- 轮播图配置
- 文件上传管理
## 运行说明
### 环境要求
- JDK 1.8+
- MySQL 8.0+
- Maven 3.6+
### 启动步骤
1. 创建数据库
   
   执行 SQL 脚本初始化数据库：
2. 配置数据库连接
   
   修改 back/src/main/resources/application.yml ：
3. 构建项目
4. 运行项目
5. 访问地址
   
   - 前端页面： http://localhost:8080/ershoushujiaoyipingtai/
   - 后端 API： http://localhost:8080/ershoushujiaoyipingtai/api/
### 测试账户
角色 用户名 密码 管理员 admin 123456 用户 用户1 123456 用户 用户2 123456 用户 用户3 123456

## API 接口说明
### 用户接口
接口路径 方法 说明 是否需要登录 /yonghu/login POST 用户登录 否 /yonghu/register POST 用户注册 否 /yonghu/session GET 获取当前用户 是 /yonghu/logout GET 退出登录 是 /yonghu/resetPass GET 忘记密码 否

### 图书接口
接口路径 方法 说明 是否需要登录 /tushu/list GET 前端图书列表 否 /tushu/detail/{id} GET 图书详情 否 /tushu/add POST 添加图书 是 /tushu/page GET 后端图书列表 是 /tushu/update POST 修改图书 是 /tushu/delete POST 删除图书 是

### 订单接口
接口路径 方法 说明 是否需要登录 /tushuOrder/list GET 订单列表 是 /tushuOrder/add POST 创建订单 是 /tushuOrder/update POST 更新订单 是

### 购物车接口
接口路径 方法 说明 是否需要登录 /cart/list GET 购物车列表 是 /cart/add POST 添加商品 是 /cart/update POST 修改数量 是 /cart/delete POST 删除商品 是

## 安全机制
### 登录认证
- 使用 Token 机制进行身份认证
- Token 存储在数据库中，包含过期时间
- 请求头携带 Token 进行接口访问
### 权限控制
- 使用自定义注解 @LoginUser 和 @APPLoginUser 标记需要登录的接口
- 使用 @IgnoreAuth 标记不需要登录的接口
- 通过拦截器 AuthorizationInterceptor 统一处理权限校验
- 管理员和普通用户拥有不同的角色权限
### 数据安全
- 使用 MyBatis Plus 防止 SQL 注入
- 密码明文存储（注：实际生产环境应使用加密存储）
- 逻辑删除机制，数据不会真正删除
## 特色功能
1. 图书分类浏览 ：支持按图书类型筛选浏览
2. 购物车功能 ：支持批量购买和数量修改
3. 订单状态追踪 ：完整的订单状态流转（待支付、已支付、已发货、已收货）
4. 用户反馈系统 ：用户可提交问题，管理员进行回复
5. 图书求购 ：用户可发布求购信息，等待卖家联系
6. 图书留言 ：支持用户对图书进行留言和回复
7. 字典管理 ：灵活的字典配置，支持动态添加数据类型