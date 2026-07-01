# AI 應用平台前端設計與架構規範說明書 V2 (Design Specification)

version: alpha
name: Platform-Design-Typography
description: "基於專業極簡主義（Professional Minimalism）所制定的字體與排版系統。以 Noto Sans TC 為繁體中文通用核心，並在數字與特定硬體環境下客製化整合 Roboto、-apple-system 與 BlinkMacSystemFont，確保在 Mac OS 與各系統語境下皆能呈現極致流暢、穩重且現代化的黑白技術感排版。"

typography:
  h1:
    fontFamily: "Noto Sans TC, -apple-system, Roboto, sans-serif"
    fontSize: 40pt
    fontWeight: 700
    lineHeight: 1.20
    comment: "頁面標題 (fs-1)"
  h2:
    fontFamily: "Noto Sans TC, -apple-system, Roboto, sans-serif"
    fontSize: 32pt
    fontWeight: 700
    lineHeight: 1.20
    comment: "頁面標題 (fs-2)"
  h3:
    fontFamily: "Noto Sans TC, -apple-system, Roboto, sans-serif"
    fontSize: 28pt
    fontWeight: 600
    lineHeight: 1.20
    comment: "頁面標題 (fs-3)"
  h4:
    fontFamily: "Noto Sans TC, -apple-system, Roboto, sans-serif"
    fontSize: 24pt
    fontWeight: 700
    lineHeight: 28.8px
    comment: "Breadcrumb (fs-4)"
  h5:
    fontFamily: "Noto Sans TC, -apple-system, Roboto, sans-serif"
    fontSize: 20pt
    fontWeight: 500
    lineHeight: 24px
    comment: "頁面標題 (fs-5)"
  p:
    fontFamily: "Noto Sans TC, -apple-system, Roboto, sans-serif"
    fontSize: 16pt
    fontWeight: 400
    lineHeight: 28.8px
    comment: "內文文字 (fs-6 / H6)"
  sidebar-text:
    fontFamily: "Noto Sans TC, -apple-system, Roboto, sans-serif"
    fontSize: 14pt
    fontWeight: 400
    lineHeight: 20px
    comment: "一般文字 (fs-7 / sidebar / H7)"
  small-body:
    fontFamily: "Noto Sans TC, -apple-system, Roboto, sans-serif"
    fontSize: 12pt
    fontWeight: 400
    lineHeight: 16px
    comment: "小註解、補助文字 (Small / Body)"

css-implementation:
  font-family-fallback: "-apple-system, Noto Sans TC, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen, Ubuntu, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;"
  font-size-root: "16px /* 1rem 基準 */"

font-mapping:
  通用: "Noto Sans TC, -apple-system, Roboto, sans-serif"
  數字: "Roboto"
  其他: "BlinkMacSystemFont, Segoe UI"
  
---

本文件旨在梳理與規範 AI 應用平台的前端 UI/UX 設計與架構實作。基於現有開發原始碼（包含 `chat.html`、`ai-agent.html`、`sidebar-user.html`、`sidebar-admin.html` 以及相關樣式表 `style.css`、`sidebar.css`、`chat.css`、`modal.css`），歸納出整合性的設計系統與組件開發指引。

---

## 一、 設計哲學與視覺風格 (Design Philosophy & Visual Style)

平台定位為企業級 AI 應用與管理系統，整體設計依循**專業極簡主義 (Professional Minimalism)** 核心原則、與中性專業風格，以純白、深灰、純黑為基底，並搭配「專業藍」作為核心系統語意強調色。強調視覺的流暢度與功能的高效操作。

### 1. 色彩系統 (Color Palette)
色彩規劃採用低飽和度的中性色為基調，搭配專業藍色調作為主色與關鍵強調色，以營造穩重、專注且現代化的科技感。
* **主要背景與區域 (Backgrounds):**
    * 主內容區背景：`--content-area-bg: #F9FBFF` (輕盈、帶有極微量藍色調的冷白)
    * 卡片與基本區塊：`--card-bg: #ffffff`
    * 一般使用者側邊欄背景：`--sidebar-bg: #e6ebf7` (柔和的淺藍灰)
    * 管理者模式側邊欄背景：`--admin-sidebar-bg-color: #373737` (沉穩的深沉炭灰，用於明確區分操作語境)
