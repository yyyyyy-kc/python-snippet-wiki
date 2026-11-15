# AGENTS.md — Python 練習心得與程式碼碎片庫 (Python Snippet & Insight Wiki)

本文件是專案的「單一事實來源」，用來規範 AI 助手如何理解、維護與擴充本專案。
**開始任何修改前，請先完整閱讀本文件；若使用者指令與本文件衝突，以使用者最新指令為準，並在回覆中說明差異。**

---

## 1. 專案目的 (Project Purpose)

- **核心定位**：收錄個人在 Python 學習、演算法練習與日常開發中整理的「實戰心得」與「程式碼碎片 (Code Snippets)」，作為可隨時回頭查閱的個人知識庫。
- **使用情境**：忘記某個語法、想回顧當時踩過的坑、想快速複製一段可執行的範例。
- **目標讀者**：未來的自己（主要）、正在學 Python 的同學或朋友（次要）。
- **內容特色**：所有說明、註解與邏輯拆解，皆須以**使用者自己的語言與思考脈絡**描述（口語、白話、繁體中文），拒絕生硬或純理論的官方文件腔調。
- **成功標準**：打開網頁 10 秒內能找到想要的碎片，並看懂「這段程式在做什麼、我當時為什麼這樣寫、哪裡容易錯」。

---

## 2. 技術架構與限制 (Tech Stack & Constraints)

- **零複雜框架**：純 `HTML` + `Tailwind CSS`（CDN）+ 原生 `JavaScript`（ES6+）。
- **零建置工具 (No Build Tools)**：不使用 npm、webpack、Vite、React、Vue 等；不得要求使用者執行任何指令才能預覽。
- **部署方式**：直接推送到 **GitHub Pages**（`main` 分支根目錄）即可瀏覽。所有資源路徑必須使用**相對路徑**。
- **資料載入**：資料以 `<script src="data/snippets.js">` 載入（**不用 `fetch` 讀 JSON**），確保雙擊 `index.html` 本機開啟也能正常運作。
- **CDN 依賴（固定版本，不得隨意更換）**：
  - CSS：Tailwind CSS (CDN)
  - 程式碼高亮：Prism.js（含 Python 語言包與 Copy 功能）
  - 圖標（選用）：Lucide Icons
- **相容性**：支援最新版 Chrome / Edge / Safari / Firefox；需 RWD（手機 ≥ 360px 可正常閱讀）。

---

## 3. 檔案結構與命名規範 (Directory Structure & Naming)

```text
my-python-wiki/
├── AGENTS.md            # 本專案的 AI 開發規範文件（本檔）
├── README.md            # 專案簡介、線上網址、使用與新增方式
├── index.html           # 主頁面：搜尋列 + 分類篩選 + 卡片 Grid
├── assets/
│   └── app.js           # 渲染、搜尋、篩選、複製按鈕等互動邏輯
└── data/
    └── snippets.js      # 所有碎片資料（唯一需要新增內容的地方）
```

**命名規則**
- 檔案與資料夾：小寫英文 + 連字號（kebab-case），例如 `snippets.js`。
- 碎片 `id`：小寫英文 + 連字號，且**全域唯一**，例如 `list-comprehension-basic`。
- 分類 (`category`)：只能使用 §5 列出的既有分類；新增分類需先更新本文件。
- 標籤 (`tags`)：小寫英文或繁體中文皆可，每張卡片 2–5 個。

> 規則：**新增內容 = 只改 `data/snippets.js`**；除非需要新功能，否則不要動 `index.html` 與 `app.js`。

---

## 4. 資料結構 (Data Schema)

每個碎片是 `data/snippets.js` 中 `SNIPPETS` 陣列的一個物件：

