# 区块链技术方案

## 为什么选择 Solana？

### 技术优势

1. **高性能**
   - TPS：理论最高 65,000+ 每秒
   - 区块时间：约 400ms
   - 低延迟：适合实时游戏交互

2. **低成本**
   - 交易费用：平均 $0.00025
   - 用户友好：降低参与门槛
   - 可持续性：适合高频交互

3. **环保**
   - PoS 共识机制
   - 能源效率高
   - 碳中和目标

4. **生态成熟**
   - 丰富的开发工具
   - 活跃的开发者社区
   - 完善的 DeFi 基础设施

## 技术架构

### 链上/链下分工

```
┌─────────────────────────────────────────┐
│              客户端层                     │
│   React + Three.js + Wallet Adapter     │
└─────────────────────────────────────────┘
                    ↓
┌─────────────────────────────────────────┐
│            Web3 交互层                    │
│        Solana Web3.js SDK               │
└─────────────────────────────────────────┘
                    ↓
┌──────────────────┬──────────────────────┐
│    链上层         │      链下层           │
│  Smart Contracts │   Game Server        │
│  (Solana)        │   (Centralized)      │
└──────────────────┴──────────────────────┘
```

### 链上处理
- ✅ NFT 铸造和转移
- ✅ 代币交易
- ✅ 土地所有权
- ✅ 市场交易
- ✅ 治理投票
- ✅ 质押和解押

### 链下处理
- ⚡ 3D 场景渲染
- ⚡ 实时聊天
- ⚡ 游戏逻辑计算
- ⚡ 临时状态存储
- ⚡ 社交互动

## Solana 程序架构

### 使用的标准程序

#### 1. Token Program (代币程序)
```
地址: TokenkegQfeZyiNwAJbNbGKPFXCWuBvf9Ss623VQ5DA
用途: 管理 SPL Token (DGC)
```

#### 2. Metaplex NFT Standard
```
程序: Metaplex Token Metadata Program
用途: NFT 元数据管理
特性:
  - 符合行业标准
  - 支持 Royalty
  - 兼容主流钱包和市场
```

#### 3. Associated Token Account
```
用途: 简化代币账户管理
优势: 确定性地址、用户友好
```

### 自定义程序

#### 1. Character Program
```rust
// 伪代码示例
pub mod character_program {
    use anchor_lang::prelude::*;

    #[program]
    pub mod character {
        use super::*;

        pub fn mint_character(
            ctx: Context<MintCharacter>,
            metadata_uri: String,
        ) -> Result<()> {
            // 铸造角色 NFT
            // 初始化属性
            // 设置元数据
            Ok(())
        }

        pub fn level_up(
            ctx: Context<LevelUp>,
        ) -> Result<()> {
            // 验证经验值
            // 提升等级
            // 更新属性
            Ok(())
        }
    }
}
```

#### 2. Land Program
```rust
pub mod land_program {
    use anchor_lang::prelude::*;

    #[program]
    pub mod land {
        use super::*;

        pub fn mint_land(
            ctx: Context<MintLand>,
            x: i32,
            y: i32,
            size: LandSize,
        ) -> Result<()> {
            // 验证坐标可用性
            // 铸造土地 NFT
            // 记录坐标映射
            Ok(())
        }

        pub fn develop_land(
            ctx: Context<DevelopLand>,
            development_type: DevelopmentType,
        ) -> Result<()> {
            // 验证所有权
            // 消耗资源
            // 提升开发等级
            Ok(())
        }
    }
}
```

## 账户结构设计

### Character Account
```rust
#[account]
pub struct Character {
    pub owner: Pubkey,              // 32 bytes
    pub mint: Pubkey,               // 32 bytes
    pub level: u8,                  // 1 byte
    pub experience: u64,            // 8 bytes
    pub strength: u16,              // 2 bytes
    pub intelligence: u16,          // 2 bytes
    pub vitality: u16,              // 2 bytes
    pub luck: u16,                  // 2 bytes
    pub created_at: i64,            // 8 bytes
    pub last_action: i64,           // 8 bytes
    pub metadata_uri: String,       // 4 + 256 bytes
    // Total: ~358 bytes
}
```

### Land Account
```rust
#[account]
pub struct Land {
    pub owner: Pubkey,              // 32 bytes
    pub mint: Pubkey,               // 32 bytes
    pub x: i32,                     // 4 bytes
    pub y: i32,                     // 4 bytes
    pub size: LandSize,             // 1 byte
    pub development_level: u8,      // 1 byte
    pub buildings: Vec<Building>,   // 4 + (n * 32) bytes
    pub last_harvest: i64,          // 8 bytes
    pub metadata_uri: String,       // 4 + 256 bytes
    // Total: ~342 + buildings bytes
}
```

## 交易优化

### Batch 交易
```typescript
// 批量处理多个操作
const transaction = new Transaction()
transaction.add(
  instruction1,
  instruction2,
  instruction3
)

// 单次签名，降低成本
const signature = await sendAndConfirmTransaction(
  connection,
  transaction,
  [payer]
)
```

