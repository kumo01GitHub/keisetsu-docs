# keisetsu 文档

[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/kumo01GitHub/keisetsu-docs/pulls)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)

这是 keisetsu 整体设计意图和运营方针的文档中心。

`keisetsu-docs` 是一个集中管理所有 keisetsu 实现（publisher / database / mobile）跨仓库规范、运营规则和更新流程的地方。

- 明确每个仓库的职责
- 独立于实现记录分发和验证流程
- 在规范变更时维护共同的决策标准

## 概念

keisetsu 是一个开源单词卡应用，公开学习数据的存储方式和分发路径，让用户可以拥有并使用自己的学习资料。

- 目标
  - 创建一个任何人只需一部智能手机就能学习的环境
- 必要性
  - 解决数据不公开、依赖在线、更新路径不透明等现有问题
- 优势
  - 所有规范、数据和分发流程均公开透明
  - 开源：任何人都可以免费更新和使用数据
- 实现方式
  - 将制作（publisher）、分发（database）、使用（mobile）分离，便于更新和复用
  - 采用公开 schema 统一数据结构，公开 catalog 明确分发路径，支持离线学习的应用

## 用户指南

### 如何使用 keisetsu 移动应用

1. 在智能手机上安装 Expo Go 应用。
    - [Expo Go (iOS)](https://apps.apple.com/app/expo-go/id982107779)
    - [Expo Go (Android)](https://play.google.com/store/apps/details?id=host.exp.exponent)
2. 扫描二维码启动 keisetsu 应用。

![Expo QR](assets/eas-update.svg)

您可以立即开始使用 keisetsu 应用。

### 如何使用 keisetsu 网页牌组编辑器

1. 访问 [keisetsu-publisher 公共页面](https://keisetsu-publisher.vercel.app)
2. 新建牌组，或导入 CSV / 现有 kdb
3. 编辑卡片和牌组信息（ID、标题、语言等）
4. 下载 ZIP 文件
5. 解压下载的 ZIP 并将生成的文件放入 keisetsu-database，然后[提交添加/编辑请求](https://github.com/kumo01GitHub/keisetsu-database/issues)

### 支持的语言

- 英语 (`en`)
- 日语 (`ja`)
- 西班牙语 (`es`)
- 葡萄牙语 (`pt`)
- 中文 (`zh`)
- 韩语 (`ko`)

## 开发者指南

有关详细的仓库结构、运营规则和技术信息，请参阅 [DEVELOPER.md](./DEVELOPER.md)。
