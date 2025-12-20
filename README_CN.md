# GitLab 项目说明 (中文版)

> 完整的详细分析文档请查看: [GITLAB_项目分析文档.md](./GITLAB_项目分析文档.md)

## 快速了解

GitLab 是一个完整的 DevOps 平台，提供从代码托管到生产部署的全流程工具链。

### 核心特性

- 🔧 **Git 仓库管理**: 精细化的访问控制，保护代码安全
- 👥 **代码审查**: 通过合并请求（Merge Request）增强协作
- 🚀 **CI/CD 流水线**: 自动化构建、测试和部署
- 📋 **项目管理**: Issue 跟踪、看板、Wiki 等
- 🌍 **全球使用**: 超过 10 万个组织使用

### 技术栈总览

| 组件 | 技术 | 用途 |
|------|------|------|
| **后端框架** | Ruby on Rails 7.2 | Web 应用核心 |
| **前端框架** | Vue.js 3 | 用户界面 |
| **数据库** | PostgreSQL 16.5+ | 数据存储 |
| **缓存/队列** | Redis 6.0+ | 缓存和任务队列 |
| **反向代理** | GitLab Workhorse (Go) | 请求处理和优化 |
| **Git 服务** | Gitaly (Go) | Git 操作 RPC 服务 |
| **SSH 服务** | GitLab Shell (Go) | SSH 连接处理 |
| **后台任务** | Sidekiq | 异步任务处理 |

### 目录结构速览

```
gitlabhq/
├── app/              # Rails 应用核心（MVC 架构）
│   ├── controllers/  # 控制器 - 处理请求
│   ├── models/       # 模型 - 数据和业务逻辑
│   ├── services/     # 服务 - 核心业务逻辑
│   ├── workers/      # 后台任务
│   └── ...
├── config/           # 配置文件
├── db/               # 数据库迁移和结构
├── lib/              # 库和扩展
│   ├── api/         # REST API
│   └── gitlab/      # GitLab 核心功能
├── spec/             # RSpec 测试
├── workhorse/        # Go 反向代理
├── doc/              # 完整文档
└── public/           # 静态资源
```

### 快速开始

#### 开发环境设置（推荐使用 GDK）

```bash
# 安装 GitLab Development Kit
git clone https://gitlab.com/gitlab-org/gitlab-development-kit.git
cd gitlab-development-kit
gem install gitlab-development-kit
gdk install

# 启动服务
gdk start

# 访问 http://localhost:3000
```

#### 运行测试

```bash
# Ruby 测试
bundle exec rspec

# JavaScript 测试  
yarn jest

# 代码检查
bundle exec rubocop
yarn lint:eslint
```

### 架构简图

```
┌─────────────┐
│   浏览器     │ ←→ HTTPS
└─────────────┘
       ↓
┌─────────────┐
│   NGINX     │ ←→ 负载均衡
└─────────────┘
       ↓
┌─────────────┐
│  Workhorse  │ ←→ 智能代理
└─────────────┘
       ↓
┌─────────────┐         ┌─────────────┐
│ Puma (Rails)│ ←→ ←→  │   Sidekiq   │
└─────────────┘         └─────────────┘
       ↓                       ↓
┌──────────────────────────────────┐
│  PostgreSQL  │  Redis  │  Gitaly │
└──────────────────────────────────┘
```

### 核心概念

#### 1. **服务对象模式 (Service Object)**
将复杂的业务逻辑封装在独立的服务类中，保持代码整洁和可测试性。

#### 2. **查找器模式 (Finder)**
封装数据查询逻辑，避免在控制器中编写复杂的查询。

#### 3. **策略模式 (Policy)**
使用 Pundit 管理授权逻辑，集中处理权限控制。

#### 4. **异步处理**
使用 Sidekiq 处理耗时任务，避免阻塞主请求。

### 版本信息

- **当前版本**: 18.8.0-pre
- **Ruby**: 3.3.10
- **Node.js**: 22.12.0
- **Rails**: 7.2.3

### 参与贡献

1. Fork 项目仓库
2. 创建功能分支
3. 编写代码和测试
4. 提交 Merge Request
5. 代码审查
6. 合并到主分支

### 许可证

- **社区版 (CE)**: MIT 许可证
- **企业版 (EE)**: 专有许可证（源码可见，接受贡献）

### 资源链接

- 📖 [完整项目分析文档](./GITLAB_项目分析文档.md)
- 🌐 [官方网站](https://about.gitlab.com/)
- 📚 [官方文档](https://docs.gitlab.com/)
- 💻 [开发文档](https://docs.gitlab.com/ee/development/)
- 🔧 [开发工具包 (GDK)](https://gitlab.com/gitlab-org/gitlab-development-kit)
- 🐛 [问题跟踪](https://gitlab.com/gitlab-org/gitlab/issues)

---

## 详细内容导航

完整的 [GITLAB_项目分析文档.md](./GITLAB_项目分析文档.md) 包含以下章节：

1. **项目概述** - 基本信息和版本
2. **目录结构详解** - 完整的目录说明和设计理念
3. **架构设计** - 系统架构、组件交互、数据流
4. **核心技术原理** - Git 管理、CI/CD、权限系统等
5. **背景知识** - 项目历史、开发哲学、技术选型
6. **如何使用** - 开发环境、代码规范、测试、部署
7. **性能优化** - 数据库、缓存、异步处理
8. **安全机制** - 认证、授权、安全扫描
9. **监控和可观测性** - 指标、日志、追踪
10. **扩展性设计** - 水平扩展、高可用架构

---

*如有任何问题或建议，欢迎提出 Issue 或 Merge Request！*