```js
const SNIPPETS = [
  {
    id: "list-comprehension-basic",      // 唯一 id (kebab-case)
    title: "List Comprehension 一行搞定迴圈",   // 簡短標題，≤ 20 字
    category: "基礎語法",                  // 必須來自 §5 分類表
    level: "初級",                        // 初級 | 中級 | 進階
    tags: ["list", "迴圈", "簡潔寫法"],
    date: "2026-11-15",                   // YYYY-MM-DD，新增或最後修改日
    insight:                              // 我的心得：用自己的話，2–5 句
      "以前我都先 append 再 return，後來發現 comprehension 可以一行搞定。" +
      "但條件一多就很難讀，超過兩層我還是會改回 for。",
    code:                                 // 可直接執行的完整範例
`squares = [n ** 2 for n in range(10) if n % 2 == 0]
print(squares)  # [0, 4, 16, 36, 64]`,
    pitfalls:                             // 踩坑提醒（選填，可為空陣列）
      ["comprehension 內的變數在 Python 3 不會外洩到外層"],
    related: ["generator-expression"]     // 相關碎片 id（選填）
  }
];
```

**欄位規則**
| 欄位 | 必填 | 說明 |
|------|------|------|
| `id` / `title` / `category` / `level` / `date` / `insight` / `code` | ✅ | 缺一不可 |
| `tags` | ✅ | 2–5 個 |
| `pitfalls` / `related` | ❌ | 沒有就給 `[]` |

---

## 5. 分類表 (Categories)

| 分類 | 適用內容 |
|------|----------|
| 基礎語法 | 變數、運算子、流程控制、字串、容器操作 |
| 函式與物件 | function、lambda、class、decorator、dataclass |
| 資料結構與演算法 | 排序、搜尋、遞迴、動態規劃、LeetCode 類題目 |
| 檔案與資料處理 | 檔案讀寫、JSON/CSV、正規表達式、pandas 入門 |
| 實用工具 | 日常自動化腳本、標準庫小技巧、debug 手法 |
| 踩坑筆記 | 錯誤訊息、易混淆概念、效能陷阱 |

---

## 6. 內容撰寫規範 (Content Style Guide)

### 6.1 心得 (`insight`) 的寫法
- 用**第一人稱**與口語繁體中文：「我之前以為…，後來發現…」。
- 一定要包含至少一項：**為什麼這樣寫 / 我的理解 / 和其他寫法的比較**。
- **禁止**：整段複製官方文件、空泛形容（「非常強大」「十分方便」）、純翻譯式語句。
- 長度 2–5 句；超過請拆成 `pitfalls`。

### 6.2 程式碼 (`code`) 的寫法
- 必須是**可直接複製執行**的完整片段（含必要的 `import`），並以 `print()` 或註解標示預期輸出。
- 遵守 PEP 8：4 空格縮排、`snake_case` 命名；單段建議 ≤ 25 行。
- 註解用繁體中文，說明「為什麼」而不是重複「做什麼」。
- 不得包含真實個資、API Key、密碼或本機絕對路徑。

### 6.3 語言與用字
- 介面與內容一律**繁體中文**；專有名詞保留英文（如 list、dict、decorator）。
- 標點使用全形（，。：），中英文之間加半形空格。

---

## 7. UI / 設計規範 (UI Guidelines)

- **版面**：頂部標題 + 搜尋框 + 分類篩選按鈕；下方為 **卡片式 Grid**（手機 1 欄、平板 2 欄、桌機 3 欄）。
- **卡片內容順序**：分類徽章 + 難度 → 標題 → 心得 → 程式碼區塊（附「複製」按鈕）→ 踩坑提醒 → 標籤。
- **互動**：
  - 搜尋同時比對 `title`、`tags`、`insight`（不分大小寫）。
  - 分類篩選與搜尋可疊加；無結果時顯示友善的空狀態文字。
  - 「複製」按鈕點擊後顯示 1.5 秒的「已複製 ✓」提示。
- **視覺**：沿用 Tailwind 預設色票，主色固定為 `indigo`，難度徽章：初級 `green`、中級 `amber`、進階 `rose`；支援深色背景的程式碼區塊（Prism `tomorrow` 主題）。
- **無障礙**：按鈕需有 `aria-label`；色彩對比需足夠；整頁可用鍵盤操作。

---

## 8. AI 作業流程 (Workflows)

### 8.1 新增一張碎片
1. 讀取 `data/snippets.js`，確認 `id` 不重複、`category` 在 §5 範圍內。
2. 依 §4 格式在陣列**末端**新增物件，並依 §6 撰寫內容。
3. 更新 `README.md` 的「碎片數量」（若有標註）。
4. 回報：新增了哪張卡片、`id` 為何。

### 8.2 修改既有碎片
1. 以 `id` 定位，只改必要欄位，並將 `date` 更新為今日。
2. 不得更動其他碎片或改變 `id`（避免破壞 `related` 連結）。

### 8.3 新增分類或功能
1. 先在本文件 §5 或 §7 補上規則，再實作程式。
2. 保持零建置原則，不引入新框架。

### 8.4 提交前檢查清單 (Pre-commit Checklist)
- [ ] 雙擊 `index.html` 可正常開啟、無 Console 錯誤
- [ ] 所有路徑為相對路徑（GitHub Pages 可用）
- [ ] `id` 唯一、欄位齊全、`category` 合法
- [ ] 程式碼可執行，語法高亮正常，複製按鈕有效
- [ ] 手機寬度（360px）排版正常
- [ ] 心得語氣符合 §6.1（第一人稱、口語）
- [ ] README 與本文件如有受影響處已同步更新

---

## 9. 禁止事項 (Do's & Don'ts)

**✅ 請這樣做**
- 小步修改、每次只處理一件事，並說明改了哪些檔案。
- 內容不確定時，詢問使用者，而不是自行編造心得。
- 保持現有風格一致（命名、縮排、配色）。

**❌ 請不要**
- 不要引入 npm / 打包工具 / 前端框架。
- 不要使用 `fetch`、`localStorage` 以外需要伺服器的功能。
- 不要刪除或重寫使用者既有的心得內容（除非被明確要求）。
- 不要把官方文件原文貼進 `insight`。
- 不要在程式碼或文件中寫入任何金鑰或個資。

---

## 10. 部署與版本控管 (Deployment & Git)

- **部署**：GitHub → Settings → Pages → Source 選 `main` / `(root)`；網址格式 `https://<帳號>.github.io/my-python-wiki/`。
- **Commit 訊息**（繁體中文，前綴分類）：
  - `新增：list comprehension 碎片`
  - `修改：調整卡片 RWD 排版`
  - `文件：更新 AGENTS.md 分類表`
  - `修正：複製按鈕在 Safari 失效`
- **分支**：個人專案可直接使用 `main`；大型改動建議開 `feature/*` 分支。

---

## 11. 延伸與重複使用 (Extensibility)

本規範設計為可複用的「個人知識庫範本」，之後可平移到其他主題（如 SQL 筆記、JavaScript 碎片庫）：
1. 複製本專案，修改 §1 專案目的與 §5 分類表。
2. 保留 §2–§4 的零建置架構與資料驅動設計。
3. 只需替換 `data/snippets.js` 的內容，即可產生新的知識庫網站。

**未來可擴充方向（需先更新本文件再實作）**：深色模式切換、標籤雲、依日期排序、匯出為 Markdown、每日隨機一張複習卡片。
