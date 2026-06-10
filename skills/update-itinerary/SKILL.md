---
name: update-itinerary
description: 討論完行程異動後，同步更新 itinerary.md 與 days/ 每日檔案
disable-model-invocation: true
allowed-tools: Read, Write, Edit, Bash, PowerShell
---

每次討論有行程變動後，執行此技能，將最新內容同步到文件。舊版內容不另行歸檔——專案以 git 管理，版本紀錄交給 git。

## 格式規範

更新前請先閱讀（路徑相對於此 SKILL.md 所在目錄）：
- `reference/itinerary_format.md` — itinerary.md 的格式規範
- `reference/day_format.md` — days/ 每日檔的格式規範
- `reference/transportation_format.md` — transportations/ 交通指南的格式規範（僅在本次有交通指南異動時需要）

## 執行步驟

### 0. 檢查是否有待併入的草稿

若專案中存在 `itinerary_draft.md`（trip-planner 代理人的產出）：

- 與使用者確認是否以草稿內容作為本次更新依據
- 確認採用後，依下列步驟將草稿內容併入 `itinerary.md` 與 `days/`，**併入完成後刪除草稿檔**
- 使用者表明不採用，則忽略草稿，依討論結論更新

### 1. 更新 itinerary.md

依 `reference/itinerary_format.md` 將確認的行程變更寫入，範圍包括：

- 標頭（天數、日期、航班、住宿安排）
- 行程總覽表格（日期用 `MM/DD` 補零、住宿、摘要）
- 表格日期欄連結格式：`[MM/DD](days/MMDD.md)`
- 行程原則（如有調整）

### 2. 更新每日檔案

依 `reference/day_format.md` 更新或新增 `days/` 中受影響的檔案：

- 檔名格式：`MMDD.md`（月日補零，不含標題）
- 若已存在：直接更新內容
- 若為新日期：建立新檔案
- 若某日移除：不刪除舊檔，在檔案開頭加註 `> 此日已從行程移除（YYYY/MM/DD）`

### 3. 更新交通指南（如有）

若本次討論中查證了新的交通路段資訊（班次、票價、乘車位置等），依 `reference/transportation_format.md` 在 `transportations/` 新增或更新對應檔案，讓之後的討論直接取用、不必重查。

### 4. 回報修改清單

完成後條列：
- 各檔異動狀態（新增 / 修改 / 刪除）
- 若有併入草稿，註明 `itinerary_draft.md` 已併入並刪除

## 限制

- 不修改 `reference/` 內的格式規範檔案（相對於此技能目錄）
- 所有內容使用繁體中文
