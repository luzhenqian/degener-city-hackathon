# Stores 状态管理目录

使用 Zustand 进行状态管理。

## Store 示例

```typescript
// walletStore.ts
import { create } from 'zustand'

interface WalletState {
  connected: boolean
  publicKey: string | null
  balance: number
  connect: () => Promise<void>
  disconnect: () => void
}

export const useWalletStore = create<WalletState>((set) => ({
  connected: false,
  publicKey: null,
  balance: 0,
  connect: async () => {
    // 连接逻辑
  },
  disconnect: () => {
    set({ connected: false, publicKey: null, balance: 0 })
  },
}))
```

## Store 分类

- `walletStore.ts` - 钱包状态
- `sceneStore.ts` - 3D 场景状态
- `userStore.ts` - 用户数据
- `appStore.ts` - 应用全局状态
