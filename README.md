# 🕊️ Human-as-a-Service (真·人工大模型)

> **别人以为在调最新的顶尖大模型，其实屏幕背后是你本尊在现场手打！**

一个将你自己伪装成标准 **OpenAI 兼容接口 (`/v1/chat/completions`)** 的轻量级 Web 服务。朋友可以在任何支持 OpenAI 格式的软件（如 NextChat、Cherry Studio、Chatbox、沉浸式翻译等）里调用你的接口，而你在手机上通过 **Telegram 机器人** 或 **微信风格的专属移动端独立工作台** 实时接收并回复提问！

---

## 📚 详细部署指南

👉 **[点击查看《零基础保姆级部署手册 (DEPLOY_GUIDE.md)》](./DEPLOY_GUIDE.md)**
*(包含 Telegram 机器人创建、Zeabur 一键配置、持久化磁盘挂载、环境变量详解、多模态发图、连环成精追问、时空留言箱与故障排查全流程)*

---

## ✨ 核心特性

- 🤖 **标准 OpenAI 接口兼容**：兼容 `/v1/chat/completions` 与 `/v1/models`，支持流式 SSE 打字机效果与非流式单次输出。
- 🛡️ **首次连接强制实名登记**：新朋友第一次发消息时，系统自动拦截并要求回复 `我是: 名字` 完成登记，未认证前不打扰你，认证后自动建立专属档案！
- 💬 **微信式单人专属独立对话框**：网页端采用移动端原生级滑动架构，点开谁就跟谁聊，互不串台。
- 🔐 **控制台密码与持久化存储**：`/admin` 专属后台受密码保护，支持挂载 `/app/data` 存储卷，换节点与重新部署数据永不丢失！
- 🖼️ **视觉多模态能力 (Vision)**：支持接收朋友发来的图片，原图直接推送给你的 Telegram 与网页端查看大图。
- ⏳ **10分钟充裕回复倒计时**：内置 3 秒高频心跳保活（Keep-Alive），连接绝不断开，顶部显示实时倒计时。
- ⚡ **连环追问（大模型成精模式）**：在对方发完一句话后，你可以连续发送多句话，对方屏幕会一段接一段吐字，宛如大模型拥有自我意识！
- 💌 **离线时空留言箱**：朋友没上线时可以给 Ta 预留悄悄话，下次 Ta 刚打开客户端发第一句话时立刻置顶弹出！
- 📜 **实时查看客户端隐藏 Prompt**：深紫色卡片支持折叠展开查看客户端暗中塞入的全部 System Prompt 和人设指令。
- 🔔 **Telegram 移动端推送**：手机无需挂网页，TG 机器人直接私聊弹窗，长按消息点回复即可传回。

---

## 🚀 极速部署流程 (Zeabur)

### 1. 准备 Telegram 参数（可选，但推荐）
* 打开 Telegram 搜索并进入 `@BotFather`，发送 `/newbot` 获取 `TELEGRAM_BOT_TOKEN`。
* 搜索并进入 `@userinfobot` 获取你的纯数字 `TELEGRAM_ADMIN_CHAT_ID`。
* 进入你刚建的机器人，点击底部的 **Start** 激活对话。

### 2. 在 Zeabur 部署
1. 点击右上角 **Fork** 本仓库。
2. 打开 [Zeabur](https://zeabur.com)，创建项目并点击 **Deploy from GitHub** 选择你 Fork 的仓库。
3. 在 **Variables（变量）** 中选择 **Raw Edit**，粘贴并修改：

```env
PORT=3000
MODEL_NAME=gugu-bot
API_KEY=0111
ADMIN_PASSWORD=your_admin_password
TELEGRAM_BOT_TOKEN=你的TG机器人Token
TELEGRAM_ADMIN_CHAT_ID=你的TG数字ID
DATA_DIR=/app/data
REPLY_TIMEOUT_SECONDS=600
TIMEOUT_FALLBACK_TEXT=（大模型算力节点过热，思考超时啦，请再试一次～）
```

4. 在 **Volumes（存储卷）** 点击 **Add Volume**，挂载路径填入 `/app/data`（防丢记录与备注）。
5. 在 **Networking（网络）** 点击 **Generate Domain** 生成公网访问域名（如 `xxx.zeabur.app`）。

---

## 📱 朋友怎么用？

发给朋友以下配置：
* **接口地址 (Base URL)**: `https://你的域名.zeabur.app/v1`（注意带 `/v1`）
* **API Key**: 填你在 `API_KEY` 设置的值（如 `0111`）
* **模型名称 (Model)**: 填你在 `MODEL_NAME` 设置的值（默认 `gugu-bot`）

朋友首次使用发第一句话时，按系统提示回复 `我是: 名字` 即可完成认证开始对话！

---

## 🖥️ 管理员后台

用手机浏览器打开：
👉 **`https://你的域名.zeabur.app/admin`**
* 输入 `ADMIN_PASSWORD` 登录，手机会自动记住状态。
* 具有完整的微信式独立会话列表、新提问红点闪烁、看图、人设展示、连环追发与留言箱功能。

---

## 📄 开源协议
MIT License
