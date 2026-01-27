# Degener City - 黑客松项目

> 一个基于 Solana 区块链的 Web3 互动体验项目

## 项目简介

Degener City 是一个结合了 3D 可视化和区块链技术的创新项目，旨在为用户提供沉浸式的 Web3 交互体验。

## 技术栈

- **前端框架**: React 18
- **3D 渲染**: Three.js + React Three Fiber
- **区块链**: Solana Web3.js
- **钱包集成**: Solana Wallet Adapter
- **状态管理**: Zustand
- **构建工具**: Vite
- **样式**: Tailwind CSS
- **国际化**: i18next

## 核心功能

- 🎮 3D 交互场景
- 💰 Solana 钱包连接
- 🌐 多语言支持
- 📊 数据可视化
- 🎨 响应式设计

## 项目结构

```
degener-city-hackathon/
├── src/              # 源代码目录
│   ├── components/   # React 组件
│   ├── scenes/       # 3D 场景
│   ├── stores/       # 状态管理
│   ├── utils/        # 工具函数
│   └── locales/      # 国际化文件
├── public/           # 静态资源
└── docs/             # 文档
```

## 快速开始

### 环境要求

- Node.js >= 18
- pnpm >= 9.0.0

### 安装依赖

```bash
pnpm install
```

### 开发模式

```bash
pnpm dev
```

### 构建生产版本

```bash
pnpm build
```

## 特色亮点

1. **创新的 3D 交互体验**：使用 Three.js 打造身临其境的视觉效果
2. **无缝的 Web3 集成**：支持主流 Solana 钱包（Phantom、Solflare 等）
3. **性能优化**：利用 Vite 的快速构建和热更新能力
4. **用户友好**：多语言支持，降低使用门槛

## 路线图

- [x] 基础 3D 场景搭建
- [x] 钱包连接功能
- [x] 多语言支持
- [ ] 智能合约集成
- [ ] 社交功能
- [ ] 移动端适配

## 技术文档

详细的技术文档请参考 `docs/` 目录。

## 开发团队

本项目为黑客松参赛作品，致力于探索 Web3 和 3D 技术的结合可能性。

## 许可证

MIT License

---

**注意**: 本仓库为黑客松展示版本，包含项目架构和技术说明，不包含完整的生产代码。
