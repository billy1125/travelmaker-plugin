# Travelmaker — Claude Code 旅遊規劃 Plugin

用 Claude Code 規劃自助旅行的一整套工作流程。所有行程資料都是純 Markdown 檔案，放在你自己的 git repo 裡：總行程一張表、每天一個檔案、交通指南逐段累積、參考網站自動整理摘要。

想知道用這套流程能做出什麼，直接看 **[examples/okayama-2026/](examples/okayama-2026/)** —— 一趟真實規劃的 2026 日本岡山・倉敷・尾道 9 天 8 晚行程。

## 安裝

在 Claude Code 中執行：

```
/plugin marketplace add billy1125/travelmaker-plugin
/plugin install travelmaker@travelmaker-plugin
```

## 工作流程

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
5. **`/save-website-abstract`** — 討論中抓取過的網站，整理成「對旅程有用的具體事實」摘要，依交通／美食／購物／景點分類歸檔，下次討論直接取用，不必重抓。

## 內容物

| 類型 | 名稱 | 用途 |
|---|---|---|
| Skill | `new-trip` | 初始化旅程專案（目錄、骨架檔案、CLAUDE.md） |
| Skill | `discuss-itinerary` | 討論前讀取全部行程與參考資源 |
| Skill | `update-itinerary` | 同步更新總行程與每日檔案（含格式規範） |
| Skill | `save-website-abstract` | 將抓取過的網站整理成分類摘要 |
| Agent | `trip-planner` | 旅遊規劃師：依需求產出結構化行程草稿（`itinerary_draft.md`） |
| Agent | `trip-reviewer` | 行程審查員：檢查時間可行性、公休日、地理動線、預算與風險，只審查不修改 |

## 產出的專案長什麼樣

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
└── transportations/
    └── OKJ_OkayamaStation.md  # 逐段累積的交通指南
```

完整實例見 [examples/okayama-2026/](examples/okayama-2026/)。

## 語言

本 plugin 的技能、格式規範與產出內容均為**繁體中文**。

## License

MIT
