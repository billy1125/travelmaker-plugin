# Travelmaker — Claude Code 旅遊規劃 Plugin

> **Trip Planning Plugin for Claude Code** — 用自然語言在 Claude Code 裡規劃自助旅行，行程全部存成純 Markdown，放進你自己的 git repo。

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Claude Code](https://img.shields.io/badge/Claude%20Code-Plugin-7C3AED.svg)](https://claude.com/claude-code)
[![語言](https://img.shields.io/badge/%E8%AA%9E%E8%A8%80-%E7%B9%81%E9%AB%94%E4%B8%AD%E6%96%87-0A7BBB.svg)](#-語言-language)

用 Claude Code 規劃自助旅行的一整套工作流程。所有行程資料都是**純 Markdown 檔案**，放在你自己的 **git repo** 裡：**總行程**一張表、**每天一個檔案**、**交通指南**逐段累積、**參考網站**自動整理摘要。不綁任何旅遊平台、可版本控管、可離線閱讀。

**關鍵字 Keywords**：Claude Code plugin、旅遊規劃、自助旅行行程、行程表 Markdown、trip planning、itinerary planner、travel itinerary、Claude Code skill、日本自由行、繁體中文。

想知道用這套流程能做出什麼，直接看 **[examples/okayama-2026/](examples/okayama-2026/)** —— 一趟真實規劃的 2026 日本岡山・倉敷・尾道 9 天 8 晚行程。

---

## 🧭 為什麼用 Travelmaker Why

- **資料是純 Markdown，進你自己的 git**：行程不鎖在任何 App 或網站，可版本控管、可離線看、想搬就搬。
- **討論前先讀齊資料，不憑空推測**：`/discuss-itinerary` 會先讀完整份行程、交通指南與參考資源，再開始討論。
- **交通指南逐段累積**：每查過一段接駁就存成一檔，下次直接取用，不必重查。
- **參考網站自動歸檔**：討論中抓過的網頁整理成「對旅程有用的具體事實」摘要，依五大分類存檔，免得每次重抓。

## 🚀 安裝 Installation

在 Claude Code 中執行：

```
/plugin marketplace add billy1125/travelmaker-plugin
/plugin install travelmaker@travelmaker-plugin
```

## 🔄 工作流程 Workflow

```
/new-trip ──► /discuss-itinerary ──► 與 Claude 討論 ──► /update-itinerary ──► /save-website-abstract
（初始化一次）   （每次討論前）        （可委派代理人）      （變動寫入檔案）       （網站摘要歸檔）
                      ▲                                                            │
                      └────────────────────── 反覆循環，直到出發 ◄─────────────────┘
```

1. **`/new-trip`** — 建立新旅程專案：目錄結構、`itinerary.md` 骨架、每日檔案、CLAUDE.md 工作流程說明。只需提供目的地與日期，其餘可後補。
2. **`/discuss-itinerary`** — 每次討論前執行，Claude 會先讀齊全部行程、交通指南與參考資源，確保討論有根據、不憑空推測。
3. **與 Claude 討論** — 貼參考網址、問交通接駁、調整景點順序。需要產出整份草稿時委派 **trip-planner** 代理人；要檢查可行性（時間衝突、公休日、預算）時委派 **trip-reviewer** 代理人。
4. **`/update-itinerary`** — 把討論確定的變動同步寫入 `itinerary.md` 與 `days/`，格式由內建規範統一。
5. **`/save-website-abstract`** — 討論中抓取過的網站，整理成「對旅程有用的具體事實」摘要，依交通／美食／購物／景點／行李準備五大分類歸檔，下次討論直接取用，不必重抓。

## 🧩 內容物 Skills & Agents

| 類型 | 名稱 | 用途 |
|---|---|---|
| Skill | `new-trip` | 初始化旅程專案（目錄、骨架檔案、CLAUDE.md） |
| Skill | `discuss-itinerary` | 討論前讀取全部行程與參考資源 |
| Skill | `update-itinerary` | 同步更新總行程與每日檔案（含格式規範） |
| Skill | `save-website-abstract` | 將抓取過的網站整理成分類摘要 |
| Agent | `trip-planner` | 旅遊規劃師：依需求產出結構化行程草稿（`itinerary_draft.md`） |
| Agent | `trip-reviewer` | 行程審查員：檢查時間可行性、公休日、地理動線、預算與風險，只審查不修改 |

## 💡 使用範例 Usage

實際在 Claude Code 裡的典型互動：

```
> /new-trip 幫我開一個 2026 京都 5 天 4 晚的行程專案
> /discuss-itinerary 第二天想加金閣寺，從清水寺怎麼接過去？順路嗎？
> （貼上一篇交通查詢網頁）幫我看一下這班巴士的班次和票價
> /update-itinerary 把剛剛確定的第二天改動寫進檔案
> /save-website-abstract 把今天查到的網站整理成摘要存起來
```

需要一次產出整份草稿，或想請人檢查行程是否可行時，在討論中委派 **trip-planner** / **trip-reviewer** 代理人即可。

## 🗂️ 產出的專案長什麼樣 Project structure

```
my-trip/
├── CLAUDE.md                  # 工作流程說明（/new-trip 產生）
├── itinerary.md               # 總行程：日期表（連到每日檔）+ 行程原則
├── days/
│   ├── 0828.md                # 每天一檔：時間表、交通、景點（含地圖連結）、備案
│   └── ...
├── assets/
│   ├── reference_website.md   # 使用者維護的參考連結索引
│   └── website_abstract.md    # Claude 整理的網站摘要
├── transportations/
│   └── OKJ_OkayamaStation.md  # 逐段累積的交通指南
└── luggage_items.md           # 行李準備清單
```

完整實例見 [examples/okayama-2026/](examples/okayama-2026/)。

## 🌐 語言 Language

本 plugin 的技能、格式規範與產出內容均為**繁體中文**。

## 📄 授權 License

[MIT](LICENSE) © 2026 Cho-Hsun Lu (billy1125) — 內容依 MIT「AS IS」提供，不負擔保責任。
