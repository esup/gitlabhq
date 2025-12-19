# GitLab 项目目录结构详解

本文档详细说明 GitLab 项目的目录结构，帮助开发者快速了解代码组织方式。

## 完整目录树

```
gitlabhq/
│
├── 📁 app/                          # Rails 应用程序主目录
│   ├── 📁 assets/                   # 前端资源文件
│   │   ├── 📁 javascripts/          # JavaScript/Vue.js 源代码
│   │   │   ├── 📁 entrypoints/      # Webpack 入口点
│   │   │   ├── 📁 admin/            # 管理后台功能
│   │   │   ├── 📁 boards/           # 看板功能
│   │   │   ├── 📁 ci/               # CI/CD 相关前端代码
│   │   │   ├── 📁 issues/           # 问题跟踪前端
│   │   │   ├── 📁 merge_requests/   # 合并请求前端
│   │   │   ├── 📁 pipelines/        # CI Pipeline 前端
│   │   │   ├── 📁 vue_shared/       # Vue 共享组件
│   │   │   ├── 📁 graphql_shared/   # GraphQL 查询和片段
│   │   │   ├── 📁 lib/              # 工具函数和辅助类
│   │   │   ├── 📁 api/              # API 客户端封装
│   │   │   └── ...                  # 其他功能模块 (190+ 目录)
│   │   ├── 📁 stylesheets/          # SCSS/CSS 样式文件
│   │   │   ├── 📁 framework/        # 基础框架样式
│   │   │   ├── 📁 pages/            # 页面特定样式
│   │   │   ├── 📁 components/       # 组件样式
│   │   │   └── 📁 vendors/          # 第三方库样式
│   │   └── 📁 images/               # 图片资源
│   │       ├── 📁 logos/            # Logo 图片
│   │       ├── 📁 emoji/            # Emoji 图标
│   │       └── 📁 auth_buttons/     # 认证按钮图标
│   │
│   ├── 📁 controllers/              # Rails 控制器
│   │   ├── 📁 admin/                # 管理员控制器
│   │   ├── 📁 projects/             # 项目相关控制器
│   │   ├── 📁 groups/               # 群组相关控制器
│   │   └── concerns/                # 控制器 Concern
│   │
│   ├── 📁 models/                   # ActiveRecord 模型
│   │   ├── 📁 ci/                   # CI/CD 模型
│   │   ├── 📁 concerns/             # 模型 Concern
│   │   ├── 📁 integrations/         # 第三方集成
│   │   ├── project.rb               # 项目模型
│   │   ├── user.rb                  # 用户模型
│   │   ├── issue.rb                 # 问题模型
│   │   ├── merge_request.rb         # 合并请求模型
│   │   └── ...                      # 其他模型文件
│   │
│   ├── 📁 services/                 # 业务逻辑服务对象
│   │   ├── 📁 issues/               # 问题相关服务
│   │   ├── 📁 merge_requests/       # MR 相关服务
│   │   ├── 📁 ci/                   # CI/CD 服务
│   │   ├── 📁 projects/             # 项目服务
│   │   ├── 📁 users/                # 用户服务
│   │   └── base_service.rb          # 服务基类
│   │
│   ├── 📁 workers/                  # Sidekiq 后台任务
│   │   ├── 📁 ci/                   # CI 相关 Worker
│   │   ├── 📁 repository/           # 仓库操作 Worker
│   │   ├── 📁 post_receive/         # Git push 后处理
│   │   └── application_worker.rb    # Worker 基类
│   │
│   ├── 📁 graphql/                  # GraphQL Schema 定义
│   │   ├── 📁 types/                # GraphQL 类型
│   │   ├── 📁 mutations/            # GraphQL 变更
│   │   ├── 📁 resolvers/            # GraphQL 解析器
│   │   └── gitlab_schema.rb         # Schema 入口
│   │
│   ├── 📁 policies/                 # 权限策略 (Pundit)
│   │   ├── project_policy.rb        # 项目权限
│   │   ├── issue_policy.rb          # 问题权限
│   │   └── base_policy.rb           # 策略基类
│   │
│   ├── 📁 presenters/               # 展示层对象
│   ├── 📁 serializers/              # API 序列化器
│   ├── 📁 finders/                  # 查询对象
│   ├── 📁 validators/               # 自定义验证器
│   ├── 📁 uploaders/                # 文件上传处理
│   ├── 📁 mailers/                  # 邮件发送
│   ├── 📁 helpers/                  # 视图辅助方法
│   ├── 📁 views/                    # Rails 视图模板 (HAML/ERB)
│   ├── 📁 channels/                 # Action Cable WebSocket 通道
│   ├── 📁 components/               # ViewComponent 组件
│   ├── 📁 events/                   # 事件对象
│   ├── 📁 experiments/              # A/B 测试实验
│   └── 📁 facades/                  # 外观模式封装
│
├── 📁 config/                       # 配置文件目录
│   ├── application.rb               # Rails 应用配置
│   ├── environment.rb               # 环境初始化
│   ├── routes.rb                    # 路由配置
│   ├── 📁 environments/             # 环境配置
│   │   ├── development.rb           # 开发环境
│   │   ├── test.rb                  # 测试环境
│   │   └── production.rb            # 生产环境
│   ├── 📁 initializers/             # 初始化器 (100+ 文件)
│   │   ├── 1_settings.rb            # 设置加载
│   │   ├── sidekiq.rb               # Sidekiq 配置
│   │   ├── devise.rb                # 认证配置
│   │   └── ...
│   ├── 📁 locales/                  # 国际化翻译文件
│   ├── 📁 routes/                   # 路由分组
│   ├── 📁 feature_flags/            # 特性标志定义
│   ├── 📁 metrics/                  # Prometheus 指标配置
│   ├── webpack.config.js            # Webpack 配置
│   ├── vite.config.js               # Vite 配置
│   ├── babel.config.js              # Babel 配置
│   ├── tailwind.config.js           # TailwindCSS 配置
│   ├── gitlab.yml.example           # GitLab 主配置模板
│   ├── database.yml.postgresql      # 数据库配置模板
│   ├── redis.yml.example            # Redis 配置模板
│   ├── sidekiq.yml.example          # Sidekiq 配置模板
│   └── puma.rb.example              # Puma 服务器配置
│
├── 📁 db/                           # 数据库相关
│   ├── 📁 migrate/                  # 数据库迁移文件 (3000+ 文件)
│   ├── 📁 post_migrate/             # 后置迁移 (零停机部署)
│   ├── 📁 fixtures/                 # 固定数据/种子数据
│   ├── 📁 schema_migrations/        # Schema 版本管理
│   ├── 📁 docs/                     # 数据库文档
│   ├── 📁 click_house/              # ClickHouse 相关
│   ├── structure.sql                # PostgreSQL 数据库结构
│   ├── ci_structure.sql             # CI 数据库结构
│   └── seeds.rb                     # 数据库种子数据
│
├── 📁 lib/                          # 共享库和工具
│   ├── 📁 api/                      # Grape REST API 定义
│   │   ├── api.rb                   # API 入口
│   │   ├── 📁 entities/             # API 实体
│   │   ├── projects.rb              # 项目 API
│   │   ├── issues.rb                # 问题 API
│   │   └── ...                      # 其他 API 端点
│   ├── 📁 gitlab/                   # GitLab 核心库
│   │   ├── 📁 auth/                 # 认证授权
│   │   ├── 📁 ci/                   # CI/CD 核心逻辑
│   │   ├── 📁 git/                  # Git 操作封装
│   │   ├── 📁 database/             # 数据库工具
│   │   ├── 📁 import_export/        # 项目导入导出
│   │   ├── 📁 graphql/              # GraphQL 工具
│   │   ├── 📁 middleware/           # Rack 中间件
│   │   └── ...
│   ├── 📁 backup/                   # 备份和恢复
│   ├── 📁 banzai/                   # Markdown 处理管道
│   ├── 📁 click_house/              # ClickHouse 集成
│   ├── 📁 bulk_imports/             # 批量导入
│   ├── 📁 atlassian/                # Atlassian (Jira) 集成
│   ├── 📁 bitbucket/                # Bitbucket 集成
│   ├── 📁 error_tracking/           # 错误追踪
│   ├── 📁 tasks/                    # Rake 任务
│   └── feature.rb                   # 特性标志管理
│
├── 📁 gems/                         # Monorepo 内部 Gems
│   ├── 📁 gitlab-rspec/             # RSpec 测试扩展
│   ├── 📁 gitlab-database-load_balancing/  # 数据库负载均衡
│   ├── 📁 gitlab-schema-validation/ # Schema 验证工具
│   ├── 📁 gitlab-backup-cli/        # 备份命令行工具
│   ├── 📁 activerecord-gitlab/      # ActiveRecord 扩展
│   ├── 📁 gitlab-safe_request_store/# 请求存储
│   ├── 📁 bundler-checksum/         # Bundler 校验和
│   └── ...                          # 其他内部 Gems (20+)
│
├── 📁 workhorse/                    # Go 语言反向代理服务
│   ├── 📁 cmd/                      # 命令行入口
│   ├── 📁 internal/                 # 内部实现
│   │   ├── 📁 git/                  # Git HTTP 协议处理
│   │   ├── 📁 upload/               # 文件上传处理
│   │   ├── 📁 download/             # 文件下载处理
│   │   ├── 📁 proxy/                # 代理逻辑
│   │   ├── 📁 senddata/             # 数据发送
│   │   └── 📁 api/                  # API 通信
│   ├── go.mod                       # Go 模块定义
│   ├── go.sum                       # Go 依赖校验
│   ├── Makefile                     # 构建脚本
│   └── README.md                    # Workhorse 文档
│
├── 📁 spec/                         # RSpec 测试目录
│   ├── 📁 features/                 # 功能测试 (Capybara)
│   ├── 📁 requests/                 # 请求测试 (API)
│   ├── 📁 models/                   # 模型单元测试
│   ├── 📁 services/                 # 服务单元测试
│   ├── 📁 controllers/              # 控制器测试
│   ├── 📁 graphql/                  # GraphQL 测试
│   ├── 📁 workers/                  # Worker 测试
│   ├── 📁 policies/                 # 策略测试
│   ├── 📁 frontend/                 # 前端 Jest 测试
│   ├── 📁 fixtures/                 # 测试夹具
│   ├── 📁 factories/                # FactoryBot 工厂
│   ├── 📁 support/                  # 测试辅助工具
│   ├── 📁 contracts/                # 契约测试
│   └── spec_helper.rb               # RSpec 配置
│
├── 📁 qa/                           # 质量保证测试套件
│   ├── 📁 qa/                       # QA 测试代码
│   │   ├── 📁 specs/                # QA 测试用例
│   │   ├── 📁 page/                 # 页面对象模式
│   │   ├── 📁 resource/             # 测试资源
│   │   └── 📁 scenario/             # 测试场景
│   └── Gemfile                      # QA 专用依赖
│
├── 📁 doc/                          # 项目文档
│   ├── 📁 api/                      # API 文档
│   ├── 📁 development/              # 开发者文档
│   ├── 📁 user/                     # 用户文档
│   ├── 📁 administration/           # 管理员文档
│   ├── 📁 ci/                       # CI/CD 文档
│   ├── 📁 install/                  # 安装文档
│   ├── 📁 security/                 # 安全文档
│   └── README.md                    # 文档索引
│
├── 📁 public/                       # 静态资源目录
│   ├── 📁 assets/                   # 编译后的前端资源
│   ├── 📁 uploads/                  # 用户上传文件
│   ├── favicon.ico                  # 网站图标
│   └── robots.txt                   # 搜索引擎爬虫配置
│
├── 📁 vendor/                       # 第三方依赖
│   ├── 📁 assets/                   # 第三方前端资源
│   └── 📁 gems/                     # Vendored Gems
│
├── 📁 scripts/                      # 实用脚本
│   ├── 📁 frontend/                 # 前端开发脚本
│   ├── 📁 db/                       # 数据库脚本
│   ├── 📁 ci/                       # CI 辅助脚本
│   └── 📁 lint/                     # Lint 脚本
│
├── 📁 tooling/                      # 开发工具
│   ├── 📁 danger/                   # Danger 插件
│   ├── 📁 rspec_flaky/              # Flaky 测试检测
│   ├── 📁 bin/                      # 工具可执行文件
│   └── 📁 lib/                      # 工具库
│
├── 📁 danger/                       # Danger 自动化代码审查
│   ├── 📁 plugins/                  # Danger 插件
│   ├── database_dictionary.rb       # 数据库字典检查
│   ├── documentation.rb             # 文档检查
│   ├── specs.rb                     # 测试检查
│   └── ...                          # 其他检查规则 (50+)
│
├── 📁 storybook/                    # Storybook 组件文档
│   ├── 📁 config/                   # Storybook 配置
│   ├── package.json                 # 独立的 package.json
│   └── yarn.lock                    # 独立的依赖锁定
│
├── 📁 .gitlab/                      # GitLab 特定配置
│   ├── 📁 ci/                       # CI 配置模块
│   ├── 📁 issue_templates/          # Issue 模板
│   ├── 📁 merge_request_templates/  # MR 模板
│   └── CODEOWNERS                   # 代码所有者
│
├── 📁 locale/                       # 国际化翻译文件 (80+ 语言)
│   ├── 📁 en/                       # 英语
│   ├── 📁 zh_CN/                    # 简体中文
│   ├── 📁 zh_TW/                    # 繁体中文
│   └── ...
│
├── 📁 changelogs/                   # 变更日志
│   ├── 📁 unreleased/               # 未发布的更改
│   └── archive.md                   # 历史变更
│
├── 📁 fixtures/                     # 测试固件
│   ├── 📁 emojis/                   # Emoji 数据
│   └── 📁 lib/                      # 库固件
│
├── 📁 data/                         # 静态数据文件
│   ├── 📁 whats_new/                # 新功能公告
│   └── 📁 deprecations/             # 弃用通知
│
├── 📁 bin/                          # 可执行脚本
│   ├── rails                        # Rails 命令
│   ├── rake                         # Rake 命令
│   ├── bundle                       # Bundler 命令
│   └── ...
│
├── 📁 tmp/                          # 临时文件目录
│   ├── 📁 cache/                    # 缓存
│   ├── 📁 pids/                     # 进程 PID
│   └── 📁 sockets/                  # Unix Socket
│
├── 📁 log/                          # 日志文件目录
│   ├── development.log              # 开发日志
│   ├── test.log                     # 测试日志
│   └── production.log               # 生产日志
│
├── 📁 .rubocop_todo/                # RuboCop 待办事项 (按目录分)
├── 📁 .rubocop/                     # RuboCop 自定义检查
├── 📁 haml_lint/                    # HAML Lint 自定义检查
│
├── 📄 package.json                  # Node.js 依赖配置
├── 📄 yarn.lock                     # Yarn 依赖锁定文件
├── 📄 Gemfile                       # Ruby 依赖配置
├── 📄 Gemfile.lock                  # Bundler 依赖锁定文件
├── 📄 Gemfile.next                  # 下一版本 Ruby 依赖
├── 📄 config.ru                     # Rack 应用配置
├── 📄 Rakefile                      # Rake 任务定义
├── 📄 .gitlab-ci.yml                # GitLab CI/CD 主配置
├── 📄 tests.yml                     # 测试配置
├── 📄 lefthook.yml                  # Git Hooks 配置
├── 📄 .ruby-version                 # Ruby 版本 (3.2.5)
├── 📄 .nvmrc                        # Node 版本 (22.12.0)
├── 📄 VERSION                       # GitLab 版本号
├── 📄 INSTALLATION_TYPE             # 安装类型标识
├── 📄 README.md                     # 项目自述文件
├── 📄 CONTRIBUTING.md               # 贡献指南
├── 📄 CHANGELOG.md                  # 变更日志
├── 📄 LICENSE                       # MIT 许可证
│
└── 📄 各种配置文件                   # Linter、Formatter 等配置
    ├── .rubocop.yml                 # RuboCop 配置
    ├── .eslintrc.yml                # ESLint 配置
    ├── .prettierrc                  # Prettier 配置
    ├── .stylelintrc                 # Stylelint 配置
    ├── .haml-lint.yml               # HAML Lint 配置
    ├── babel.config.js              # Babel 配置
    ├── jest.config.js               # Jest 配置
    ├── postcss.config.js            # PostCSS 配置
    ├── .editorconfig                # EditorConfig
    └── .gitignore                   # Git 忽略文件
```

