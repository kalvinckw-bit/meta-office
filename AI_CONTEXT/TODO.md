# Project Task Backlog & Priorities

## P0: Immediate Priority (真人協作平台骨架補完 — 2026-08-30 架構轉向後新排序)
- [ ] **「有空嗎」雙向確認流程**：目前只有單向打招呼，需補上「A 邀請 B → B 看到邀請 → B 接受/拒絕 → A 即時收到結果」的雙向機制。純前端無後端目前無法跨瀏覽器同步，需先決定：Firebase Realtime DB／Firestore，或先用同機模擬雙人測試。
- [ ] **Pre-call brief 介面**：接受邀請後，通話開始前，加一個簡短輸入框「你想聊什麼？」，雙方確認後才進通話。
- [ ] **真人帳號系統雛形**：目前 `TEAM` 是寫死假資料。至少要有：登入（或邀請連結）、暱稱/頭像設定、上線狀態自己可切換（online/away/offline），否則社長招來的真人無法真的出現在地圖上。
- [ ] **決定 Cowork 六位部長技能去留**：`/ceo` `/cfo` `/cto` `/cmo` `/coo` `/advisor` 仍在帳號內可用，但已與 `metaoffice.html` 脫鉤。社長需明確表態：完全不要了 → 才動手停用同步；或保留作為純文字諮詢工具。

## P1: High Priority
- [ ] WebRTC 真實視訊/音訊連線（目前麥克風/鏡頭按鈕是 stub）。需要信令伺服器（Firebase Realtime 或 Socket.io），會產生持續性成本，需社長核准預算方向。
- [ ] 把麥克風/鏡頭的原生授權邏輯（v2.0 已寫好）搬回 v3.0（v3.0 目前尚未接回）。
- [ ] **在專案資料夾跑一次 `git init && git add . && git commit`** —— AI 在 Cowork 橋接下沒有刪檔權限，git 無法運作，必須由社長手動起頭。
- [ ] 確認 `_to_delete/` 內容確實是舊副本，然後整個資料夾刪掉（AI 沒有刪檔權限，需社長手動）。

## P2: Backlog & Enhancements
- [ ] **【待社長購買域名】** 部署 `metaoffice.html` 到 `ck-holdings.com.my`（社長另外購買，2026-09-02 尚未下單）。需配置 Firebase Hosting site、更新 DNS、驗證 https 下麥克風/鏡頭授權。目前暫保持本機測試狀態，不急於上線。
- [ ] ~~決定是否購買網域：`metaboardroom.asia`（首選）／`metaboard.asia`（備選）。~~ 已由社長決定用 `ck-holdings.com.my`。
- [ ] 決策紀錄功能（v2.0 有 localStorage 版本）尚未搬到 v3.0，需重新設計成「協作記錄」而非「AI 會議決策」的語境。
- [ ] 地圖編輯器：讓社長自己擺桌子、改樓層、加成員。
- [ ] 手機觸控走位優化。
- [ ] v3.0 圖形持續打磨：目前是「向量漸層」，離 MetaLife 的完整立體/材質感還有距離，可視社長回饋再迭代。

## CK Holdings 集團雲端基礎設施與網域生命週期維護 (Domain & Cloud Lifecycle TODO)
- [x] 2026-08-29: 完成 CK Holdings Master Firebase 專案一號通 (One-Auth) 授權網域配置 (`voiceout.asia`, `sougu.online`, `christykalvin.com`)。
- [x] 2026-08-29: 透過 CLI 建立專屬獨立 Firestore 資料庫實例：`sougu-db`、`christykalvin-db`、`creditcard`、`dead-man-switch`。
- [x] 2026-08-29: 建立 Firebase Multi-Site Hosting 站點目標 (`sougu-online`, `christykalvin-web`, `voiceout-asia`) 並綁定本地 `.firebaserc` / `firebase.json`。
- [x] 2026-08-29: 清理 `(default)` 資料庫中非 VoiceOut 殘留集合 (`cc_users`, `jpcc_users`)。
- [ ] **【重要 DNS 維護】Cloudflare DNS 保持灰色雲朵（DNS Only 模式）**：
  - 確保 `christykalvin.com`、`sougu.online` 等自訂網域在 Cloudflare 上的 `A` 記錄維持 **DNS Only (灰色雲朵 ☁️)**，確保 Google Firebase 自動 SSL 憑證簽發與續簽 100% 暢通不被攔截。
- [ ] **【2027 網域自動扣款防禦】解除 GMO (お名前.com) 冗餘網域自動續費**：
  - 在 お名前.com 後台「ドメイン自動更新設定」中，將非核心網域 (`voiceout.click`, `voiceout.help`, `voiceout.online`, `ck-japan.shop`, `ck-japan.net`) 設定為「解除自動更新」，避免 2027 年產生無謂扣款。
- [ ] **【2027 網域續約/轉移準備 (Domain Transfer to Cloudflare)】**：
  - 2027/01/15 前：`voiceout.asia` 評估無痛轉移至 Cloudflare Registrar 以批發成本價 ($9.77/yr) 永久續費。
  - 2027/04/14 ~ 2027/08/27 前：`christykalvin.com` 與 `sougu.online` 視情況由 Cloudflare 承接續約。
