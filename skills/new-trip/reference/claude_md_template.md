# CLAUDE.md 範本

`/new-trip` 依此範本產生專案的 `CLAUDE.md`，將 `{...}` 佔位替換為實際資料。

---

```markdown
# CLAUDE.md

此檔案提供給 Claude Code（claude.ai/code）在此專案目錄中工作時的指引。

## 這個專案是什麼

這是一個個人旅遊規劃目錄，記錄 {年份} {目的地描述}之旅，並非軟體專案。目錄結構：

- `itinerary.md` — 主行程總覽（含各日連結），包括行程的使用者基本設定，關於行程的基本資料都從這裡開始
- `days/` — 每日詳細行程，各自獨立的 Markdown 檔案（命名格式：`MMDD.md`）
- `assets/` — 參考資料（機票、住宿確認書、網站參考資源索引與摘要）
- `transportations/` — 各路段交通指南（命名格式：`起訖點代碼_路段.md`）
- `README.md` — 簡易專案說明

## 工作流程

1. 執行 `/discuss-itinerary`
   - 自動讀取全部行程、交通指南與參考資源，確保討論有完整的資料基礎
   - 若使用者提供外部網址，抓取後納入；需即時資訊則網路搜尋

2. 與使用者討論
   - 依據前述資料與使用者的限制，完成希望的行程內容
   - 需要產出行程草稿時可委派 trip-planner 代理人；需要檢查可行性時委派 trip-reviewer 代理人

3. 執行 `/update-itinerary`
   - 同步更新 `itinerary.md` 與 `days/` 內的受影響檔案

4. 整理資料（強制：凡本次討論中有抓取任何網站內容，即須執行）
   - 執行 `/save-website-abstract`
   - 逐一確認每個已抓取的網站：若 `assets/website_abstract.md` 尚無該網站的摘要，補寫並歸入對應分類

## 資料來源

- {列出 assets/ 內的機票、訂房等檔案，各一行說明}
- `assets/reference_website.md` — 網頁參考資源索引（交通、美食、購物、景點連結），*由使用者維護*
- `assets/website_abstract.md` — Claude 整理的網站摘要（依 `reference_website.md` 分類歸入）

## 編輯行程時的原則

- 行程的限制與條件，設定在 `itinerary.md`
- 去回程日若有對應交通指南，在每日檔案標頭加入連結
- 新增或修改行程時，執行 `/update-itinerary` 同步 `itinerary.md` 與 `days/` 對應檔案
- 討論中只要有抓取網站內容，結束前必須執行 `/save-website-abstract`
- {其他使用者指定的原則}
```
