# 範例：2026 日本岡山・倉敷・尾道 9 天 8 晚

這是一趟**真實規劃中的旅程**，完整使用 travelmaker 工作流程產出，原樣保留作為範例（僅移除電子機票、訂房確認書等含個人資料的檔案）。

## 從哪裡開始看

1. **[itinerary.md](itinerary.md)** — 總行程：9 天總覽表（每列連到當日細節）與行程原則。注意「行程原則」如何記錄使用者限制（早出發、不每天換飯店），後續所有討論都以此為準。
2. **[days/](days/)** — 每日檔案。看 [0828.md](days/0828.md)（抵達日：含航班、機場交通連結與完整時間表）和 [0903.md](days/0903.md)（島波海道單車日：含交通表與備案）最能感受格式。
3. **[transportations/OKJ_OkayamaStation.md](transportations/OKJ_OkayamaStation.md)** — 交通指南範例：機場↔市區的利木津巴士班次、票價、乘車位置，討論中查證過一次就歸檔，不必重查。
4. **[assets/website_abstract.md](assets/website_abstract.md)** — Claude 整理的網站摘要：每個網站 3–5 條「對旅程有用的具體事實」，依交通／美食／購物／景點分類。
5. **[assets/reference_website.md](assets/reference_website.md)** — 使用者自行維護的參考連結索引，與上述摘要對應。
6. **[luggage_items.md](luggage_items.md)** — 行李清單，同樣由討論產出。

## 這個範例示範的工作流程

- 行程從粗到細：先定住宿基地（岡山 3 晚 → 尾道 5 晚），再逐日討論填入景點、時間表與備案
- 每次討論前 `/discuss-itinerary` 讀齊資料，討論後 `/update-itinerary` 同步檔案
- 查證過的網站經 `/save-website-abstract` 歸檔，知識隨討論累積
- 大原美術館週一公休 → 倉敷拆成兩次造訪，這類可行性問題由討論與 trip-reviewer 把關
