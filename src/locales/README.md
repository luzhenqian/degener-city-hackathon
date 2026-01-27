# Locales 国际化目录

存放多语言翻译文件。

## 结构

```
locales/
├── zh-CN/
│   ├── common.json
│   └── wallet.json
└── en/
    ├── common.json
    └── wallet.json
```

## 翻译文件示例

```json
// zh-CN/common.json
{
  "welcome": "欢迎来到 Degener City",
  "connect": "连接钱包",
  "disconnect": "断开连接"
}

// en/common.json
{
  "welcome": "Welcome to Degener City",
  "connect": "Connect Wallet",
  "disconnect": "Disconnect"
}
```

## 使用方式

```typescript
import { useTranslation } from 'react-i18next'

function Component() {
  const { t } = useTranslation()
  return <h1>{t('common:welcome')}</h1>
}
```
