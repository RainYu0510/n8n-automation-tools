# 🤖 AI 不只有聊天？做出屬於自己的 AI Agent 吧！
課程的學習筆記與實作成果
---

## 📖 關於這個 Repo

這裡存放我在 n8n AI Agent 課程中所有的學習資料，包含：

- 📄 課程講義 PDF
- 🔁 實作的 n8n 工作流程（`.json` 匯入檔）
- 💡 三個從零打造的自動化 AI Agent 專案

---

## 📁 檔案結構

```
n8n-automation-tools/
├── AI 不只有聊天？做出屬於自己的 AI Agent 吧！.pdf   # 課程講義
├── 1. Discord Calendar Agent.json                    # 實作一：行程管理 Agent
├── 2. 自動推播新聞工具.json                           # 實作二：每日新聞推播
└── 3. Notion.json                                    # 實作三：社課問答機器人
```

---

## 🛠 使用工具

| 工具 | 說明 |
|------|------|
| ![n8n](https://img.shields.io/badge/n8n-EA4B71?style=flat&logo=n8n&logoColor=white) | 自動化工作流程平台 |
| ![OpenAI](https://img.shields.io/badge/OpenAI-412991?style=flat&logo=openai&logoColor=white) | GPT-4.1-mini 語言模型 |
| ![Discord](https://img.shields.io/badge/Discord-5865F2?style=flat&logo=discord&logoColor=white) | 訊息觸發與回覆介面 |
| ![Google Calendar](https://img.shields.io/badge/Google%20Calendar-4285F4?style=flat&logo=googlecalendar&logoColor=white) | 行程管理服務 |
| ![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=flat&logo=gmail&logoColor=white) | 信件推播 |
| ![Notion](https://img.shields.io/badge/Notion-000000?style=flat&logo=notion&logoColor=white) | 社課資料庫 |

---

## 📚 課程實作一覽

### 1. Discord Calendar Agent

在 Discord 用自然語言管理 Google 行程，支援新增、查詢、修改、刪除。

**觸發方式**：Discord 訊息（Webhook）  
**核心整合**：OpenAI GPT-4.1-mini × Google Calendar

```
使用者：幫我在明天下午三點新增「期末報告」到五點
Bot：✅ 已新增行程「期末報告」2025/06/10 15:00–17:00
```

---

### 2. 自動推播新聞工具

每天早上 08:00 自動從 TechCrunch RSS 抓取最新文章，由 AI 篩選 AI／ML／LLM 相關新聞，翻譯成繁體中文後寄送到 Gmail。

**觸發方式**：每日 08:00 排程  
**核心整合**：OpenAI GPT-4.1-mini × TechCrunch RSS × Gmail

---

### 3. Notion 社課問答機器人

串接 Notion 資料庫，讓社員在 Discord 直接查詢社課時間、地點、講師、報名連結等資訊。

**觸發方式**：Discord 訊息（Webhook）  
**核心整合**：OpenAI GPT-4.1-mini × Notion Database × Discord

```
使用者：下週有社課嗎？
Bot：下週三晚上 7 點有「Python 爬蟲入門」，地點在 R303，講師是 XXX。
```

---

## 🚀 如何匯入工作流程

1. 開啟 n8n（self-hosted 或 n8n Cloud）
2. 點選右上角 **Import from file**
3. 選擇對應的 `.json` 檔案匯入
4. 進入各節點補上所需的 API 憑證
5. 點擊 **Toggle Active** 啟用流程

### 所需憑證

| 服務 | 取得方式 |
|------|---------|
| OpenAI | [platform.openai.com](https://platform.openai.com) → API Keys |
| Google Calendar / Gmail | Google Cloud Console → OAuth2 憑證 |
| Notion | [notion.so/my-integrations](https://www.notion.so/my-integrations) |
| Discord Bot | [discord.com/developers](https://discord.com/developers/applications) |

---

## 👤 作者

**余萬崧（Rain Yu）**  
大同大學資訊工程學系

[![GitHub](https://img.shields.io/badge/GitHub-RainYu0510-181717?style=flat&logo=github)](https://github.com/RainYu0510)
[![HackMD](https://img.shields.io/badge/HackMD-RainYu0510-14b8a6?style=flat)](https://hackmd.io/@RainYu0510)

---

© 2026 Rain Yu. All rights reserved.
