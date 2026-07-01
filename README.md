# design.md
一些design.md檔

| Name | .md檔 |
| :--- | :--- |
| **TWAI 官網** | design_twai.md |
| **AFS AI Hub 應用平台** | design_aihub.md |
| :--- | :--- |
| 參考 | https://github.com/VoltAgent |



## TWAI 官網
### 1. 全站架構色彩系統 (Color Palette Table)

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

## 二、 全站分層前端組件與排版規範 (Tiered UI Component & Typography)

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


## AFS AI Hub 應用平台

## 一、 設計哲學與視覺風格 (Design Philosophy & Visual Style)

平台定位為企業級 AI 應用與管理系統，整體設計依循**專業極簡主義 (Professional Minimalism)** 核心原則與中性專業風格，以純白、深灰、純黑為基底，並搭配「專業藍」作為核心系統語意強調色。強調視覺的流暢度與功能的高效操作。

### 1. 色彩系統表格 (Color Palette Table)

| 變數名稱 / 類別 | 色碼 (HEX) | 適用場景與設計說明 |
| --- | --- | --- |
| `--content-area-bg` | `#F9FBFF` | 主內容區背景：輕盈、帶有極微量藍色調的冷白 |
| `--card-bg` | `#ffffff` | 卡片與基本獨立區塊背景 |
| `--sidebar-bg` | `#e6ebf7` | 一般使用者側邊欄背景（柔和的淺藍灰） |
| `--admin-sidebar-bg-color` | `#373737` | 管理者模式側邊欄背景（沉穩的深沉炭灰，明確區分操作語境） |
| `--main-text-color` | `#000000` | 主要文字顏色（純黑） |
| 次要文字顏色 | `#636363` | 說明文字、微小時間戳記 |
| `--primary` | `#222222` | 主色/核心強調色 |
| `--second-color` | `#23237B` | 次要主色（深邃藍，用於核心系統語意強調） |
| `--error-color` | `#CA0729` | 錯誤提示主色 |
| `--second-error-color` | `#ad001d` | 錯誤提示次要色/深紅色 |

### 2. 邊框、圓角與陰影 (Borders, Rounded & Shadows)

| 屬性分類 | 規範名稱 / Class | 具體設定值 | 設計與互動指引 |
| --- | --- | --- | --- |
| **圓角 (Rounded)** | 對話框訊息泡泡 | `border-radius: 22px` | 確保長文字對話時的視覺流暢與柔和感 |
| **圓角 (Rounded)** | 基本卡片/場景方塊 | `border-radius: 12px` | 俐落的微圓角設計 |
| **陰影 (Shadows)** | 標準卡片陰影 | `box-shadow: 0px 3px 5px rgba(0, 0, 0, 0.05)` | 輕量、細緻的投影，避免沉重的視覺負擔 |
| **陰影 (Shadows)** | 懸浮增強陰影 | `box-shadow: 0 8px 20px rgba(0, 0, 0, 0.08)` | `:hover` 觸發，提供平滑的懸浮回饋感 |

---

## 3. 字級與排版系統 (Typography System)

全站字體採用現代系統預設黑體互補族群，確保程式碼與視覺高度還原。

### 核心字型映射 (Font Mapping)

| 語境分類 | 字型家族 (Font Family) |
| --- | --- |
| **通用 / 繁體中文** | `Noto Sans TC, -apple-system, BlinkMacSystemFont, sans-serif` |
| **數字 / 英數標題** | `Roboto, Segoe UI, Helvetica Neue, Arial` |
| **CSS 備用機制 (Fallback)** | `-apple-system, Noto Sans TC, BlinkMacSystemFont, Segoe UI, Roboto, Oxygen, Ubuntu, Fira Sans, Droid Sans, Helvetica Neue, sans-serif;` |

### 字體級距表 (Typography Hierarchy)

| 標籤 / Class | 級距 (Size) | 字重 (Weight) | 行高 (Line Height) | 台灣專業語意與對應場景 (Comments) |
| --- | --- | --- | --- | --- |
| `h1` / `.fs-1` | `40pt` (2.5rem) | 700 (Bold) | 1.20 | 頂層頁面大型標題 |
| `h2` / `.fs-2` | `32pt` (2.0rem) | 700 (Bold) | 1.20 | 次級頁面標題 |
| `h3` / `.fs-3` | `28pt` | 600 (Semi-Bold) | 1.20 | 組件區塊中型標題 |
| `h4` / `.fs-4` | `24pt` (1.5rem) | 700 (Bold) | 28.8px | 麵包屑導覽 (Breadcrumb) 與次要標題 |
| `h5` / `.fs-5` | `20pt` | 500 (Medium) | 24px | 彈窗或小組件標題 |
| `p` / `h6` / `.fs-6` | `16pt` (1.0rem) | 400 (Regular) | 28.8px (1.8rem) | 核心內文文字、對話內容區（寬鬆行高確保長文舒適度） |
| `.fs-7` / `sidebar` | `14pt` (0.875rem) | 400 (Regular) | 20px | 側邊欄導覽文字、自訂/客製化參數輔助說明標籤 |
| `small` / `body-sm` | `12pt` | 400 (Regular) | 16px | 系統極小註解、微小時間戳記與補助文字 |

---
