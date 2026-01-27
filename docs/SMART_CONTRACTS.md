# 智能合约文档

## 概述

Degener City 使用 Solana 区块链构建去中心化的游戏经济系统，通过智能合约实现资产所有权、交易市场和游戏机制。

## 合约架构

### 主要合约模块

```
contracts/
├── nft/              # NFT 资产合约
│   ├── character/    # 角色 NFT
│   ├── land/         # 土地 NFT
│   └── item/         # 道具 NFT
├── marketplace/      # 交易市场合约
├── staking/          # 质押奖励合约
├── governance/       # 治理合约
└── game/            # 游戏逻辑合约
```

## 核心合约说明

### 1. Character NFT Contract (角色 NFT)

**功能**:
- 铸造独特的角色 NFT
- 角色属性和等级系统
- 角色升级和进化
- 可交易和转让

**数据结构**:
```rust
pub struct Character {
    pub owner: Pubkey,
    pub level: u8,
    pub experience: u64,
    pub attributes: CharacterAttributes,
    pub created_at: i64,
    pub metadata_uri: String,
}

pub struct CharacterAttributes {
    pub strength: u16,
    pub intelligence: u16,
    pub vitality: u16,
    pub luck: u16,
}
```

**主要方法**:
- `initialize_character` - 初始化新角色
- `level_up_character` - 角色升级
- `transfer_character` - 转让角色
- `update_attributes` - 更新属性

### 2. Land NFT Contract (土地 NFT)

**功能**:
- 虚拟土地铸造和管理
- 土地坐标系统
- 土地开发和建设
- 土地租赁机制

**数据结构**:
```rust
pub struct Land {
    pub owner: Pubkey,
    pub coordinates: (i32, i32),
    pub size: LandSize,
    pub development_level: u8,
    pub buildings: Vec<Building>,
    pub metadata_uri: String,
}

pub enum LandSize {
    Small,
    Medium,
    Large,
    Mega,
}
```

**主要方法**:
- `mint_land` - 铸造土地
- `develop_land` - 开发土地
- `build_structure` - 建造建筑
- `rent_land` - 土地租赁

### 3. Marketplace Contract (交易市场)

**功能**:
- NFT 挂单和购买
- 竞价拍卖系统
- 交易手续费管理
- 交易历史记录

**数据结构**:
```rust
pub struct Listing {
    pub seller: Pubkey,
    pub nft_mint: Pubkey,
    pub price: u64,
    pub listing_type: ListingType,
    pub created_at: i64,
    pub expires_at: Option<i64>,
}

pub enum ListingType {
    FixedPrice,
    Auction { min_bid: u64, current_bid: u64 },
}
```

**主要方法**:
- `create_listing` - 创建挂单
- `buy_nft` - 购买 NFT
- `place_bid` - 竞价出价
- `cancel_listing` - 取消挂单

### 4. Staking Contract (质押奖励)

**功能**:
- NFT 质押挖矿
- 流动性池质押
- 奖励分发机制
- 解押和提取

**数据结构**:
```rust
pub struct StakePool {
    pub authority: Pubkey,
    pub token_mint: Pubkey,
    pub reward_rate: u64,
    pub total_staked: u64,
    pub start_time: i64,
}

pub struct StakeAccount {
    pub owner: Pubkey,
    pub pool: Pubkey,
    pub amount: u64,
    pub reward_debt: u64,
    pub last_stake_time: i64,
}
```

**主要方法**:
- `create_stake_pool` - 创建质押池
- `stake_tokens` - 质押代币
- `unstake_tokens` - 解除质押
- `claim_rewards` - 领取奖励

### 5. Governance Contract (治理)

**功能**:
- 社区提案系统
- 投票机制
- 参数调整治理
- 国库管理

**数据结构**:
```rust
pub struct Proposal {
    pub id: u64,
    pub proposer: Pubkey,
    pub title: String,
    pub description: String,
    pub votes_for: u64,
    pub votes_against: u64,
    pub status: ProposalStatus,
    pub created_at: i64,
    pub voting_ends_at: i64,
}

pub enum ProposalStatus {
    Active,
    Passed,
    Rejected,
    Executed,
}
```

**主要方法**:
- `create_proposal` - 创建提案
- `vote` - 投票
- `execute_proposal` - 执行提案
- `cancel_proposal` - 取消提案

## 代币经济

### DGC Token (主代币)

- **总供应量**: 1,000,000,000 DGC
- **用途**:
  - 游戏内购买和交易
  - 质押获得奖励
  - 治理投票权
  - 土地购买和开发

### 分配方案

```
├── 社区奖励: 40% (400M)
├── 团队和顾问: 20% (200M, 2年线性解锁)
├── 生态发展: 20% (200M)
├── 流动性池: 10% (100M)
├── 种子轮: 5% (50M)
└── 公开发售: 5% (50M)
```

## 安全措施

### 1. 访问控制
- 基于角色的权限管理
- 多签钱包管理关键操作
- 时间锁机制

### 2. 审计
- 代码审计计划
- 漏洞赏金计划
- 持续安全监控

### 3. 升级机制
- 可升级的代理合约模式
- 治理投票批准升级
- 紧急暂停功能

## 开发路线

### Phase 1: 基础合约 (Q1 2026)
- [x] NFT 基础合约
- [x] 钱包集成
- [ ] 测试网部署

### Phase 2: 市场和经济 (Q2 2026)
- [ ] 交易市场上线
- [ ] 质押系统
- [ ] 代币分发

### Phase 3: 治理和社区 (Q3 2026)
- [ ] 治理合约
- [ ] DAO 组织
- [ ] 社区国库

### Phase 4: 高级功能 (Q4 2026)
- [ ] 跨链桥
- [ ] 第三方集成 API
- [ ] 移动端支持

## 技术规范

### 使用的 Solana 程序
- **Metaplex**: NFT 标准和元数据
- **Token Program**: SPL Token 管理
- **Associated Token Account**: 关联代币账户
- **System Program**: 基础系统调用

### 开发工具
- **Anchor Framework**: 智能合约开发框架
- **Solana Web3.js**: JavaScript SDK
- **Phantom/Solflare**: 钱包支持
- **Rust**: 合约编程语言

## 测试网信息

### Devnet 部署地址 (示例)

```
Character NFT:     Char1111111111111111111111111111111111111
Land NFT:          Land1111111111111111111111111111111111111
Marketplace:       Mark1111111111111111111111111111111111111
Staking Pool:      Stak1111111111111111111111111111111111111
Governance:        Gove1111111111111111111111111111111111111
DGC Token:         DGCt1111111111111111111111111111111111111
```

### 水龙头
- 获取测试 SOL: https://solfaucet.com
- 获取测试 DGC: (待上线)

## API 文档

详细的合约 API 文档和集成指南将在主网上线前发布。

## 社区和支持

- Discord: (待公布)
- Twitter: (待公布)
- GitHub: https://github.com/luzhenqian/degener-city-hackathon
- 文档站: (开发中)
