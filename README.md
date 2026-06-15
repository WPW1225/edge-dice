# 边缘骰子 · Edge Dice

> 掷出1即为边缘 —— 一个带云同步的骰子博弈游戏

## 🎲 游戏规则

| 事件 | 规则 |
|------|------|
| **掷骰** | 消耗 1 积分，掷出 1-6 |
| **安全（2-6）** | 点数累加到边缘进度，利率小幅下降 |
| **边缘（1）** | 当前进度归零，利率上升，5分钟禁令 |
| **兑换积分** | 边缘进度达到阈值 → 自动获得积分 |
| **利率衰减** | 边缘次数每30秒按利率衰减 |

### 操作流程
1. 用**边缘次数**兑换积分（或消耗进度换积分）
2. 用**积分**掷骰子
3. 安全 → 进度+利率优惠；边缘 → 进度清零+禁令
4. Admin 可调整参数、解除禁令

## ✨ 功能

- 🎲 3D CSS 骰子动画
- 🔐 Admin 密码保护
- 📊 实时统计面板（边缘次数、利率、积分、进度）
- ⏱️ 边缘禁令倒计时
- 📜 掷骰记录 + 管理员日志
- ☁️ Firebase Realtime Database 云同步
- 🎨 粒子背景 + 暗色主题
- 📱 响应式移动端适配

## 🚀 部署

### 方式一：Firebase Hosting

1. 创建 Firebase 项目 → 启用 **Realtime Database**（测试模式）
2. 在游戏中点击「云同步设置」填入 Firebase 配置
3. 部署：
```bash
npm install -g firebase-tools
firebase login
firebase init   # 选择 Hosting，public 目录填 .
firebase deploy
```

### 方式二：任意静态服务器

```bash
# Python
python3 -m http.server 8080

# Node
npx serve .
```

### Firestore 安全规则

```
{
  "rules": {
    "gameState": {
      ".read": true,
      ".write": true
    }
  }
}
```

> ⚠️ 测试模式规则允许所有人读写，生产环境请修改为认证规则

## 🔧 自定义

修改 `index.html` 中的常量：

```js
const ADMIN_PASSWORD = 'edge2024';  // 管理员密码
```

## 📁 项目结构

```
edge-dice/
├── index.html       # 完整游戏（单文件部署）
├── firebase.json    # Firebase Hosting 配置
└── README.md
```

## 📄 License

MIT
