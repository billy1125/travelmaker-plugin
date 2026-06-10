# Changelog

## 未發佈

### 修正

- `update-itinerary`：移除有名無實的「歸檔舊版」描述（版本紀錄交給 git）；新增 `itinerary_draft.md` 草稿併入步驟（併入後刪除）與交通指南更新步驟
- `itinerary_format.md`：標頭格式改為 `## 行程概覽` 區塊＋粗體 bullet list，與範例一致
- 網站摘要分類由四類統一為五類（補上「行李準備」），與 `reference_website.md` 範本對齊
- 所有 SKILL.md 的 `allowed-tools` 改為逗號分隔
- `day_format.md`：通用規範中移除岡山行程特定的例子（地中美術館）
- `trip-planner` 代理人 model 由 `sonnet` 改為 `inherit`，與 `trip-reviewer` 一致

### 新增

- `transportation_format.md` — transportations/ 交通指南的格式規範（檔名規則、範本、規則）
- `new-trip` 明確說明 `luggage_items.md` 不在初始化時建立
- 專案根目錄 `CLAUDE.md`、`.gitignore`、`CHANGELOG.md`

## 0.1.0 — 2026-06-10

- 初始版本：4 個技能（new-trip、discuss-itinerary、update-itinerary、save-website-abstract）、2 個代理人（trip-planner、trip-reviewer）、okayama-2026 完整範例
