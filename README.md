# Degener City - 黑客松项目

> 一个基于 Solana 区块链的 Web3 互动体验项目

🌐 **游戏官网**: [https://degener.city/](https://degener.city/)

## 项目简介

Degener City 是一个结合了 3D 可视化和区块链技术的创新项目，旨在为用户提供沉浸式的 Web3 交互体验。通过 Solana 区块链技术，玩家可以真正拥有虚拟资产，参与去中心化治理，在虚拟城市中自由创造和交易。

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

- 🎮 **3D 交互场景** - 基于 Three.js 的沉浸式虚拟城市
- 💰 **Solana 钱包连接** - 支持 Phantom、Solflare 等主流钱包
- 🎨 **NFT 系统** - 角色 NFT、土地 NFT、道具 NFT
- 🏪 **交易市场** - 去中心化的 NFT 交易平台
- 💎 **质押挖矿** - NFT 质押获取代币奖励
- 🗳️ **DAO 治理** - 社区提案和投票系统
- 🌐 **多语言支持** - 简体中文、English
- 📊 **数据可视化** - 链上数据实时展示
- 🎨 **响应式设计** - 支持桌面端和移动端

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

1. **创新的 3D 交互体验**
   - 使用 Three.js 打造身临其境的视觉效果
   - 流畅的 60 FPS 渲染性能
   - 优化的资源加载和场景管理

2. **完整的 Web3 经济系统**
   - NFT 资产真实所有权
   - 去中心化交易市场
   - 质押挖矿和收益机制
   - DGC 代币经济模型

3. **无缝的区块链集成**
   - 低延迟交易（Solana 400ms 区块时间）
   - 低成本交互（平均 $0.00025 手续费）
   - 支持主流钱包（Phantom、Solflare 等）

4. **社区驱动的治理**
   - DAO 提案和投票系统
   - 社区国库管理
   - 透明的链上治理记录

5. **性能优化**
   - Vite 快速构建和热更新
   - 代码分割和懒加载
   - Three.js 实例复用和 LOD

6. **用户友好**
   - 多语言支持，降低使用门槛
   - 直观的 UI/UX 设计
   - 新手引导系统

## 区块链架构

### 智能合约系统

- **Character NFT** - 角色 NFT 合约（属性、等级、升级）
- **Land NFT** - 土地 NFT 合约（坐标、开发、建筑）
- **Marketplace** - 交易市场合约（挂单、购买、拍卖）
- **Staking** - 质押合约（NFT 质押、奖励分发）
- **Governance** - 治理合约（提案、投票、执行）

### DGC Token

- **总供应量**: 1,000,000,000 DGC
- **代币用途**: 游戏内交易、质押奖励、治理投票、土地购买
- **分配方案**: 社区奖励 40% | 团队 20% | 生态发展 20% | 其他 20%

详细的智能合约文档请查看 [docs/SMART_CONTRACTS.md](docs/SMART_CONTRACTS.md)。

## 技术文档

- 📖 [技术架构](docs/ARCHITECTURE.md) - 系统架构设计和技术选型
- 🔗 [区块链方案](docs/BLOCKCHAIN.md) - Solana 集成和链上/链下分工
- 📜 [智能合约](docs/SMART_CONTRACTS.md) - 合约架构和代币经济
- ✨ [功能特性](docs/FEATURES.md) - 已实现和计划功能
- 🗺️ [发展路线图](docs/ROADMAP.md) - 详细的产品路线图和里程碑

## 快速路线图

### 2026 Q1 - 基础设施 🏗️
- [x] 基础 3D 场景搭建
- [x] 钱包连接功能
- [x] 多语言支持
- [ ] NFT 合约测试网部署

### 2026 Q2 - NFT 和市场 🎨
- [ ] Character NFT 铸造
- [ ] Land NFT 首次发售
- [ ] 交易市场上线
- [ ] DGC 代币发布

### 2026 Q3 - 游戏化 🎮
- [ ] 角色升级系统
- [ ] 土地开发功能
- [ ] 质押挖矿
- [ ] 社交功能

### 2026 Q4 - DAO 治理 🌐
- [ ] 治理系统上线
- [ ] 创作者工具包
- [ ] 生态系统扩展

完整路线图请查看 [docs/ROADMAP.md](docs/ROADMAP.md)。

## 开发团队

本项目为黑客松参赛作品，致力于探索 Web3 和 3D 技术的结合可能性，构建一个去中心化、社区驱动的虚拟城市元宇宙。

## 社区和联系

- 🌐 官网: [https://degener.city/](https://degener.city/)
- 📦 GitHub: [https://github.com/luzhenqian/degener-city-hackathon](https://github.com/luzhenqian/degener-city-hackathon)
- 📖 文档: [docs/](docs/)

## 贡献指南

欢迎社区贡献！请查看我们的贡献指南（开发中）。

## 许可证

MIT License - 详见 [LICENSE](LICENSE) 文件

---

**注意**: 本仓库为黑客松展示版本，包含项目架构和技术说明，展示了我们的技术创新和愿景。完整的生产代码和美术素材在私有仓库中开发。

**加入我们，一起建设 Degener City！** 🌆✨
