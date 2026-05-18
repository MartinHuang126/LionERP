# LionERP - 拼多多1688铺货ERP系统

![LionERP Logo](docs/images/logo.png)

> 🦁 **LionERP** - 为拼多多商家打造的智能ERP系统，让铺货、订单、采购、售后、客服一站式管理！

---

## 📋 目录

- [项目简介](#项目简介)
- [核心功能](#核心功能)
- [技术栈](#技术栈)
- [项目结构](#项目结构)
- [开发计划](#开发计划)
- [安装和运行](#安装和运行)
- [人为节点介入清单](#人为节点介入清单)
- [API 对接说明](#api-对接说明)
- [参考文档](#参考文档)
- [贡献指南](#贡献指南)
- [许可证](#许可证)
- [联系方式](#联系方式)

---

## 项目简介

LionERP 是一个面向拼多多商家的 ERP 管理系统，主要功能是从 1688 市场铺货到拼多多店铺，并提供订单管理、自动采购、发货同步、售后同步、客服机器人等一站式管理功能。

本项目参考市场上成熟的**妙手ERP**应用，采用分阶段实施策略，逐步完善功能，最终打造一个适合中小拼多多商家的轻量级ERP系统。

### 🎯 项目特色

- **专注拼多多+1688**：深度优化拼多多店铺管理和1688铺货流程
- **智能客服**：接入大模型（GPT/国内大模型），提供AI智能客服
- **开源免费**：基于MIT许可证开源，可自由定制功能
- **分阶段实施**：功能模块逐步开发，降低开发风险

---

## 核心功能

### 第一阶段（基础功能）✅

1. **商品铺货管理**
   - 从 1688 采集商品信息
   - 商品信息编辑和优化
   - 一键铺货到拼多多店铺
   - 商品素材本地化管理

2. **订单管理**
   - 拼多多订单自动同步
   - 订单自动匹配 1688 货源
   - 自动采购和下单
   - 订单状态跟踪

3. **发货同步**
   - 1688 发货信息自动同步
   - 自动回填拼多多发货信息
   - 物流信息实时更新

### 第二阶段（进阶功能）🚧

4. **售后管理**
   - 拼多多售后自动同步
   - 售后原因自动分析
   - 1688 售后自动申请
   - 售后进度跟踪

5. **货源管理**
   - 商品与 1688 货源关联
   - 货源一键替换
   - 多货源比价和选择
   - 货源稳定性监控

6. **多店铺管理**
   - 多店铺授权和管理
   - 多店铺订单统一处理
   - 多店铺商品统一管理

### 第三阶段（智能功能）🔮

7. **智能客服**
   - 接入拼多多客服系统
   - 接入大模型（GPT/国内大模型）
   - 自动回复常见问题
   - 人工客服协同

8. **数据分析**
   - 销售数据分析
   - 利润分析
   - 库存预警

9. **营销工具**
   - 批量修改商品信息
   - AI生成营销文案
   - 水印添加

---

## 技术栈

### 后端

| 技术 | 版本 | 用途 |
|------|------|------|
| .NET Core | 8.0 | Web API 框架 |
| Entity Framework Core | 8.0 | ORM 框架 |
| PostgreSQL | 14+ | 主数据库 |
| Redis | 7+ | 缓存数据库 |
| Hangfire | 1.8+ | 定时任务 |
| Swagger/OpenAPI | 6.0+ | API 文档 |
| AutoMapper | 12.0+ | 对象映射 |

### 前端

| 技术 | 版本 | 用途 |
|------|------|------|
| React | 18+ | 前端框架 |
| Ant Design Pro | 5.0+ | UI 组件库 |
| Redux Toolkit | 1.9+ | 状态管理 |
| React Router | 6.0+ | 路由管理 |
| Axios | 1.6+ | HTTP 客户端 |
| TypeScript | 5.0+ | 类型安全 |

### 开发工具

| 工具 | 用途 |
|------|------|
| Visual Studio 2022 | 后端开发 IDE |
| VS Code | 前端开发 IDE |
| Postman | API 测试 |
| Git | 版本控制 |
| GitHub | 代码托管 |
| Docker | 容器化部署 |

---

## 项目结构

```
LionERP/
├── src/
│   ├── LionERP.Core/                # 领域核心层
│   │   ├── Entities/               # 实体类
│   │   │   ├── Product.cs         # 商品实体
│   │   │   ├── Order.cs           # 订单实体
│   │   │   ├── PurchaseOrder.cs  # 采购订单实体
│   │   │   ├── AfterSale.cs      # 售后实体
│   │   │   └── Shop.cs           # 店铺实体
│   │   ├── Interfaces/           # 接口定义
│   │   │   ├── IRepository.cs   # 仓储接口
│   │   │   └── IService.cs      # 服务接口
│   │   ├── DomainEvents/         # 领域事件
│   │   └── ValueObjects/         # 值对象
│   │
│   ├── LionERP.Application/        # 应用服务层
│   │   ├── DTOs/                 # 数据传输对象
│   │   │   ├── ProductDto.cs
│   │   │   ├── OrderDto.cs
│   │   │   └── ...
│   │   ├── Interfaces/           # 服务接口
│   │   ├── Services/             # 应用服务实现
│   │   │   ├── ProductService.cs
│   │   │   ├── OrderService.cs
│   │   │   └── ...
│   │   └── Profiles/             # AutoMapper 配置
│   │
│   ├── LionERP.Infrastructure/    # 基础设施层
│   │   ├── Data/                 # 数据访问
│   │   │   ├── ApplicationDbContext.cs
│   │   │   └── Migrations/
│   │   ├── Repositories/         # 仓储实现
│   │   ├── ExternalServices/     # 外部服务集成
│   │   │   ├── PddApi/          # 拼多多 API
│   │   │   ├── Ali1688Api/      # 1688 API
│   │   │   └── AiService/       # AI 大模型服务
│   │   └── Services/             # 基础设施服务
│   │
│   └── LionERP.Api/              # Web API 层
│       ├── Controllers/           # 控制器
│       │   ├── ProductsController.cs
│       │   ├── OrdersController.cs
│       │   └── ...
│       ├── Middlewares/           # 中间件
│       ├── Filters/               # 过滤器
│       ├── appsettings.json       # 配置文件
│       └── Program.cs            # 入口文件
│
├── frontend/                      # 前端项目
│   ├── src/
│   │   ├── components/           # 组件
│   │   ├── pages/                # 页面
│   │   ├── services/             # API 服务
│   │   └── store/                # 状态管理
│   ├── public/
│   ├── package.json
│   └── README.md
│
├── tests/                         # 测试项目
│   ├── LionERP.Core.Tests/
│   ├── LionERP.Application.Tests/
│   └── LionERP.Api.Tests/
│
├── docs/                          # 文档
│   ├── 妙手ERP功能参考.md          # 妙手功能参考文档
│   ├── API文档.md
│   ├── 数据库设计.md
│   └── images/
│
├── .gitignore
├── LionERP.sln                    # 解决方案文件
└── README.md
```

---

## 开发计划

### 阶段一：项目初始化（当前阶段）✅

- [x] 创建项目目录结构
- [x] 初始化 .NET Core 解决方案和项目
- [x] 创建前端项目框架
- [x] 配置 Git 和 GitHub
- [x] 调研妙手功能并生成参考文档
- [ ] 设计数据库架构
- [ ] 创建实体类和 DbContext
- [ ] 配置依赖注入
- [ ] 创建第一个 API 接口

### 阶段二：基础功能开发（1-2个月）🚧

- [ ] **商品管理模块**
  - [ ] 实现 1688 API 集成
  - [ ] 商品信息采集
  - [ ] 商品信息编辑
  - [ ] 商品一键铺货到拼多多

- [ ] **订单管理模块**
  - [ ] 实现拼多多 API 集成
  - [ ] 订单自动同步
  - [ ] 订单自动审核
  - [ ] 订单状态跟踪

- [ ] **采购管理模块**
  - [ ] 订单自动匹配1688货源
  - [ ] 自动采购和下单
  - [ ] 采购订单跟踪

- [ ] **发货同步模块**
  - [ ] 1688发货信息自动同步
  - [ ] 拼多多发货信息回填
  - [ ] 物流信息实时更新

### 阶段三：进阶功能开发（2-3个月）🔮

- [ ] **售后管理模块**
  - [ ] 拼多多售后自动同步
  - [ ] 售后原因自动分析
  - [ ] 1688售后自动申请
  - [ ] 售后进度跟踪

- [ ] **货源管理模块**
  - [ ] 商品与1688货源关联
  - [ ] 货源一键替换
  - [ ] 多货源比价和选择

- [ ] **多店铺管理模块**
  - [ ] 多店铺授权
  - [ ] 多店铺订单统一处理
  - [ ] 多店铺商品统一管理

### 阶段四：智能功能开发（3-4个月）🔮

- [ ] **智能客服模块**
  - [ ] 接入拼多多客服系统
  - [ ] 接入大模型API（GPT/国内大模型）
  - [ ] 自动回复常见问题
  - [ ] 人工客服协同

- [ ] **数据分析模块**
  - [ ] 销售数据分析
  - [ ] 利润分析
  - [ ] 库存预警

- [ ] **营销工具模块**
  - [ ] 批量修改商品信息
  - [ ] AI生成营销文案
  - [ ] 水印添加

### 阶段五：测试和优化（1个月）🧪

- [ ] 编写单元测试
- [ ] 进行集成测试
- [ ] 性能优化
- [ ] 安全加固

### 阶段六：部署和运维（1个月）🚀

- [ ] 配置生产环境
- [ ] 部署应用
- [ ] 配置监控和日志
- [ ] 编写运维文档

---

## 人为节点介入清单

以下是开发过程中需要人工介入的关键节点：

### 第一阶段：环境搭建和授权申请 ⚠️

- [ ] **人为节点 1**: 申请 1688 开放平台账号和应用（需要企业资质）
  - 官网：https://open.1688.com/
  - 需要资料：企业营业执照、法人身份证等
  
- [ ] **人为节点 2**: 申请拼多多开放平台账号和应用（需要商家资质）
  - 官网：https://open.pinduoduo.com/
  - 需要资料：店铺账号、商家资质等

- [ ] **人为节点 3**: 配置数据库连接字符串
  - 安装 PostgreSQL 数据库
  - 创建数据库和用户
  - 配置连接字符串到 `appsettings.json`

- [ ] **人为节点 4**: 配置 API 密钥和回调地址
  - 配置 1688 API 的 AppKey、AppSecret
  - 配置拼多多 API 的 ClientId、ClientSecret
  - 配置回调地址

### 第二阶段：核心功能开发 ⚠️

- [ ] **人为节点 5**: 测试 1688 API 接口调用权限
  - 测试商品详情查询接口
  - 测试订单创建接口
  - 测试物流查询接口

- [ ] **人为节点 6**: 测试拼多多 API 接口调用权限
  - 测试商品上传接口
  - 测试订单查询接口
  - 测试订单发货接口

- [ ] **人为节点 7**: 验证商品铺货流程
  - 测试从1688采集商品
  - 测试商品编辑和审核
  - 测试一键铺货到拼多多

- [ ] **人为节点 8**: 验证订单同步和自动采购流程
  - 测试拼多多订单同步
  - 测试自动匹配1688货源
  - 测试自动采购和下单

### 第三阶段：测试和部署 ⚠️

- [ ] **人为节点 9**: 功能测试和问题修复
  - 执行完整的测试用例
  - 记录和修复bug

- [ ] **人为节点 10**: 性能测试和优化
  - 压力测试
  - 数据库优化
  - 代码优化

- [ ] **人为节点 11**: 生产环境部署配置
  - 配置服务器
  - 配置域名和SSL证书
  - 配置监控和日志

- [ ] **人为节点 12**: 正式上线和监控
  - 正式上线
  - 监控系统运行状态
  - 处理线上问题

---

## 安装和运行

### 后端运行 🖥️

#### 环境要求

- .NET Core 8.0 SDK
- PostgreSQL 14+
- Redis 7+（可选，用于缓存）

#### 步骤

1. **安装 .NET Core 8.0 SDK**
   - 下载地址：https://dotnet.microsoft.com/download/dotnet/8.0

2. **安装和配置 PostgreSQL**
   - 下载地址：https://www.postgresql.org/download/
   - 创建数据库：`LionERP`
   - 创建用户并授权

3. **配置数据库连接字符串**
   - 打开 `src/LionERP.Api/appsettings.json`
   - 修改 `ConnectionStrings` 节点

   ```json
   {
     "ConnectionStrings": {
       "DefaultConnection": "Host=localhost;Database=LionERP;Username=postgres;Password=your_password"
     }
   }
   ```

4. **运行数据库迁移**
   ```bash
   cd src/LionERP.Infrastructure
   dotnet ef migrations add InitialCreate
   dotnet ef database update
   ```

5. **启动 API 项目**
   ```bash
   cd src/LionERP.Api
   dotnet run
   ```

6. **访问 Swagger 文档**
   - 打开浏览器访问：https://localhost:5001/swagger

### 前端运行 🌐

#### 环境要求

- Node.js 16+
- npm 8+ 或 yarn 1.22+

#### 步骤

1. **安装 Node.js**
   - 下载地址：https://nodejs.org/

2. **安装依赖**
   ```bash
   cd frontend
   npm install
   # 或使用 yarn
   yarn install
   ```

3. **配置 API 地址**
   - 打开 `frontend/src/services/config.js`
   - 修改 `API_BASE_URL` 为后端API地址

   ```javascript
   export const API_BASE_URL = 'https://localhost:5001/api';
   ```

4. **启动开发服务器**
   ```bash
   npm run dev
   # 或使用 yarn
   yarn dev
   ```

5. **访问前端页面**
   - 打开浏览器访问：http://localhost:3000

---

## API 对接说明

### 1688 开放平台 🔗

- **官网**：https://open.1688.com/
- **主要 API**：
  - `alibaba.product.get` - 商品详情查询
  - `alibaba.product.search` - 商品搜索
  - `alibaba.trade.create` - 订单创建
  - `alibaba.trade.get` - 订单查询
  - `alibaba.logistics.get` - 物流查询

- **授权方式**：OAuth 2.0
- **API 文档**：https://open.1688.com/docs/

### 拼多多开放平台 🔗

- **官网**：https://open.pinduoduo.com/
- **主要 API**：
  - `pdd.goods.add` - 商品上传
  - `pdd.order.list.get` - 订单查询
  - `pdd.order.shipment.update` - 订单发货
  - `pdd.refund.list.get` - 售后查询
  - `pdd.refund.handle` - 售后处理

- **授权方式**：OAuth 2.0
- **API 文档**：https://open.pinduoduo.com/#/document

---

## 参考文档

本项目参考了以下资料和文档：

### 妙手ERP功能参考 📚

- **文档位置**：`docs/妙手ERP功能参考.md`
- **内容概要**：
  - 妙手ERP的核心功能模块
  - 商品管理、订单管理、采购管理、仓储管理、物流管理、财务管理、客服管理、营销管理、数据分析、系统管理
  - LionERP可参考的核心功能
  - 功能差异分析

- **数据来源**：
  - 妙手官网：https://91miaoshou.com/
  - 妙手帮助中心：https://erp.91miaoshou.com/help_center
  - 妙手百度百科：https://baike.baidu.com/item/妙手ERP/63235295

### 其他参考资料 📚

- **1688开放平台API文档**：https://open.1688.com/docs/
- **拼多多开放平台API文档**：https://open.pinduoduo.com/#/document
- **.NET Core 官方文档**：https://docs.microsoft.com/zh-cn/aspnet/core/
- **React 官方文档**：https://react.dev/
- **Ant Design Pro 官方文档**：https://pro.ant.design/

---

## 贡献指南

我们欢迎任何形式的贡献！

### 如何贡献

1. **Fork 本仓库**
2. **创建你的特性分支**
   ```bash
   git checkout -b feature/AmazingFeature
   ```
3. **提交你的更改**
   ```bash
   git commit -m 'Add some AmazingFeature'
   ```
4. **推送到分支**
   ```bash
   git push origin feature/AmazingFeature
   ```
5. **打开一个 Pull Request**

### 代码规范

- **C# 代码**：遵循 Microsoft C# 编码规范
- **TypeScript/JavaScript 代码**：遵循 Airbnb JavaScript 规范
- **提交信息**：使用 Conventional Commits 规范

### 报告 Bug

如果你发现了一个 bug，请：

1. 检查是否已有相关的 Issue
2. 如果没有，创建一个新的 Issue
3. 详细描述 bug 的复现步骤

---

## 许可证

本项目采用 **MIT 许可证** - 查看 [LICENSE](LICENSE) 文件了解详情。

MIT 许可证允许你：
- ✅ 自由使用、复制、修改、合并、发布、分发、再授权和销售本软件的副本
- ✅ 用于个人和商业用途
- ✅ 修改源代码
- ✅ 分发二进制文件

唯一的要求是：
- ⚠️ 保留版权声明和许可证声明

---

## 联系方式

如果你有任何问题或建议，请通过以下方式联系我们：

- **GitHub Issues**：[提交 Issue](https://github.com/MartinHuang126/LionERP/issues)
- **Email**：[请联系项目负责人]
- **微信群**：[请加入我们的微信群]

---

## 致谢

- 感谢 **妙手ERP** 提供的功能参考和设计灵感
- 感谢所有为这个项目做出贡献的开发者

---

## 更新日志

### v0.1.0 (2026-05-19)

- ✅ 初始化项目结构
- ✅ 创建 .NET Core 解决方案和项目
- ✅ 配置 Git 和 GitHub
- ✅ 调研妙手功能并生成参考文档
- ✅ 创建 README.md 项目文档

### 即将到来...

- 🚧 设计数据库架构
- 🚧 创建实体类和 DbContext
- 🚧 实现1688 API集成
- 🚧 实现拼多多API集成

---

**⭐ 如果这个项目对你有帮助，请给它一个星标！**

**🍴 欢迎 Fork 和贡献代码！**

**📢 分享给更多需要的人！**