* **文字與主要色彩 (Typography & Primary):**
    * 主要文字色：`--main-text-color: #000000` 
    * 次要/說明文字色：`#636363` (灰)
    * 主色/強調色：`--primary: #222222` 與次要主色 `--second-color: #23237B` (深邃藍)
* **狀態與錯誤 (Status & Error):**
    * 錯誤提示色：`--error-color: #CA0729` / `--second-error-color: #ad001d`

### 2. 邊框與陰影 (Borders & Shadows)
* **圓角規範：** 卡片與獨立區塊採用微圓角設計（如側邊欄邊界或對話框圓角控制），對話框訊息泡泡設定為 `border-radius: 22px`，在柔和與俐落間取得平衡。
* **陰影效果：** 採用輕量、細緻的投影，避免沉重的視覺負擔。
    * 標準卡片陰影：`box-shadow: 0px 3px 5px rgba(0, 0, 0, 0.05)`
    * 懸浮 (Hover) 增強陰影：`box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08)`

## 3. 字級與排版 (Typography)
全站字體採用現代系統預設黑體互補族群，確保程式碼與視覺高度還原：
* `font-family`: `-apple-system`, `BlinkMacSystemFont`, `Segoe UI`, `Roboto`, `Helvetica Neue`, `Arial`, `sans-serif`
* `h1` / `.fs-1`: `2.5rem` (Bold 700)
* `h2` / `.fs-2`: `2.0rem` (Bold 700)
* `h4` / `.fs-4`: `1.5rem` (Semi-Bold 600)
* `body` / `.fs-6`: `1.0rem` (Regular 400，對話與內容區行高設定為 `1.8rem` 確保長文閱讀舒適度)
* `.fs-7`: `0.875rem` (14px，輔助說明、微小時間戳記)


---

## 二、 核心組件設計架構 (Core Component Architecture)

### 1. 雙模側邊欄 (Dual-Mode Sidebar)
系統具備兩套獨立的側邊欄架構，分別對應一般使用者 (`sidebar-user.html`) 與系統管理員 (`sidebar-admin.html`)。兩者共享相同的響應式收合邏輯，但透過色彩與功能進行視覺隔離。

* **基礎佈局與收合 (Layout & Collapse):**
    * 展開狀態：固定寬度 `304px` (或最小 `280px` ~ 最大 `304px`)，提供充足的導覽標籤空間。
    * 收合狀態 (`.collapsed`): 寬度變更為 `80px`，自動隱藏所有文字標籤 (`.sidebar-text`, `span` 等)，僅保留核心 SVG 圖示。
    * 動態效果：設定 `transition: width 0.35s ease`，確保收合與展開時的視覺流暢。
* **互動細節：**
    * **歷史紀錄按鈕懸浮再現：** 歷史紀錄列表中的操作按鈕（如 `.btn-history`）預設透明度為 `0` (`opacity: 0`)，當游標懸浮至該導覽項目 (`.nav-item:hover`) 時，始平滑漸變至 `opacity: 1`，保持介面在靜態下的極簡乾淨。
    * **Bootstrap Tooltip 整合：** 為防止收合後無法辨識圖示含意，所有導覽項目均強制整合 `data-bs-toggle="tooltip"`，並設定於下方 (`data-bs-placement="bottom"`) 顯示提示。
    * **「顯示更多」摺疊面板：** 針對多餘的應用程式區塊，採用 `collapse` 面板控制，並透過 JavaScript 動態變更控制文字與箭頭方向（例如展開時顯示「顯示更少」並切換箭頭）。

### 2. AI 對話視窗介面 (Chat Interface)
對話介面為本平台核心互動場域，配置於最大寬度 `770px` 的置中流暢佈局內 (`.section-max-width-770`)。

* **對話泡泡佈局 (Message Bubbles):**
    * **使用者訊息 (`.chat-user-message`):** 整體靠右對齊 (`align-items: flex-end`)。對話框採用中性淺灰背景 (`background-color: #EBEBEB`)，內距設定為 `4px 16px`，圓角為 `22px`，最大寬度限制為螢幕的 `70%`，確保長文字的易讀性。
    * **AI 回覆訊息 (`.chat-assistant-message`):** 整體靠左對齊 (`align-items: flex-start`)。背景為透明或全域畫布色，文字行高加寬，確保排版具有呼吸感。

