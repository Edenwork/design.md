# AFS Suite 平台設計系統與維運實務架構規範說明書 (Design & Operations Specification)

---

## 專案基本資訊 (Meta Information)

| 屬性 | 設定值 |
| --- | --- |
| **Version** | v1.0.0-Release |
| **Name** | AFS-Suite-Design-Operations-Specification |
| **Description** | 本文件為台智雲 AFS Suite (AI Foundry Service Suite) 全棧主權 AI 平台之 UI/UX 設計系統與前端維運工程規範。旨在融合「企業主權 AI (Sovereign AI)」架構與「專業極簡主義」視覺語言，建立從算力、模型管理到多 Agent 協作平台的標準化前端開發組件與維運防呆指引。 |
| **Author** | Eden |

---

## 一、 設計哲學與視覺風格 (Design Philosophy & Visual Style)

AFS Suite 定位為國家級算力延伸之企業級主權 AI 基礎設施。整體介面依循**專業極簡主義 (Professional Minimalism)**，視覺軸線以純白、深灰、純黑為基底，並引入代表安全、穩重與科技控制權的「**專業藍 (Professional Blue)**」作為系統核心語意強調色。

### 1. 全棧架構色彩系統 (Color Palette Table)

為了清晰隔離「一般企業應用」、「多租戶/管理者控制」以及「高風險警示」之操作語境，定義以下全域 CSS 變數：

| 變數名稱 / 類別 | 色碼 (HEX) | 適用場景與設計說明 |
| --- | --- | --- |
| `--content-area-bg` | `#F9FBFF` | 全域主內容區背景：輕盈、帶有極微量藍色調的冷白，降低長時間監控的眼部疲勞。 |
| `--card-bg` | `#FFFFFF` | 核心功能方塊、FAQ 摺疊面板、模型卡片背景。 |
| `--primary-text` | `#000000` | 主要文字、主標題（純黑），確保最高對比度度與可讀性。 |
| `--secondary-text` | `#636363` | 說明文字、微小時間戳記、審計日誌次要內文（中灰）。 |
| `--primary-brand` | `#222222` | 主色/核心強調色，用於頂層導覽與基礎按鈕。 |
| `--sovereign-blue` | `#23237B` | 系統核心語意色（專業藍）：象徵「主權控制權」，用於核心架構強調、核心進度條與通過驗證之標籤。 |
| `--error-color` | `#CA0729` | 錯誤提示主色（如外部平台綁定警告、算力超載、資安護欄觸發）。 |
| `--second-error-color` | `#AD001D` | 錯誤提示次要色/深紅色。 |

### 2. 核心視覺資產規範 (Visual Asset Standards)

* **標誌與圖示規範 (Iconography):**
    * 系統圖示優先採用高解析度、可縮放且不失真的 **SVG** 格式（如自訂資產路徑 `/images/logo/favicon.ico`），減少傳統點陣圖資源之請求負擔。
      
* **邊框與陰影 (Borders & Shadows):**
    * 基礎卡片、FAQ 面板、場景方塊之圓角統一規範為 `border-radius: 12px` (俐落微圓角)。
    * 標準卡片陰影使用輕量、細緻的投影：`box-shadow: 0px 3px 5px rgba(0, 0, 0, 0.05)`。
    * 滑過狀態 (`:hover`) 僅允許微妙的陰影加深：`box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08)`，**禁止使用**刺眼的霓虹或彩色漸層。

---

## 二、 全棧分層前端組件與排版規範 (Tiered UI Component & Typography)

### 1. 字體級距表 (Typography Hierarchy)
全站字體以 `Noto Sans TC` 為繁體中文核心，在 Mac OS 環境下客製化整合 `-apple-system` 與 `BlinkMacSystemFont`，數字則強制映射 `Roboto`。

