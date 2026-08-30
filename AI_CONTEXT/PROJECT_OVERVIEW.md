# Project Overview & Architecture Map

## 1. Project Summary
- **Project Name**: Meta Office (產品代號：訊號指揮室 / VoiceOut Executive Space)
- **Core Purpose**: 給沒有合夥人的創辦人一組 AI 高管團隊。六位 AI 部長（CEO/CFO/CTO/CMO/COO/顧問）常駐在 Cowork 裡，可單獨諮詢或召開全體會議；另有一個 MetaLife 風格的 2D 像素辦公室介面，走到誰面前就「自動連線」拿到對應指令。
- **Primary Tech Stack**: 單檔 HTML + Canvas 2D（無框架、無建置流程）；Cowork Plugin（Markdown SKILL.md）
- **Target Platforms**: Web（桌機與行動瀏覽器）＋ Claude Cowork 外掛
- **Business Owner**: CK（社長）。母事業為 VoiceOut（voiceout.asia）。
- **Commercial Intent**: 目前自用；未來計畫開放給其他公司訂閱方案。

## 2. Directory Structure & Key Modules
```text
Meta Office/
├── metaoffice.html        # 2D 像素辦公室介面（單一檔案，直接用瀏覽器開）
├── plugin/                # Cowork 外掛原始碼（打包成 .plugin 後安裝）
│   ├── .claude-plugin/
│   │   └── plugin.json    # 外掛清單
│   ├── context/
│   │   └── voiceout-context.md   # 六位部長共用的業務背景（改這一份就好）
│   ├── skills/            # 七個 Skill：ceo cfo cto cmo coo advisor board-meeting
│   └── README.md
├── docs/                  # 設計參考與筆記
├── AI_CONTEXT/            # Multi-AI SSoT 治理框架
└── _to_delete/            # 重組前的舊副本，確認無誤後可整個刪除
```

## 3. Build, Run & Verification Commands
- **開啟介面**: 直接用瀏覽器打開 `metaoffice.html`（無需安裝、無需伺服器）
- **打包外掛**: `cd plugin && zip -r ../voiceout-boardroom.plugin .`
- **安裝外掛**: 在 Cowork 開啟該 `.plugin` 檔 → 按「安裝」
- **驗證方式**: 手動 —— 走位／碰撞／自動連線／視訊格／`/ceo` 等指令是否觸發
- **Deploy Command**: 尚未設定（規劃：Cloudflare Pages 靜態託管）

## 4. Key Architectural Boundaries
- `metaoffice.html` **必須維持單一自足檔案**：所有 CSS/JS 內嵌，唯一外部資源是 Google Fonts。
- 業務背景只放在 `plugin/context/voiceout-context.md` 一處；六位部長共用，不得各自複製一份。
- 決策紀錄存在瀏覽器 `localStorage`，屬**單機單瀏覽器**資料，不跨裝置、不上傳。
- 麥克風／鏡頭走瀏覽器原生 `getUserMedia` 授權；**需要 https**，`file://` 下會被瀏覽器擋掉。
- 不引入任何付費服務或外部 API（社長明確要求零成本）。
