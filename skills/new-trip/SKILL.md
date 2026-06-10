---
name: new-trip
description: 初始化一個新的旅遊規劃專案：建立目錄結構、行程骨架檔案與工作流程說明（CLAUDE.md）
allowed-tools: Read Write Glob Bash AskUserQuestion
---

在目前的工作目錄初始化一個旅遊規劃專案。執行完成後，使用者即可用 `/discuss-itinerary` → 討論 → `/update-itinerary` → `/save-website-abstract` 的循環逐步完善行程。

## 執行步驟

### 1. 檢查目前目錄

- 用 Glob 檢查目前目錄是否已有 `itinerary.md` 或 `days/`
- 若已存在，**停止並詢問使用者**：這裡似乎已有行程專案，是要補齊缺少的檔案，還是選錯目錄？不可覆蓋既有內容

### 2. 收集基本資料

詢問使用者（已在對話中提供的不重問）：

1. **目的地與旅程描述**（例：日本岡山・倉敷・尾道）
2. **日期範圍**（出發日與回程日，據此推算天數與每日檔案清單）
3. **航班資訊**（航班號與時間；尚未訂票可填「待訂」）
4. **住宿安排**（各城市住幾晚；尚未訂房可填「待訂」）
5. **行程原則或限制**（例：早出發、不每天換飯店、有長輩同行；可留待之後討論再補）

只有 1、2 為必要，其餘可用佔位文字先建立骨架。

### 3. 建立目錄與檔案

依下列結構建立（格式規範參考 update-itinerary 技能的 `reference/itinerary_format.md` 與 `reference/day_format.md`，本技能目錄下的 `reference/` 也有範本）：

```
{專案目錄}/
├── CLAUDE.md                      # 由 reference/claude_md_template.md 產生，填入旅程資訊
├── README.md                      # 一段話描述本旅程 + 檔案結構表
├── itinerary.md                   # 總行程骨架：標頭、總覽表（每日一列）、行程原則
├── days/
│   └── MMDD.md                    # 每個旅程日一個檔案，含標題與「待規劃」佔位
├── assets/
│   └── reference_website.md       # 由 reference/reference_website_template.md 產生
└── transportations/
    └── .gitkeep                   # 交通指南之後依討論逐段新增
```

要求：

- `itinerary.md` 總覽表的日期欄使用 `[MM/DD](days/MMDD.md)` 連結格式，月日補零
- `days/MMDD.md` 至少包含 `# {MM/DD}（Day {N}）` 標題、住宿欄位與 `## 行程` 區塊（內容可為「待規劃」）
- 抵達日與回程日的每日檔案需填入航班資訊欄位
- `CLAUDE.md` 範本中的 `{...}` 佔位全部替換為實際資料；資料未定者填「待訂」「待規劃」

### 4. 回報結果

條列建立的檔案，並向使用者說明後續工作流程：

1. `/discuss-itinerary` — 每次討論行程前執行，讓 Claude 讀齊全部資料
2. 與 Claude 討論行程（可提供參考網址，或請 trip-planner / trip-reviewer 代理人協助）
3. `/update-itinerary` — 把討論確定的變動同步寫入 `itinerary.md` 與 `days/`
4. `/save-website-abstract` — 討論中有抓取網站時，將摘要歸檔到 `assets/website_abstract.md`

## 限制

- 不覆蓋任何既有檔案
- 所有產出內容使用繁體中文