### 优先费用
```typescript
// 在高峰期提高交易优先级
const instruction = ComputeBudgetProgram.setComputeUnitPrice({
  microLamports: 1000, // 可调整
})
transaction.add(instruction)
```

### 交易重试机制
```typescript
async function sendTransactionWithRetry(
  connection: Connection,
  transaction: Transaction,
  signers: Keypair[],
  maxRetries = 3
) {
  for (let i = 0; i < maxRetries; i++) {
    try {
      const signature = await sendAndConfirmTransaction(
        connection,
        transaction,
        signers
      )
      return signature
    } catch (error) {
      if (i === maxRetries - 1) throw error
      await sleep(1000 * (i + 1))
    }
  }
}
```

## 安全措施

### 1. 访问控制
```rust
// 验证签名者
#[derive(Accounts)]
pub struct MintCharacter<'info> {
    #[account(mut)]
    pub payer: Signer<'info>,

    #[account(
        mut,
        constraint = authority.key() == payer.key()
    )]
    pub authority: Account<'info, Authority>,
}
```

### 2. 重入保护
```rust
// 使用标志位防止重入
#[account(mut)]
pub struct GameState {
    pub is_locked: bool,
    // ...
}

// 操作前检查
require!(!game_state.is_locked, ErrorCode::Locked);
game_state.is_locked = true;

// 操作后解锁
game_state.is_locked = false;
```

### 3. 溢出保护
```rust
use anchor_lang::prelude::*;

// 使用 checked 操作
let new_level = character.level
    .checked_add(1)
    .ok_or(ErrorCode::Overflow)?;

let new_exp = character.experience
    .checked_sub(required_exp)
    .ok_or(ErrorCode::InsufficientExperience)?;
```

## 性能优化

### 1. 账户租金优化
```rust
// 使用 close 回收租金
#[account(
    mut,
    close = receiver
)]
pub temp_account: Account<'info, TempData>,
```

### 2. 数据压缩
```rust
// 使用位标志减少存储
pub struct CharacterFlags {
    pub flags: u32, // 可以存储32个布尔值
}

impl CharacterFlags {
    pub fn set_premium(&mut self) {
        self.flags |= 1 << 0;
    }

    pub fn is_premium(&self) -> bool {
        (self.flags & (1 << 0)) != 0
    }
}
```

### 3. 预计算优化
```rust
// 预计算常见值，避免重复计算
pub const EXPERIENCE_TABLE: [u64; 100] = [
    100, 220, 350, 500, 670, // ...
];

pub fn get_required_exp(level: u8) -> u64 {
    EXPERIENCE_TABLE[level as usize]
}
```

## 监控和分析

### RPC 端点
```typescript
// 生产环境使用专业 RPC 服务
const connection = new Connection(
  process.env.SOLANA_RPC_URL ||
  'https://api.mainnet-beta.solana.com',
  'confirmed'
)
```

### 链上数据索引
- 使用 The Graph Protocol
- 自建索引服务
- 缓存常用查询

### 交易监控
```typescript
// 监听交易状态
connection.onSignature(
  signature,
  (result) => {
    if (result.err) {
      console.error('Transaction failed:', result.err)
    } else {
      console.log('Transaction confirmed!')
    }
  },
  'confirmed'
)
```

## 开发工具

### Anchor Framework
```bash
# 安装 Anchor
cargo install --git https://github.com/coral-xyz/anchor anchor-cli --locked

# 初始化项目
anchor init degener-city-contracts

# 构建
anchor build

# 测试
anchor test

# 部署
anchor deploy --provider.cluster devnet
```

### Solana CLI
```bash
# 查看余额
solana balance

# 空投测试币
solana airdrop 2

# 查看账户
solana account <ADDRESS>

# 部署程序
solana program deploy target/deploy/program.so
```

## 测试策略

### 单元测试
```rust
#[cfg(test)]
mod tests {
    use super::*;

    #[test]
    fn test_level_up() {
        // 测试角色升级逻辑
    }
}
```

### 集成测试
```typescript
import * as anchor from "@coral-xyz/anchor"

describe("character-program", () => {
  it("Mints a character", async () => {
    // 测试完整的铸造流程
  })
})
```

### 压力测试
- 模拟高并发交易
- 测试账户租金消耗
- 验证错误处理

## 主网部署清单

- [ ] 代码审计完成
- [ ] 测试网全面测试
- [ ] 性能基准测试
- [ ] 安全评估
- [ ] 多签钱包设置
- [ ] 应急预案准备
- [ ] 监控系统就绪
- [ ] 文档完善
- [ ] 社区公告

## 资源链接

- [Solana 官方文档](https://docs.solana.com/)
- [Anchor 框架](https://www.anchor-lang.com/)
- [Metaplex 文档](https://docs.metaplex.com/)
- [Solana Cookbook](https://solanacookbook.com/)
- [Solana Program Library](https://spl.solana.com/)
