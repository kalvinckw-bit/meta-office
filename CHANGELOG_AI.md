# AI Modification Changelog

All material changes to codebase architecture, major features, or project configuration made by AI agents are recorded here chronologically.

---

### [Initial Setup] - 2026-08-27
- **Author**: Master AI Context Framework
- **Changes**: Initialized standard enterprise Multi-AI Context governance framework.

### [v0.1 — Cowork 外掛] - 2026-08-26
- **Author**: Claude (Cowork, Windows)
- **Changes**: 建立 `voiceout-boardroom` 外掛：六位 AI 部長 Skill（CEO/CFO/CTO/CMO/COO/顧問）＋ `board-meeting` 全體會議協調器 ＋ 共用業務背景 `context/voiceout-context.md`。每位部長設定明確的預設反對立場，避免一群只會附和的顧問。

### [v0.2 — 介面第一版（已淘汰）] - 2026-08-26
- **Author**: Claude (Cowork, Windows)
- **Changes**: 產出可走動的向量式 2D 地圖。**社長判定不合格** —— 看起來是示意圖，不是辦公室。

### [v0.3 — 介面第二版（已淘汰）] - 2026-08-27
- **Author**: Claude (Cowork, Windows)
- **Changes**: 加入卡通角色、玻璃會議室、視訊泡泡。**社長再次判定不像** —— 仍是向量風格。
- **Root Cause**: 雲端環境連不上 metalife.co.jp，WebFetch 會剝除圖片，Chrome 外掛斷線 —— 前兩版皆為「照文字描述盲做」。

### [v1.0 — 像素風重製] - 2026-08-27
- **Author**: Claude (Cowork, Windows)
- **Changes**: 社長提供實際截圖後重製。改為真正的 16-bit 像素風：離屏 1x 畫布 + 最近鄰放大、薰衣草磚牆、人字拼木地板、奶油色辦公桌、Q 版角色、隔板、綠色圓地毯對話區、頂部視訊格列（`名字@部門` + 綠色麥克風圖示）、雙擊瞬移、走近自動連線、麥克風／鏡頭原生授權、表情反應、縮放跟隨鏡頭、小地圖。
- **Verification**: Playwright 實跑無 console error；靠近單人顯示 2 格、站上綠地毯顯示 7 格。

### [專案結構化] - 2026-08-27
- **Author**: Claude (Cowork, Windows)
- **Changes**: 套用 Master AI Context Template；外掛原始碼移入 `plugin/`；舊副本移入 `_to_delete/`（AI 無刪檔權限，待社長手動清除）。

### [v1.1 — 對話框改為 RPG 風格] - 2026-08-28
- **Author**: Claude (Cowork, Windows)
- **Changes**: 社長指出「跟部長對話」的彈出視窗長得像網頁表單，沒有 game 感。拆掉置中 modal 卡片，改成底部錨定的 RPG 對話框（頭像框＋名牌＋台詞＋快速提問清單＋輸入行），視覺對齊 MetaLife 截圖裡的 NPC 對話語彙。功能不變：走近仍自動開啟、快速提問點了會填入輸入框、按 ENTER／傳送鍵複製指令到剪貼簿讓社長貼回 Cowork 對話框（純前端頁面無法直接連真的 Claude，這是零成本前提下唯一的橋接方式，已向社長說明原因）。
- **Verification**: Playwright 實跑點擊 CEO 桌子 → 對話框開啟、名牌無重複文字、點快速提問正確填入輸入框、傳送鍵正確觸發複製與「已送出！」提示，console 無 JS error。

### [v2.0 — 辦公室擴建 + 完整工具列 + 預留員工席] - 2026-08-28
- **Author**: Claude (Cowork, Windows)
- **社長指示**: (1) 將來要聘請員工，位子先做起來；(2) 底部工具列補齊；(3) 辦公室該有的東西都放進去（鋼琴這類不必要的先略過）；(4) 目標接近 100% 像 MetaLife。
- **Changes**:
  - 地圖由 44×28 擴為 **52×34**（704×448 → 832×544），空出真正的分區。
  - 新增分區：**休息區**（三人沙發 ×2、扶手椅 ×2、茶几、人字拼木地板）、**茶水間**（流理台＋水槽＋咖啡機＋熱水壺＋杯子、冰箱、高腳桌＋吧凳、地磚）、**團隊席**（地毯帶）、**接待區**（接待櫃台＋簽到板＋電話、等候長椅、玄關地墊＋走道）、**收納角**（影印機、檔案櫃）、**書櫃角**（雙層彩色書櫃、紙箱）。
  - 牆面新增：白板（含長條圖）、簡報螢幕、**兩扇窗（城市天際線＋雲）**、壁掛時鐘、加高的伺服器機櫃。
  - **四張空桌（空位 1–4）預留給真人同事**：灰階待機外觀、虛線幽靈名牌 `空位 N@待入職`、右側名單新增 OPEN SEATS 區塊；點下去會開對話框並把問題導向 CFO（請人＝花錢）。
  - 視訊格重做成參考圖的樣式：白色名牌在上、**圓形像素頭像徽章咬住左上角**、影像在下、綠色麥克風圓鈕、舉手圖示；七格時自動縮小成單排不換行（`.tiles.many`）。
  - 底部工具列重做成「圖示在上、文字在下」：麥克風／鏡頭／**分享畫面**（`getDisplayMedia`，另開一格較寬的螢幕分享格）／**舉手**／**表情**（八款，彈出式選盤）／回入口／開全體會議／縮放／**離開**（紅色，一鍵關掉所有裝置並走回入口）。