| 標籤 / Class | 級距 (Size) | 字重 (Weight) | 行高 (Line Height) | 台灣專業語意與對應場景 (Comments) |
| --- | --- | --- | --- | --- |
| `h1` / `.fs-1` | `40pt` (2.5rem) | 700 (Bold) | 1.20 | 頂層頁面大型主視覺標題（如「打造安全可控的企業主權 AI」） |
| `h2` / `.fs-2` | `32pt` (2.0rem) | 700 (Bold) | 1.20 | 核心產品線標題（如 AFS AI Fabric, AFS AI Hub, AFS Claws） |
| `h3` / `.fs-3` | `28pt` | 600 (Semi-Bold) | 1.20 | 組件區塊中型標題（如「三大特色」、「FAQ」） |
| `h4` / `.fs-4` | `24pt` (1.5rem) | 700 (Bold) | 1.35 | 麵包屑導覽 (Breadcrumb) 與卡片內核心技術指標標題 |
| `p` / `h6` / `.fs-6` | `16pt` (1.0rem) | 400 (Regular) | 1.80 | 核心內文文字、FAQ 回答內文（寬鬆行高確保長文閱讀舒適度） |
| `.fs-7` | `14pt` (0.875rem) | 400 (Regular) | 1.40 | 側邊欄導覽文字、客製化參數輔助說明標籤、表單說明文字 (`.form-text`) |
| `small` / `body-sm` | `12pt` | 400 (Regular) | 1.30 | 審計日誌時間戳記、算力使用量微小註解、版權宣告 |

---

### 2. 四大核心層級模組化 UI 表現

架構分層 (Architecture Tier),核心前端組件與維運實作範疇 (Core Components & Implementation)
1. AI 應用服務層(AFS Claws Panel),支援多 Agent 工作流配置面板、檢索增強生成 (RAG) 節點、多模型路由選單。
2. AI 平台服務層(Fabric 多租戶面板 / Hub 快速部署卡片),企業控制與治理核心：多部門/多租戶控制項、模型一鍵部署開關。
3. 信任與資料服務層(Security Guardrails Display),權限控管狀態、安全沙盒隔離提示、行為審計流水線日誌。
4. 主權算力服務層(Sovereign Compute Monitor),GPU 雲端資源看板、大型 AIHPC 算力調度可視化 (ECharts Stacked Bar)。
   

#### A. AFS Claws 營運面板 (多 Agent 協作與路由)
* **深度思考區塊 (`.btn-reasoning-collapse`):** 針對具備推理能力之模型（Reasoning Model），其思考歷程必須預設或提供手動折疊面板。左側配置微小灰色裝飾線（`border-left: 2px solid #ccc`），內文變更為次要輔助灰，與正式回覆做出明確視覺區隔。
* **整置點擊群組卡片 (`.card-add-model-container`):** 使用者點擊模型卡片內任意非控制區域時，須自動觸發內嵌之單選按鈕 (`.radio-btn`) 進行選取切換。JavaScript 事件處理中必須明確排除具備 `.disabled` 類別之元素，防止唯讀或無效狀態之卡片被誤點擊。
* **多模型路由選單:** 扁平化 Dropdown 樣式，點擊互動元素必須明確宣告 `cursor: pointer;`。

#### B. AFS AI Fabric / Hub 部署與控制項
* **雙模側邊欄佈局 (Dual-Mode Sidebar):**
    * 區分一般企業模式（輕量淺藍灰背景 `--sidebar-bg: #e6ebf7`）與**高階 Fabric 管理者模式（沉穩炭灰背景 `--admin-sidebar-bg-color: #373737`）**，明確隔離操作語境。
    * 展開狀態固定寬度 `304px`，收合狀態 (`.collapsed`) 變更為 `80px` 並隱藏所有文字標籤。設定 `transition: width 0.35s ease`。
    * **Tooltip 整合:** 收合後為防止無法辨識，導覽項目強制整合 `data-bs-toggle="tooltip"`，設定於下方顯示提示。

