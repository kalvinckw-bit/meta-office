# Constitutional Project Decisions Registry (DECISIONS.md)

This document records permanent architectural, design, and policy decisions approved by the user.
**DECISIONS ARE PERMANENT AND CONSTITUTIONAL.** No AI may revert, modify, or re-debate approved decisions without explicit user instruction.

---

### Decision 001: Multi-AI Governance & Session Lifecycle
- **Date**: 2026-08-27
- **Status**: APPROVED
- **Context**: 專案橫跨多台機器（MacBook、Windows）與多個 AI 工具。
- **Rule**:
  1. All AIs must begin with `start` and conclude with `end`.
  2. Each AI maintains only its own designated file under `AI_CONTEXT/SESSIONS/`.
  3. `end` automatically commits and pushes session records and changes to Git remote.

### Decision 002: Architecture & Code Standards
- **Date**: 2026-08-27
- **Status**: APPROVED
- **Rule**: All source code must adhere strictly to the tech stack and guidelines defined in `PROJECT_OVERVIEW.md`.

### Decision 003: 零成本原則
- **Date**: 2026-08-27
- **Status**: APPROVED
- **Context**: 社長目前缺資金，VoiceOut 尚未證明留存。
- **Rule**: 不得引入需要付費的服務、API 或工具。任何提案都必須先給出零成本版本。唯一已核可的例外是網域註冊費（一年數百日圓量級）。

### Decision 004: 介面視覺語言 —— MetaLife 的世界 ＋ VoiceOut 的外殼
- **Date**: 2026-08-27
- **Status**: APPROVED
- **Context**: 社長多次指正：前兩版做成向量示意圖，完全不像參考對象。看到實際截圖後才確認關鍵是**16-bit 像素風**。
- **Rule**:
  1. **地圖世界**採像素風、亮色系：薰衣草磚牆、奶油色辦公桌、人字拼木地板、Q 版角色、彩色圓地毯當對話區。
  2. **介面外殼**（頂欄、成員一覽、工具列、彈出卡片）採 voiceout.asia 的實際 token：`#050505` 底、`#00E5FF` 主色、Orbitron 字體、直角無圓角。
  3. 六位部長各自綁定一個 VoiceOut 品牌色，不得混用。
  4. Canvas 一律 `imageSmoothingEnabled = false`，先在 1x 離屏畫布繪製再放大，確保像素銳利。

### Decision 005: 可以抄什麼、不可以抄什麼（對外販售前置條件）
- **Date**: 2026-08-27
- **Status**: APPROVED
- **Context**: 社長計畫未來開放其他公司購買方案。
- **Rule**:
  1. **可以沿用**：由上而下的 2D 地圖、走近自動連線、底部工具列、成員清單、小地圖、`名字@部門` 標籤 —— 這些是 Gather／oVice／ZEP／MetaLife 共通的品類慣例，無人可獨佔。
  2. **不得複製**：MetaLife 的地圖美術、傢俱貼圖、角色造型、配色、商標。本專案所有美術資產必須為自行繪製。
  3. 對外發布前必須完成一次美術資產自主性檢查。

### Decision 006: 麥克風與鏡頭採瀏覽器原生授權
- **Date**: 2026-08-27
- **Status**: APPROVED
- **Rule**: 一律使用 `navigator.mediaDevices.getUserMedia`，由瀏覽器自己跳授權視窗；使用者不同意就不開，且隨時可關。不得自建繞過授權的機制。已知限制：需 https，`file://` 下無法使用，程式須偵測並明白告知使用者。

---

