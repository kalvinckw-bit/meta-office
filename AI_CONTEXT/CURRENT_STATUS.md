# Live Project Status (Single Source of Truth)

## 1. Current Phase
- **Active Milestone**: Phase 1（自用 AI 部長版）已於 2026-08-27 結案，但 **2026-08-30 社長指示架構轉向**：拋棄 AI 部長，改建真人協作平台（100% 抄襲 MetaLife 的「真人」互動邏輯）。
- **Current Objective**: Phase 2 — 真人邀請系統。目前只有「打招呼」單向流程，需補齊「有空嗎」雙向確認、pre-call brief、WebRTC 真實連線、帳號系統。
- **Last `end`**: 尚未執行（本次為 `start` 後的進行中 session）。上一次正式 `end` 是 2026-08-27 by Claude (Desktop, Windows)。

## 2. Functional Verification Matrix
| Module / Feature | Status | Verified with Live Logs? | Notes |
| :--- | :--- | :--- | :--- |
| 真人版 `metaoffice.html`（v3.0） | Completed | **NOT verified on this machine** | 雲端 session 內瀏覽器測過移動/碰撞/邀請彈窗；本機檔案版本待社長開啟確認 |
| 在線狀態系統（online/away/offline） | Completed | Inferred | 邏輯已寫好，狀態資料目前是寫死的假資料（TEAM 陣列），非真實帳號 |
| 打招呼邀請流程（單向） | Completed | Inferred | 走近自動彈窗、接受/拒絕按鈕功能正常 |
| 「有空嗎」雙向確認流程 | **Not started** | No | 只有骨架，尚未實作「對方需先同意才進入」的等待機制 |
| Pre-call brief（通話前說明） | **Not started** | No | 尚未設計 UI |
| WebRTC 真實視訊/音訊 | **Not started** | No | 麥克風/鏡頭按鈕仍是 `alert()` stub |
| 真人帳號/登入系統 | **Not started** | No | 目前無法讓真人自己上線、離線、被邀請 |
| 圖形升級（漸層/陰影/狀態環） | Completed | Inferred | 已從像素風換成 Canvas 2D 向量漸層渲染 |
| ~~Cowork 外掛（6 位 AI 部長）~~ | Deprecated（待社長確認） | Yes（舊功能本身可動） | 部長 Skill 仍安裝在帳號內可用，但 `metaoffice.html` 已不再連結到它們；是否整個停用需社長決定 |
| 決策紀錄 localStorage | Completed（v2.0 殘留功能，v3.0 未搬過來） | Inferred | v3.0 尚未重新加入決策紀錄區塊 |
| 靜態託管上線 | Deployed | ✅ Live (2026-09-02 09:02 JST) | 已部署至 christykalvin.com/metaoffice.html；Firebase Hosting (christykalvin-web site)；兩個網域均 HTTP 200 |
| Git 版控 | **Blocked** | No | Cowork 橋接不給刪檔權限，git 無法運作；需社長手動 `git init`（見 TODO P0） |

## 2.1 Latest Deployment (2026-09-02)
- **Commit**: ChristyKalvinWeb `16676ea`
- **URL**: https://christykalvin.com/metaoffice.html （自訂域名）/ https://christykalvin-web.web.app/metaoffice.html （web.app）
- **Cache Policy**: `no-cache, no-store, must-revalidate` （避免看到舊畫面）
- **Verification**: 兩網域均返回 HTTP 200，metaoffice.html v3.0 已上線可存取

## 3. Active Blockers & Critical Notes
- **v3.0 是骨架，不是完整產品**：目前只做到「靠近會彈出打招呼邀請」。「有空嗎」的雙向同意、brief、真正視訊連線都還沒做。社長若要拿去給真人同事用，這些是硬性前提。
- **沒有真實帳號系統**：`TEAM` 陣列是寫死在程式碼裡的假資料（Alice/Bob/Carol/Dave/Eve）。要「招人進來」，需要先做登入/邀請連結/個人資料編輯，否則新同事無法真的出現在地圖上。
- **舊版已歸檔未刪除**：`docs/archive/metaoffice_v2.0_ai-ministers_20260830.html` 保留 AI 部長版本供對照，未刪除（AI 無刪檔權限）。
- **Cowork 六位部長技能去留未定**：`/ceo` `/cfo` `/cto` `/cmo` `/coo` `/advisor` 仍安裝在社長 Claude 帳號內可正常使用，只是 `metaoffice.html` 不再連結它們。若社長完全不需要 AI 意見了，需明確指示才會動手拆除/取消同步。
- **麥克風／鏡頭尚未實測**：`getUserMedia` 只在 https 環境可用，`file://` 下瀏覽器直接拒絕；v3.0 按鈕目前是 stub，尚未接回原本 v2.0 已寫好的授權邏輯。
- **網域尚未購買**：`metaboardroom.asia` 與 `metaboard.asia` 於 2026-08-27 查詢時可註冊，尚待社長決定。
