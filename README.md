# NavLink - 多应用集成平台

> 一个现代化、模块化的私有应用集成平台，提供导航站、订阅管理和Docker管理等多个实用应用。

![Version](https://img.shields.io/badge/version-2.0.0-blue.svg)
![License](https://img.shields.io/badge/license-MIT-green.svg)

## ✨ 核心特性

- **🎨 现代化设计**：基于 React 19 + Tailwind CSS，极致美观的用户界面
- **🔐 安全认证**：JWT 身份认证，支持多用户管理
- **💾 数据持久化**：SQLite 数据库，轻量高效
- **📱 响应式布局**：完美适配桌面端和移动端
- **🐳 容器化部署**：Docker 一键部署，开箱即用
- **🔌 可扩展架构**：模块化应用设计，易于扩展新功能

## 📦 集成应用

### 1️⃣ NavLink - 智能导航站

**功能特点：**
- 📂 分类管理：多级分类，拖拽排序
- 🔍 智能搜索：快速查找收藏的网站
- ⭐ 热门推荐：高频访问推荐
- 🎨 个性化配置：自定义主题、图标、布局
- 🔗 链接健康检查：自动检测失效链接
- 🌐 Chrome 扩展：一键保存当前网页

**适用场景：** 个人书签管理、团队资源导航、企业内网入口

### 2️⃣ Sub - 订阅管理器

**功能特点：**
- 📅 订阅追踪：管理各类订阅服务（视频、音乐、软件等）
- 🔔 到期提醒：支持邮件/系统通知
- 💰 费用统计：订阅成本分析
- 🔄 自动续费：续费状态跟踪
- 📊 数据可视化：订阅趋势分析
- 🌙 农历支持：支持农历日期提醒

**适用场景：** 个人订阅管理、家庭账单跟踪、企业订阅审计

### 3️⃣ Docker - 容器管理平台

**功能特点：**
- 🖥️ 多服务器管理：统一管理多台 Docker 主机
- 📦 容器管理：创建、启动、停止、删除容器
- 🎯 镜像管理：拉取、删除镜像
- 🌐 网络管理：查看和管理 Docker 网络
- 💾 卷管理：数据卷查看和删除
- 📊 实时监控：容器状态、资源使用情况
- 🔐 SSH 认证：支持密码和私钥认证
- 📝 操作审计：完整的操作日志记录

**适用场景：** DevOps 运维、容器化应用管理、服务器监控

## 🚀 快速开始

### 方式一：Docker 部署（推荐）

```bash
# 克隆项目
git clone https://github.com/txwebroot/NavLink.git
cd NavLink

# 启动服务
docker-compose up -d

# 访问应用
# 地址: http://localhost:8088
# 默认密码: admin
```

### 方式二：本地开发

**环境要求：** Node.js 20+

```bash
# 安装依赖
npm install

# 启动开发服务器（前端 + 后端）
npm run dev:all

# 访问地址
# 前端: http://localhost:3000
# 后端: http://localhost:3001
```

## 📖 使用指南

### 首次登录

1. 访问 `http://localhost:8088`
2. 点击右上角用户图标
3. 使用默认密码 `admin` 登录
4. 建议立即修改密码

### 应用切换

点击顶部导航栏的应用图标即可切换不同应用：
- 🏠 NavLink - 导航站
- 📋 Sub - 订阅管理
- 🐳 Docker - 容器管理

### 后台管理

登录后，再次点击右上角用户图标即可打开管理面板。

## 📁 项目结构

```
NavLink/
├── src/                      # 前端源码
│   ├── apps/                 # 应用模块
│   │   ├── navlink/          # 导航站应用
│   │   ├── sub/              # 订阅管理应用
│   │   └── docker/           # Docker管理应用
│   └── shared/               # 共享组件和工具
├── server/                   # 后端源码
│   ├── database/             # 数据库层 (SQLite)
│   │   ├── dao/              # 数据访问对象
│   │   └── schema.sql        # 数据库架构
│   ├── routes/               # API 路由
│   │   ├── app.js            # 应用配置路由
│   │   ├── docker.js         # Docker API
│   │   └── subscription.js   # 订阅管理 API
│   └── services/             # 业务逻辑
│       └── dockerService.js  # Docker 服务
├── data/                     # 数据存储目录
│   ├── navlink.db            # SQLite 数据库
│   └── uploads/              # 上传文件
├── chrome-extension/         # Chrome 扩展
├── docker-compose.yml        # Docker 编排文件
└── README.md                 # 项目文档
```

## ⚙️ 配置说明

### 环境变量

在 `docker-compose.yml` 或 `.env` 文件中配置：

| 变量名 | 默认值 | 说明 |
|--------|--------|------|
| `PORT` | `80` | 服务端口（容器内） |
| `JWT_SECRET` | `your-secret-key` | JWT 签名密钥 |
| `ADMIN_PASSWORD` | `admin` | 管理员初始密码 |
| `DB_PATH` | `./data/navlink.db` | 数据库路径 |

### Docker 管理配置

支持多种 Docker 连接方式：
- **本地 Socket**：`/var/run/docker.sock`
- **TCP**：`tcp://host:2375`
- **TLS**：`tcp://host:2376`（需要证书）
- **SSH**：支持密码和私钥认证

### 数据备份

重要数据位于 `data/` 目录：
- `data/navlink.db` - 主数据库
- `data/uploads/` - 上传文件

**备份命令：**
```bash
# 备份数据
tar -czf navlink-backup-$(date +%Y%m%d).tar.gz data/

# 恢复数据
tar -xzf navlink-backup-YYYYMMDD.tar.gz
```

## 🧩 Chrome 扩展

### 安装步骤

1. 打开 Chrome，访问 `chrome://extensions/`
2. 启用"开发者模式"
3. 点击"加载已解压的扩展程序"
4. 选择 `chrome-extension` 目录
5. 配置服务器地址和密码

### 使用方法

- 点击扩展图标快速保存当前网页
- 支持自定义分类和标签
- 自动抓取网页图标

## 🛠️ 技术栈

### 前端
- React 19
- TypeScript
- Vite
- Tailwind CSS
- Iconify

### 后端
- Node.js
- Express
- SQLite3
- Dockerode
- SSH2

### 运维
- Docker
- Docker Compose

## 📊 性能优化

- ✅ 后端缓存机制（10s TTL）
- ✅ SSH 连接复用
- ✅ 请求超时优化
- ✅ 数据库索引优化
- ✅ 前端代码分割

## 🔒 安全特性

- JWT 认证机制
- 密码加密存储
- API 请求验证
- CORS 配置
- SQL 注入防护

## 🤝 贡献指南

欢迎贡献代码！请遵循以下步骤：

1. Fork 本仓库
2. 创建特性分支 (`git checkout -b feature/AmazingFeature`)
3. 提交更改 (`git commit -m 'Add some AmazingFeature'`)
4. 推送到分支 (`git push origin feature/AmazingFeature`)
5. 提交 Pull Request

## 📝 更新日志

### v2.0.0 (2024-12)
- ✨ 新增 Docker 管理应用
- 🔧 SSH 私钥认证支持
- ⚡ 性能优化和缓存机制
- 🐛 修复多个已知问题

### v1.1.0 (2024-11)
- ✨ 新增订阅管理应用
- 🔄 迁移至 SQLite 数据库
- 🎨 UI/UX 优化

### v1.0.0 (2024-10)
- 🎉 初始版本发布
- 📂 导航站核心功能
- 🔐 用户认证系统

## 📄 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

## 📮 联系方式

- GitHub: [@txwebroot](https://github.com/txwebroot)
- 项目地址: [https://github.com/txwebroot/NavLink](https://github.com/txwebroot/NavLink)

---

⭐ 如果这个项目对你有帮助，请给个 Star！