#### C. FAQ 交互與交付路徑引導組件
* **FAQ 摺疊面板 (Accordion Component):**
    * 基於網頁一鍵部署與分階段導入（如：只用算力、只用模型治理、或只用 Agent）之商業邏輯，FAQ 面板點擊時需呈現平滑摺疊動畫。
    * **三步驟導引區塊:** 前端採用緊湊、線性的步驟條 (Stepper UI)，引導使用者從「需求對接 ➔ 場景確認 ➔ 快速部署」完成商業閉環，步驟按鈕隨附客製化懸浮回饋。

---

## 三、 維運安全與前端防呆規範 (Operations & Anti-Patterns)

為了確保 AFS Suite 平台在實際營運、客戶展示與系統維護時的高穩定性，前端工程與維運應嚴格執行以下防呆雷區限制：

### 1. 阻斷式與非阻斷式通知規範
* **嚴禁使用瀏覽器預設 Alert 彈窗:** 系統執行特定維運或業務動作（如複製 API Key 成功、表單預約送出、模型部署成功等通知），**絕對禁止**調用原生的 `window.alert()`。
* **客製化 Snackbar 提示組件:** 必須統一使用自訂的 **Snackbar / Toast 通知組件**。當事件觸發時顯示，並設定為 **5 秒後自動滑動或淡出消失**，提供流暢的非阻斷式使用者體驗。

### 2. 彈出式視窗樣式與技術規範 (Modal Specification)
* **嚴禁使用 HTML5 原生 `<dialog>` 標籤:** 為了確保跨瀏覽器樣式的高度客製化、控制權與資安組件相容性，一律採用結構清晰的傳統 `<div>` 配合 Bootstrap Modal 機制實作。
* **控制面板內距控制:** `modal-content` 設定最小寬度 `min-width: 585px`；面板內距（`modal-body`, `modal-footer`）統一使用百分比進行精確之呼吸感控制：`padding: 4% 8% !important;`。
* **雙向綁定防呆:** 參數調節表單（如 Top-P、Temperature 等）必須由 `input[type="range"]` 與 `input[type="number"]` 共同組成，維持數值雙向同步與格式驗證，並提供「重置參數」按鈕。

### 3. 表單與密碼安全防護
* **金鑰與密碼可視性切換 (Password Visibility Toggle):** 對於涉及平台金鑰（Secret Key）或敏感密碼之輸入框，右側隨附切換按鈕，透過操作 DOM 的 `type` 屬性於 `password` 與 `text` 間進行動態轉換，並同步更新 Font Awesome 圖示 (`fa-eye` 與 `fa-eye-slash`)。
* **提示訊息區塊 (`.error-message`):** 使用漸層背景 (`linear-gradient(135deg, #e0f7fa, #f8e1e9)`) 搭配前置 Unicode ⓘ 圖示，以溫和不突兀的方式提示配置錯誤。

---

## 四、 技術標準與工程代碼規範 (Code & Terminology Standards)

1.  **CSS 變數與命名架構 (BEM):**
    * 元件與樣式命名優先遵循 **BEM (Block, Element, Modifier)** 風格（如 `.claws-agent-card`、`.fabric-tenant-container`、`.btn-modal-default`）。
    * 網頁佈局結構應妥善處理寬度邊界與 `box-sizing: border-box`，防止因 Padding 或 Border 導致的排版溢出 (Overflow)。
2.  **專業語彙規範 (Taiwan Region Context):**
    * 代碼註解、UI 介面文字與系統提示訊息一律使用台灣在地技術與商業術語。
    * **嚴禁使用** 非在地語彙如「`自定義`」、「`缺省`」、「`菜單`」。
    * **一律使用** 「**`客製化`**」或「**`自訂`**」（對應參數調整）、「**`預設值`**」（對應 Default 參數）、「**`選單`**」（對應 Dropdown UI）。
3.  **互動轉場與過渡標準:**
    * 滑過 (Hover) 與聚焦 (Focus) 狀態必須加上 `transition: all 0.2s ease-in-out;` (過渡時間嚴格控制在 150ms - 300ms 之間)，確保極致平滑的互動反饋。
