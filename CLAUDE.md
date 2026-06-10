# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 這個 repo 是什麼

travelmaker 是一個 Claude Code plugin（純 Markdown，無程式碼，沒有建置、lint 或測試指令），提供以 Markdown 檔案為核心的旅遊規劃工作流程。所有技能、格式規範與產出內容一律**繁體中文**。

驗證方式：在 Claude Code 中以 `/plugin marketplace add`（指向本目錄）安裝後實際執行各技能。

## 架構

使用者端的核心循環（README 的工作流程圖）：

`/new-trip`（初始化，僅一次）→ `/discuss-itinerary`（討論前讀齊全部資料）→ 討論 → `/update-itinerary`（變動寫檔）→ `/save-website-abstract`（網站摘要歸檔）→ 回到討論，反覆循環。

各組件的分工：

- `skills/*/SKILL.md` — 四個技能的執行步驟。`update-itinerary` 設有 `disable-model-invocation: true`（只能由使用者觸發）。
- `skills/*/reference/` — 格式規範，是各檔案格式的**單一事實來源**：
  - `update-itinerary/reference/` — `itinerary_format.md`、`day_format.md`、`transportation_format.md`
  - `save-website-abstract/reference/` — `website_abstract_format.md`
  - `new-trip/reference/` — `claude_md_template.md`、`reference_website_template.md`（產生使用者專案的 CLAUDE.md 與參考連結索引）
- `agents/` — `trip-planner`（產出 `itinerary_draft.md` 草稿，由 `/update-itinerary` 步驟 0 負責併入後刪除）、`trip-reviewer`（只審查不修改，優先讀草稿、否則逐一讀 `days/*.md`）
- `examples/okayama-2026/` — 真實規劃的完整行程範例，兼作使用者文件（README 直接引導使用者看它）
- `.claude-plugin/plugin.json` 與 `marketplace.json` — plugin 發佈設定；版本號在 `plugin.json`

## 修改時的關鍵原則

- **格式規範與範例必須保持一致**：`skills/*/reference/` 的規範範本與 `examples/okayama-2026/` 的實際檔案是一體兩面，改其中一邊就要檢查另一邊。使用者實際模仿的是範例。
- 範例是真實規劃的行程（已移除個人資料檔案），原樣保留，不為了示範而虛構內容。
- 網站摘要與參考連結固定為**五個分類**：交通、美食、購物、景點、行李準備。新增分類需同步改 `reference_website_template.md`、`website_abstract_format.md`、`save-website-abstract/SKILL.md` 與 `discuss-itinerary/SKILL.md`。
- 設計約定「`assets/reference_website.md` 由使用者維護、Claude 不修改」貫穿多個技能，調整任一技能時不可破壞此約定。
- SKILL.md frontmatter 的 `allowed-tools` 使用逗號分隔。
- 每日檔名 `MMDD.md`（月日補零）、總覽表日期連結 `[MM/DD](days/MMDD.md)`、交通指南檔名 `{起點}_{訖點}.md`——這些命名規則同時出現在多個 SKILL.md 與格式規範中，修改時需全部同步。
- 行為變更記入 `CHANGELOG.md`，發佈時更新 `plugin.json` 版本號。
