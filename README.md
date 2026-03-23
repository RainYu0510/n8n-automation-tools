# n8n Automation Tools

以 **n8n** 建構的三套自動化工作流程，整合 OpenAI、Google Calendar、Notion、Discord、Gmail 等服務，涵蓋 AI 行程管理、新聞推播、社團問答三個應用場景。

---

## 工作流程總覽

| # | 名稱 | 觸發方式 | 核心整合 |
|---|------|----------|----------|
| 1 | Discord Calendar Agent | Discord 訊息（Webhook） | OpenAI GPT-4.1-mini × Google Calendar |
| 2 | 自動推播新聞工具 | 每日 08:00（排程） | OpenAI GPT-4.1-mini × TechCrunch RSS × Gmail |
| 3 | Notion 社課問答機器人 | Discord 訊息（Webhook） | OpenAI GPT-4.1-mini × Notion Database × Discord |

---

## 1. Discord Calendar Agent

### 功能說明
在 Discord 頻道直接用自然語言管理 Google Calendar，支援新增、查詢、修改、刪除四種行程操作，無需開啟日曆應用程式。

### 流程架構
```
Discord 訊息
    → Webhook 接收
    → AI Agent（GPT-4.1-mini）判斷意圖
    → Google Calendar 工具執行對應操作
        ├── Create   新增行程
        ├── Get Many 查詢行程
        ├── Update   修改行程
        └── Delete   刪除行程
    → Discord 回覆執行結果
```

### 使用範例
```
使用者：幫我在明天下午三點新增「期末報告」，到五點結束
Bot：✅ 已新增行程「期末報告」2025/06/10 15:00–17:00

使用者：這週有什麼行程？
Bot：📅 本週行程如下：...

使用者：把期末報告改到四點開始
Bot：✅ 已更新行程時間為 16:00–18:00
```

### 所需憑證
- OpenAI API Key
- Google Calendar OAuth2
- Discord Bot Token

---

## 2. 自動推播新聞工具

### 功能說明
每天早上 08:00 自動從 TechCrunch RSS 抓取最新文章，由 AI 篩選出與 AI／機器學習／LLM 相關的新聞，翻譯成繁體中文後整合成一封摘要信寄送至指定 Gmail。

### 流程架構
```
Schedule Trigger（每日 08:00）
    → RSS Feed 讀取 TechCrunch 最新文章
    → Edit Fields 整理標題與連結
    → Aggregate 彙整所有文章為單一輸入
    → AI Agent（GPT-4.1-mini）
        ├── 篩選 AI / ML / LLM 相關新聞
        └── 翻譯成繁體中文
    → Gmail 寄送每日摘要信
```

### 信件格式
- **主旨**：`🤖 今日 AI 新聞 YYYY-MM-DD`
- **內容**：AI 相關新聞標題（繁中）+ 原文連結，彙整於單封郵件

### 所需憑證
- OpenAI API Key
- Gmail OAuth2

---

## 3. Notion 社課問答機器人

### 功能說明
串接 Notion 資料庫與 Discord，讓社員直接在 Discord 頻道用自然語言查詢社課資訊（時間、地點、講師、報名連結等），AI 只回答社課相關問題，超出範圍的問題會明確拒答。

### 流程架構
```
Discord 訊息
    → Webhook 接收
    → Notion Database 讀取所有社課活動資料
    → JavaScript 解析並結構化欄位
        （時間、活動名稱、地點、講師、類型、說明、報名連結）
    → AI Agent（GPT-4.1-mini）根據資料回答問題
    → Discord 回覆查詢結果
```

### Notion 資料庫欄位
| 欄位 | 型別 | 說明 |
|------|------|------|
| 時間 | Title | 社課日期與時段 |
| 活動名稱 | Rich Text | 社課或活動名稱 |
| 地點 | Select | 舉辦地點 |
| 講師 | Rich Text | 主講人 |
| 類型 | Select | 活動分類 |
| 說明 | Rich Text | 內容簡介 |
| 報名連結 | URL | 報名表單連結 |

### 使用範例
```
使用者：下週有社課嗎？
Bot：下週三晚上 7 點有「Python 爬蟲入門」，地點在 R303，講師是 XXX。

使用者：報名連結在哪？
Bot：報名連結：https://forms.gle/...

使用者：明天天氣怎樣？
Bot：我只能回答社課相關問題喔！
```

### 所需憑證
- OpenAI API Key
- Notion API Key
- Discord Bot Token

---

## 快速開始

### 環境需求
- n8n（self-hosted 或 n8n Cloud）
- OpenAI 帳號（使用 `gpt-4.1-mini`）

### 匯入流程
1. 在 n8n 介面點選 **Import from file**
2. 選擇對應的 `.json` 檔案匯入
3. 進入各節點設定憑證（見下方）
4. 啟用工作流程（Toggle Active）

### 憑證設定

**Discord Calendar Agent** 與 **Notion 社課機器人**需要額外設定 Discord Bot Webhook，將 Bot 的 Interaction URL 指向 n8n Webhook 路徑。

| 服務 | 取得方式 |
|------|----------|
| OpenAI | [platform.openai.com](https://platform.openai.com) → API Keys |
| Google Calendar | Google Cloud Console → OAuth2 憑證 |
| Gmail | Google Cloud Console → OAuth2 憑證 |
| Notion | [notion.so/my-integrations](https://www.notion.so/my-integrations) |
| Discord Bot | [discord.com/developers](https://discord.com/developers/applications) |

---

## 技術架構

所有工作流程均基於 **n8n LangChain 節點**建構 AI Agent，採用工具調用（Tool Calling）模式讓 LLM 自主決定執行哪個操作，而非硬編碼 if/else 邏輯。這使得系統能以自然語言作為唯一介面，同時保持對外部服務的精確控制。

---

## 作者

**余萬崧** — 大同大學資訊工程學系