* **文字動畫與動態互動：**
    * **打字機流暢動畫：** 整合 `.char` 字元動畫，並透過 JavaScript 監聽最後一個字元的 `animationend` 事件。在動畫結束後，延遲 1 秒進行重置與重新初始化，提供平滑不生硬的生成視覺感。
    * **動態置底按鈕 (`.button-to-end`):** 採用固定定位 (`position: fixed; bottom: 60px; right: 50px;`)。當使用者向上捲動頁面時自動顯現，點擊後透過 `window.scrollTo` 的 `behavior: 'smooth'` 平滑滾動至最底部。
    
    * **深度思考區塊 (`.btn-reasoning-collapse`)**: 針對具備推理能力的模型（Reasoning Model），思考歷程必須預設或可手動折疊。左側搭配微小灰色裝飾線（`border-left: 2px solid #ccc`），內文顏色變更為次要輔助灰，與正式回覆做出視覺區隔。

### 對話輸入框區塊 (Input Dialog Box)
* **彈性高度**: `textarea.form-control-chat` 預設高度為 3 行 (`rows="3"`)。當觸發檔案拖曳 (Drag and Drop) 附加檔案時，動態套用 `.shift-down` 樣式以利排版延伸。
* **控制列與下拉選單**: 模型切換、快捷提示詞（Prompt）按鈕等，一律採用簡潔的扁平化 Dropdown 樣式或輕量彈窗。

* **輸入與錯誤處理：**
    * **圖片上傳縮圖：** 提供緊湊的縮圖預覽 (`50px * 50px`)，採用 `object-fit: cover` 處理，並隨附絕對定位的刪除按鈕。
    * **Snackbar 提示通知：** 捨棄瀏覽器原生傳統的 `alert()` 彈窗，改採**客製化 Snackbar 提示**，於觸發事件時顯示並於 5 秒後自動淡出消失。
    * **提示訊息區塊 (`.error-message`):** 使用漸層背景 (`linear-gradient(135deg, #e0f7fa, #f8e1e9)`) 搭配前置 Unicode ⓘ 圖示，以溫和不突兀的方式提示錯誤或系統資訊。

### 3. AI 應用管理中心與模型卡片 (AI Agent Management & Model Cards)
依據 `ai-agent.html` 的架構，管理中心負責展示與設定可用的 AI 代理人與模型資產。

* **基礎外觀**: 背景使用 `--card-bg` (`#ffffff`)，搭配極輕微陰影 `box-shadow: 0px 3px 5px rgba(0, 0, 0, 0.05)`，邊框為 `1px solid #E1E1E1`，圓角設定為 `8px` (`.rounded-3`)。
* **Hover 狀態**: 禁止使用任何刺眼的霓虹或彩色漸層。滑過時僅允許微妙的陰影加深 `box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08)`，保持畫面的乾淨與簡潔。

* **模型容器卡片區塊 (`.card-add-model-container`):**
    * **整置點擊群組 (Card-wide Click Handling):** 為提升使用者體驗，使用者點擊卡片內的任意非控制區域時，皆能自動觸發內嵌的單選按鈕 (`.radio-btn`) 進行選取切換。
    * **例外防護機制 (Event Target Exclusion):** 在 JavaScript 事件處理中，必須明確排除具備 `.disabled` 類別的元素，防止無效或唯讀狀態的卡片被誤點擊。
* **更多操作垂直選單 (`.btn-more-action-v`):**
    * 預設採用透明背景，懸浮時 (`:hover`) 轉換為白色背景並保持流暢的視覺回饋。定義於卡片右上方絕對定位 (`top: 19px; right: 16px;`)。
* **安全性互動：**
    * **密碼可視性切換 (Password Visibility Toggle):** 對於涉及金鑰或敏感密碼之輸入框（如 `#password`），右側隨附切換按鈕，透過操作 DOM 的 `type` 屬性於 `password` 與 `text` 間進行動態轉換，並同步更新 Font Awesome 圖示 (`fa-eye` 與 `fa-eye-slash`)。

