# Scenes 场景目录

这个目录用于存放 Three.js 3D 场景。

## 场景结构示例

```
scenes/
├── MainScene/       # 主场景
├── components/      # 场景组件
│   ├── Models/      # 3D 模型
│   ├── Effects/     # 特效
│   └── Controls/    # 控制器
└── utils/           # 场景工具函数
```

## 开发建议

- 使用 React Three Fiber 封装 Three.js
- 合理使用 drei 提供的辅助组件
- 注意性能优化，避免过多的重渲染
- 使用 useFrame 处理动画循环