### Decision: CK Holdings Group Unified Authentication & Cloud Architecture (集團一號通與中央雲端架構)
- **Status**: APPROVED
- **Date**: 2026-08-29
- **Context**: CK Holdings operates multiple brand portals and services (Voice Out, Sougu / Crosspath, ChristyKalvin, etc.). To prevent user registration fatigue and simplify cross-brand infrastructure, all services must share a single Master Authentication system.
- **Rule**:
  1. **Master Project Identity**: The Firebase Master Project is `CK Holdings` (Project ID: `voiceout-asia`).
  2. **Single Sign-On (One Auth)**: All frontend websites and apps (`voiceout.asia`, `sougu.online`, `christykalvin.com`, etc.) share the same Firebase Authentication instance. Users register once and maintain a consistent UID across the entire group.
  3. **Multi-Database Partitioning**: Business data for distinct brands is physically isolated using dedicated Firestore Database instances under the same Master Project:
     - `(default)`: Voice Out Web / Mobile App
     - `sougu-db`: Sougu (Crosspath)
     - `christykalvin-db`: ChristyKalvin Official Web
     - `creditcard`: Credit Card / Billing sub-system
     - `dead-man-switch`: Dead-Man-Switch sub-system
  4. **Multi-Site Hosting**: Each brand domain is mapped as an independent Hosting site target within the Master Project.

---

### Decision: AI Proactive Autonomous Execution Policy (AI 主動自主執行原則 / 禁止把 AI 能做的事推給用戶)
- **Status**: APPROVED
- **Date**: 2026-08-29
- **Context**: 用戶聘請並使用 AI 是為了極大化自動化與研發效率，而不是接收 AI 的操作指示自行手動操作。過去多次發生 AI 明明具備 CLI / 工具 / 腳本執行能力，卻習慣性列出步驟指導用戶去後台手動點擊或手動修改，嚴重違反專案效率原則。
- **Constitutional Rules (憲法級硬性準則)**:
  1. **AI 優先直接執行（Execute Directly First）**：凡是 AI 擁有工具權限能做的事（包含但不限於 Firebase CLI / 雲端資源開通、資料庫建立、環境變數配置、腳本執行、檔案修改、代碼生成、Git 自動化），AI **必須直接調用工具自主完成**，嚴禁發出「請您到後台手動點擊」、「請您自行建立」等指示。
  2. **僅限不可替代之真人行為才要求用戶參與（Human-Only Escalation Only）**：只有在牽涉「真人雙重認證（2FA/SMS 驗證碼）」、「外部金流實際付款扣款」、「重大商業策略決策確認」等物理上 AI 絕對無法執行的情況下，才允許請求用戶操作。
  3. **拒絕給用戶出作業（No Homework for User）**：AI 的責任是「徹底解決問題並交付成果」，做完後主動呈報具體執行細節與檔案路徑，而非把任務分解後丟回給用戶手動執行。

---

### Decision: CK Holdings Maximum User Telemetry & Device Intelligence Policy (全方位用戶設備與環境情報收集準則)
- **Status**: APPROVED
- **Date**: 2026-08-29
- **Context**: 為了防範集團旗下各平台遭到詐騙、濫用、盜號、惡意機器人攻擊，並掌握全方位業務與用戶設備分佈情報，所有 CK Holdings 旗下網站與應用程式必須在用戶登入與訪問時，自動、無感、最大化地採集所有可獲取之客戶端情報。
- **Constitutional Rules (憲法級硬性準則)**:
  1. **全方位情報採集範圍（Maximum Obtainable Scope）**：
     - **網路與位置**：真實公網 IP (IPv4/IPv6)、國家、城市、地區、時區、ISP 電信商、連線類型 (WiFi/5G/4G)、下載頻寬估算、延遲 (RTT)。
     - **設備與硬體**：設備類型 (Mobile/Tablet/Desktop)、作業系統及版本 (iOS/Android/Win/Mac)、瀏覽器及核心版本、螢幕解析度、可用解析度、色彩深度、像素比、CPU 核心數、記憶體估算 (RAM GB)、觸控點數支援。
     - **環境與語系**：系統語言、偏好語言清單、用戶時區、與 UTC 時差、深色/淺色主題偏好、Cookies/Storage 支援狀態。
     - **行為與來源**：訪問網域 (siteId)、當前 URL、來源網址 (Referrer / UTM)、時間戳記 (ISO/Timestamp)、UID 與 Email。
  2. **靜默自動寫入資料庫（Silent Persistence）**：
     - 每次用戶登入或啟動應用時，前端自動將最新快照更新至 users/{uid} (包含 last_telemetry, last_ip, last_device, last_city, last_country, last_login_at)。
     - 同步追加寫入至子集合 users/{uid}/telemetry_logs/{logId} 作為完整歷史審計日誌。
  3. **非阻塞與容錯原則（Graceful Fallback）**：
     - 能收集到的全部收集，若特定瀏覽器沙盒或隱私限制無法取得某欄位，則優雅降級 (Fallback)，絕對不可阻礙用戶正常使用介面。