### 4. 彈出式視窗樣式規範 (Modal Styling Specification)
依據 `modal.css` 樣式設定，彈出式視窗（Modal）用於調整客製化參數與核心表單輸入。

* **傳統 Div 實作與尺寸控制：**
    * 遵循平台技術規範，**嚴禁使用 HTML5 原生 `<dialog>` 標籤**，一律採用結構清晰的傳統 `<div>` 配合 Bootstrap Modal 機制實作，以確保跨瀏覽器樣式的高度客製化與控制權。
    * **基礎尺寸與內距：** `modal-content` 設定最小寬度 `min-width: 585px`；面板內距（`modal-body`, `modal-info`, `modal-footer`）統一使用百分比進行精確呼吸感控制：`padding: 4% 8% !important;`。
* **參數表單元件控制：**
    * **滑桿與數值雙向綁定：** 每一項參數皆由 `input[type="range"]` (滑桿) 與 `input[type="number"]` (數字輸入框) 共同組成。兩者維持數值同步與格式驗證，並提供「重置參數」按鈕一鍵恢復預設值。
    * **表單輔助說明 (`.form-text`):** 設定為 `font-size: 0.875rem` (等同 14px)，確保複雜設定下的閱讀舒適度。
* **按鈕控制組規範 (Modal Button Group):**
    * **外框按鈕 (`.btn-modal-outline`):** 預設背景透明，文字與邊框採用系統主色 `var(--main-color)`，配置左右高內距 `padding: 6px 48px;`，具備 `0.3s ease` 的平滑背景轉換動態。
    * **主實心按鈕 (`.btn-modal-default`):** 採用系統滿版主色背景，配置較大寬度之內距 `padding: 7px 58px;`，懸浮時自動與外框按鈕同步切換至 `--btn-bg-hover`。

## 5. 開發與互動防呆雷區 (Anti-Patterns & Code Standards)


---

## 三、 技術標準與開發規範 (Technical Standards)

為了維護平台代碼的高可讀性與擴充性，前端開發應嚴格遵守以下工程規範：

1.  **語意化命名與 CSS 架構：**
    * 元件與樣式命名優先遵循 **BEM (Block, Element, Modifier)** 或具備高度可讀性的語意化命名風格（如 `.chat-user-message`、`.card-add-model-container`、`.btn-modal-default`）。
    * 重複使用的元件屬性應抽取至 CSS 變數 (`:root`) 統一管理（如 `--main-color`, `--admin-sidebar-bg-color`）。
2.  **專業語彙規範 (Taiwan Context)：**
    * 代碼註解、介面文字與提示訊息一律使用台灣在地技術與商業術語。
    * **嚴禁使用** 非在地語彙如「`自定義`」，應一律使用「**`客製化`**」或「**`自訂`**」。
3.  **效能與資源優化：**
    * 圖示元件優先採用高解析度、可縮放且不失真的 **SVG** 格式，減少傳統圖片資源的請求負擔。
    * 網頁佈局結構應妥善處理寬度邊界與 `box-sizing: border-box`，防止因 Padding 或 Border 導致的排版溢出 (Overflow)。
4.  **資產完整度：**
    * 確保系統圖示、Favicon 標誌等基礎資產的路徑結構（如 `/images/logo/favicon.ico`）在各元件間的完整性。

5.  **互動轉場標準:** 所有具備點擊互動的元素（按鈕、卡片、Dropdown 項目）必須明確宣告 `cursor: pointer;`。滑過 (Hover) 與聚焦 (Focus) 狀態必須加上 `transition: all 0.2s ease-in-out;` (控制在 150ms - 300ms 之間)，確保極致平滑的互動反饋。

6.  **嚴禁使用瀏覽器預設 Alert 彈窗**: 當系統執行特定動作（如複製程式碼成功、表單送出、不滿足字數限制等通知），**絕對禁止**調用原生的 `window.alert()`。必須統一使用自訂的 **Snackbar / Toast 通知組件**，並設定為 **5 秒後自動滑動或淡出消失**，提供流暢的非阻斷式使用者體驗。
