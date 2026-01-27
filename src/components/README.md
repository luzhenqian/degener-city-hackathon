# Components 组件目录

这个目录用于存放 React 组件。

## 建议的组件结构

```
components/
├── common/          # 通用组件
│   ├── Button/
│   ├── Modal/
│   └── Loading/
├── wallet/          # 钱包相关组件
│   ├── WalletButton/
│   └── WalletModal/
├── scene/           # 3D 场景组件
│   ├── Camera/
│   └── Lights/
└── ui/              # UI 组件
    ├── Header/
    ├── Footer/
    └── Sidebar/
```

## 组件开发规范

1. 每个组件一个文件夹
2. 包含 index.tsx 和 styles（如需要）
3. 使用 TypeScript 类型
4. 编写必要的 JSDoc 注释