## 目录说明

### 🔴 核心应用目录

#### `app/`
Rails 应用的核心目录，包含所有业务逻辑、视图、资源等。

- **assets/**: 前端资源，包括 JavaScript、CSS 和图片
- **controllers/**: 处理 HTTP 请求的控制器
- **models/**: 数据模型，对应数据库表
- **services/**: 业务逻辑服务对象（GitLab 的核心架构模式）
- **workers/**: 后台异步任务
- **graphql/**: GraphQL API 定义

#### `lib/`
共享库和辅助功能，不依赖于 Rails 应用。

- **api/**: Grape REST API 定义
- **gitlab/**: GitLab 核心功能库
- **tasks/**: Rake 任务

#### `config/`
应用配置文件，包括数据库、路由、环境等。

### 🟢 测试目录

#### `spec/`
RSpec 测试套件，覆盖后端和前端。

#### `qa/`
端到端质量保证测试，模拟真实用户操作。

### 🟡 数据库目录

#### `db/`
数据库迁移、结构定义和种子数据。

- **migrate/**: 数据库迁移文件（按时间戳排序）
- **post_migrate/**: 后置迁移（支持零停机部署）

### 🔵 特殊组件

#### `workhorse/`
Go 语言编写的高性能反向代理服务器。

#### `gems/`
Monorepo 内部的 Ruby gems，作为独立模块管理。

#### `storybook/`
前端组件的可视化文档和开发环境。

### 🟣 文档和工具

#### `doc/`
完整的项目文档，包括 API、开发指南、用户手册。

#### `scripts/`
各种实用脚本，用于开发、部署、维护。

#### `tooling/`
开发工具和辅助程序。

#### `danger/`
自动化代码审查规则。

### ⚪ 配置和元数据

- **根目录配置文件**: 各种工具的配置（linter、formatter 等）
- **.gitlab/**: GitLab CI/CD 和项目管理配置
- **locale/**: 多语言翻译文件

## 目录访问频率

### 🔥 高频访问（日常开发）

```
app/assets/javascripts/    # 前端功能开发
app/models/                 # 数据模型修改
app/services/               # 业务逻辑开发
spec/                       # 编写测试
config/routes.rb            # 路由配置
```

### 🔸 中频访问（功能开发）

```
app/controllers/            # 控制器开发
app/workers/                # 后台任务
app/graphql/                # GraphQL API
lib/api/                    # REST API
db/migrate/                 # 数据库迁移
```

### 🔹 低频访问（特定任务）

```
config/initializers/        # 初始化配置
lib/gitlab/                 # 核心库修改
workhorse/                  # Go 服务开发
doc/                        # 文档更新
```

## 文件数量统计

```
总目录数:    ~2,000+
总文件数:    ~50,000+
代码文件:    ~30,000+
测试文件:    ~15,000+
配置文件:    ~1,000+
```

## 代码行数估算

```
Ruby 代码:        ~1,500,000 行
JavaScript/Vue:   ~800,000 行
Go 代码:          ~100,000 行
测试代码:         ~1,000,000 行
配置文件:         ~50,000 行
文档:             ~200,000 行
```

## 关键路径示例

### 创建一个新的 Issue

1. **前端**: `app/assets/javascripts/issues/new/` - Vue 组件
2. **路由**: `config/routes.rb` - 路由定义
3. **控制器**: `app/controllers/projects/issues_controller.rb` - 处理请求
4. **服务**: `app/services/issues/create_service.rb` - 业务逻辑
5. **模型**: `app/models/issue.rb` - 数据模型
6. **策略**: `app/policies/issue_policy.rb` - 权限检查
7. **Worker**: `app/workers/new_issue_worker.rb` - 异步通知
8. **视图**: `app/views/projects/issues/new.html.haml` - 页面模板

### CI Pipeline 执行

1. **配置解析**: `lib/gitlab/ci/yaml_processor.rb`
2. **Pipeline 创建**: `app/services/ci/create_pipeline_service.rb`
3. **Job 调度**: `app/workers/ci/pipeline_creation_worker.rb`
4. **Runner 通信**: `lib/api/ci/runner.rb`
5. **状态更新**: `app/services/ci/update_build_state_service.rb`
6. **前端展示**: `app/assets/javascripts/ci/pipeline_details/`

### GraphQL 查询

1. **Schema 定义**: `app/graphql/gitlab_schema.rb`
2. **类型定义**: `app/graphql/types/project_type.rb`
3. **解析器**: `app/graphql/resolvers/projects_resolver.rb`
4. **查询执行**: `lib/gitlab/graphql/query_analyzers/`
5. **前端查询**: `app/assets/javascripts/graphql_shared/queries/`

## 开发流程中的目录使用

### 1. 添加新功能

```
1. 创建 Issue 和设计文档 (doc/)
2. 编写特性标志 (config/feature_flags/)
3. 实现后端逻辑 (app/services/, app/models/)
4. 实现前端界面 (app/assets/javascripts/)
5. 编写测试 (spec/)
6. 更新文档 (doc/)
7. 添加变更日志 (changelogs/unreleased/)
```

### 2. 修复 Bug

```
1. 重现问题 (spec/)
2. 定位代码 (app/, lib/)
3. 修复代码
4. 添加测试覆盖
5. 验证修复
```

### 3. 数据库变更

```
1. 创建迁移 (db/migrate/)
2. 更新模型 (app/models/)
3. 添加后置迁移 (db/post_migrate/) - 如需要
4. 更新文档 (db/docs/)
5. 运行测试
```

### 4. API 开发

```
1. REST API: lib/api/
2. GraphQL API: app/graphql/
3. API 测试: spec/requests/, spec/graphql/
4. API 文档: doc/api/
```

## 目录命名约定

### Rails 约定

- 复数形式: `controllers/`, `models/`, `workers/`
- 单数形式: `app/`, `lib/`, `config/`
- 下划线: `merge_requests/`, `ci_cd/`

### JavaScript 约定

- 小驼峰: `camelCase.js`
- 连字符: `kebab-case.vue`
- 下划线: `snake_case/` (目录)

### 特殊后缀

- `_controller.rb`: 控制器
- `_service.rb`: 服务对象
- `_worker.rb`: 后台任务
- `_policy.rb`: 权限策略
- `_spec.rb`: 测试文件
- `.vue`: Vue 组件

## 总结

GitLab 的目录结构遵循 Rails 约定，同时引入了服务对象、查找器、策略等设计模式来组织代码。前端采用模块化的方式，每个功能有独立的目录。Monorepo 内部的 gems 提供可复用的功能模块。整体结构清晰，易于维护和扩展。

关键特点：
- 📦 Monorepo 架构，所有代码在一个仓库
- 🎯 服务对象模式，业务逻辑清晰分离
- 🔌 模块化前端，功能独立可复用
- 🧪 完整的测试覆盖，测试代码与源码对应
- 📚 详尽的文档，与代码同步维护
- 🔧 丰富的工具，自动化开发流程