- **Verification**: Playwright 實跑 —— 初始畫面、走上綠地毯（7 格單排不換行）、舉手、表情選盤、點空桌開對話框、離開鍵歸零，全程 console 無 error。修掉一個真實 bug：表情選盤原本被 RPG 對話框蓋住（z-index 衝突）。
- **自評**: 約 85–88% 神似。仍有差距的地方：部長是 AI，視訊格內無法有真人影像（只能放頭像）；無真正多人 WebRTC（要伺服器＝要花錢）；美術為自繪，非直接沿用對方素材。

### [v3.0 — 架構轉向：真人協作取代 AI 部長] - 2026-08-30
- **Author**: Claude (Desktop, Windows)
- **社長指示**: 「不是，我不要 AI 了，我要 100% 抄襲 metalife 的真人，現在雖然還沒有人，可是我會招人進來！接近之後會問我，要打招呼？要聊天？」「對方收到我的打招呼，會問要打招呼？」「如果我跟對方問，有空嗎？對方就要顯示要不要接受我的聊天，我們先 brief。」「然後就是圖案，能否真實一點？太 2D 了，比 metalife 還差！」
- **Changes**:
  - **拆除 AI 部長系統**：六位部長（CEO/CFO/CTO/CMO/COO/顧問）的桌子、對話框、立場文字、快速提問全部移除。`metaoffice.html` 不再是「走近 AI 問問題」的工具。
  - **改為真人成員系統**：`TEAM` 陣列取代 `POD`，每位成員有 `name`、`role`、`status`（online/away/offline）、世界座標、頭像色。目前 5 個示範席位，社長招人後可直接擴充陣列。
  - **在線狀態指示**：綠色 online（可互動）／橙色 away（可邀但人不在）／灰色 offline（無法互動，踏近無反應）。
  - **邀請流程（第一版）**：走近在線成員（距離 < 140px）自動彈出邀請面板「XXX 向你打招呼，你要回應嗎？」→ 接受／拒絕。這是「打招呼」流程的骨架；「有空嗎」雙向確認 + brief 前置說明尚未實作（見下方待辦）。
  - **圖形從像素風換成漸層寫實風**：畫布從離屏 1x 像素放大改為直接向量繪圖（Canvas 2D API），加入放射漸層頭像、狀態環、地面橢圓陰影、狀態指示光點、拖曳導航虛線。社長原話「太 2D 了，比 metalife 還差」——這版換掉整個渲染邏輯，不再是像素風。
  - 舊版（v2.0，AI 部長 + 像素風）已歸檔至 `docs/archive/metaoffice_v2.0_ai-ministers_20260830.html`，未刪除，供對照。
- **Verification**: 尚未在此裝置用 Playwright/瀏覽器實跑（雲端 session 內已用瀏覽器測過移動/碰撞/邀請彈窗，本機檔案版本待社長開啟確認）。**[Inferred from code, not yet verified on this machine]**
- **未完成（見 TODO.md P0）**：
  1. 「有空嗎」雙向確認流程（目前只有單向打招呼，未做「對方要先同意才進入」的邀請-等待-回應機制）。
  2. Pre-call brief 輸入框（通話前簡短說明想聊什麼）。
  3. WebRTC 真實視訊/音訊連線（目前麥克風/鏡頭按鈕仍是 stub `alert()`）。
  4. 真人帳號系統（目前 TEAM 是寫死在程式碼裡的假資料，無登入、無邀請連結、無法讓真人自己上線/離線）。
  5. Cowork 六位部長技能（`/ceo` `/cfo` 等）是否要一併停用或保留作為「AI 顧問」附加功能，尚未定案，需社長決定。