---

### Decision: 拋棄 AI 部長架構，改為真人協作平台 (Real-People-Only Pivot)
- **Status**: APPROVED
- **Date**: 2026-08-30
- **Context**: 社長明確指示：「不是，我不要 AI 了，我要 100% 抄襲 metalife 的真人，現在雖然還沒有人，可是我會招人進來！」六位 AI 部長（CEO/CFO/CTO/CMO/COO/顧問）走近問答的模式，從產品核心定位上被取代為「真人同事走近彼此、互相邀請、通話前先 brief」的協作邏輯。
- **Constitutional Rules**:
  1. **`metaoffice.html` 的桌位不再代表 AI 部長**：所有桌位是真人團隊成員的席位，未來由社長招募真人填入，程式碼中的 `TEAM` 陣列即為席位資料來源。
  2. **互動模式改為邀請制，非問答制**：不再是「走近部長 → 打字問問題 → AI 回答」，而是「走近同事 → 系統自動發出打招呼邀請 → 對方需回應 → 若要深聊需雙方都同意（有空嗎流程）→ 進入 brief → 才進通話」。
  3. **圖形不得再用像素風**：社長原話「太 2D 了，比 metalife 還差」——往後此專案的視覺方向是漸層/陰影/立體渲染，不回頭做像素藝術。
  4. **Cowork 六位部長 Skill 保留但脫鉤**：`/ceo` `/cfo` 等技能繼續安裝在社長帳號內（可能仍有其他用途，例如純文字諮詢），但不再是 `metaoffice.html` 的核心互動對象。是否完全移除需社長另外明確指示，AI 不得自行假設要刪除已安裝的技能。
  5. **v2.0（AI 部長版）保留歸檔，不刪除**：供對照與可能的回退需求，存放於 `docs/archive/`。
- **Consequence**: TODO.md、CURRENT_STATUS.md 的既有任務（网域、https、麥克風/鏡頭實測）順位往後，優先權讓給「補完真人邀請流程」與「真人帳號系統」。

---

### Decision: Mandatory Automatic Git Pull on Start & Git Push on End (開局必 Pull 收工必 Push 鋼鐵憲法)
- **Status**: APPROVED & MANDATORY
- **Date**: 2026-09-02
- **Context**: 針對部分 AI 誤以為 AI_CONTEXT 僅是本機留言板、不需要自動同步雲端的怠惰誤解，集團特此頒布鋼鐵憲法。
- **Constitutional Rules (憲法級硬性準則)**:
  1. **開局必 Pull（Mandatory Pull on `start`）**：
     - 每次使用者輸入 `start` 或 AI 開始新 Session 時，AI **必須首先自動執行 `git pull --rebase`**，將 GitHub 遠端最新進度拉取至本機。嚴禁以「未要求同步雲端」為由略過！
  2. **收工必 Push（Mandatory Push on `end`）**：
     - 每次使用者輸入 `end` 或任務告一段落時，AI **必須自動執行 `git add -A`、`git commit` 並立即 `git push` 至 GitHub 遠端儲存庫**。
     - **嚴禁留給使用者手動執行！嚴禁宣稱『AI_CONTEXT 沒有要求 push』！**
  3. **雙重同步架構定位（OneDrive + GitHub）**：
     - OneDrive 負責跨裝置（Windows ⟷ Mac）檔案即時傳輸。
     - GitHub 負責版本歷史與多 AI 程式碼同步。
     - **任何 AI 結束工作時未執行 `git push`，即視為嚴重失職與交接漏洞！**
