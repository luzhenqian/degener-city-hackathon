# Utils 工具函数目录

存放通用的工具函数和辅助方法。

## 建议的工具模块

```
utils/
├── solana.ts        # Solana 相关工具
├── format.ts        # 格式化函数
├── validation.ts    # 验证函数
├── constants.ts     # 常量定义
└── helpers.ts       # 其他辅助函数
```

## 示例

```typescript
// solana.ts
export const shortenAddress = (address: string, chars = 4): string => {
  return `${address.slice(0, chars)}...${address.slice(-chars)}`
}

export const lamportsToSol = (lamports: number): number => {
  return lamports / 1_000_000_000
}
```
