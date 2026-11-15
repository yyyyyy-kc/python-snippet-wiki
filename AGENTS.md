# AGENTS.md — Python 練習心得與程式碼碎片庫 (Python Snippet & Insight Wiki)

本文件是專案的「單一事實來源」，用來規範 AI 助手如何理解、維護與擴充本專案。
**開始任何修改前，請先完整閱讀本文件，並先打開 `index.html` 看現有卡片的寫法；若使用者指令與本文件衝突，以使用者最新指令為準，並在回覆中說明差異。**

- GitHub Repository：https://github.com/yyyyyy-kc/python-snippet-wiki
- 網頁（GitHub Pages）：https://yyyyyy-kc.github.io/python-snippet-wiki/

---

## 1. 專案目的 (Project Purpose)

- **核心定位**：收錄個人在 Python 學習、演算法練習與日常開發中整理的「實戰心得」與「程式碼碎片 (Code Snippets)」，作為可隨時回頭查閱的個人知識庫。
- **使用情境**：忘記某個語法、想回顧當時踩過的坑、想快速複製一段可執行的範例。
- **目標讀者**：未來的自己（主要）、正在學 Python 的同學或朋友（次要）。
- **內容特色**：所有說明、註解與邏輯拆解，皆須以**使用者自己的語言與思考脈絡**描述（口語、白話、繁體中文），拒絕生硬或純理論的官方文件腔調。
- **成功標準**：打開網頁就能快速找到想要的碎片，並看懂「這段程式在做什麼、為什麼這樣寫、哪裡容易錯」。

---

## 2. 技術架構與限制 (Tech Stack & Constraints)

- **零複雜框架**：純 `HTML` + `Tailwind CSS`（CDN）+ 原生 `JavaScript`。
- **零建置工具 (No Build Tools)**：不使用 npm、webpack、Vite、React、Vue 等；不得要求使用者執行任何指令才能預覽。
- **單一頁面**：所有內容都寫在 `index.html`，卡片直接以 HTML 撰寫，**不使用外部資料檔、不使用 `fetch`**，確保雙擊 `index.html` 就能在本機開啟。
- **部署方式**：直接推送到 **GitHub Pages**（`main` 分支根目錄）即可瀏覽。所有資源路徑使用**相對路徑**。
- **依賴套件（CDN）**：
  - CSS：Tailwind CSS
  - 程式碼高亮：Prism.js 或 Highlight.js（若頁面已使用，沿用現有的，不要換）
  - 圖標（選用）：Lucide Icons 或 FontAwesome
- **相容性**：支援最新版 Chrome / Edge / Safari / Firefox；需 RWD（手機寬度也能正常閱讀）。

---

## 3. 檔案結構 (Directory Structure)

```text
python-snippet-wiki/
├── AGENTS.md      # 本專案的 AI 開發規範文件（本檔）
├── index.html     # 唯一頁面：標題 + 卡片 Grid + 頁尾
└── README.md      # 專案簡介與網址（選用，建議補上）
```

**規則**
- 新增內容 = **只在 `index.html` 的卡片區新增一張卡片**，不要動頁首、頁尾與樣式設定。
- 新增卡片時，**複製現有卡片的 HTML 結構與 Tailwind class 當範本**，確保風格一致。
- 若日後內容變多，才考慮拆成多個頁面；拆分前必須先更新本文件。

---

## 4. 卡片結構 (Card Structure)

每張卡片包含以下區塊，**順序固定**：

| 順序 | 區塊 | 內容說明 |
|------|------|----------|
| 1 | 分類標籤 | 格式：`分類 / 主題 #編號`，例如 `物件導向 / Class #01` |
| 2 | 標題 (h2) | 一句話點出主題，例如「Python Class 核心用法與觀念筆記」 |
| 3 | 核心心得與功能說明 (h3 + 段落) | 用自己的話寫 3–5 句 |
| 4 | 輸入與輸出範例 (h3) | `Input:` / `Terminal:` 與 `Output:` 各一行 |
| 5 | 程式碼區塊 | 頂部顯示檔名（如 `vector_demo.py`）與「一鍵複製」按鈕 |

**目前已有的卡片**（新增時依序往下編號）
- `#01` 物件導向 / Class — Python Class 核心用法與觀念筆記（`vector_demo.py`）
- `#02` 命令列與系統 / sys — 使用 sys 模組接收命令列參數（`sys_demo.py`）

**編號規則**
- 編號為兩位數、依新增順序遞增（`#03`、`#04`…），不得重複或跳號。
- 分類名稱沿用既有的；若需要新分類，用簡短中文 + 英文模組名（例如 `檔案處理 / open`），並在上方「目前已有的卡片」清單補上。

**HTML 範本（僅供參考，實際以 `index.html` 現有卡片為準）**

```html
<article class="rounded-xl border bg-white p-6 shadow-sm">
  <p class="text-sm text-indigo-600">分類 / 主題 #03</p>
  <h2 class="mt-1 text-xl font-bold">卡片標題</h2>

  <h3 class="mt-4 font-semibold">核心心得與功能說明</h3>
  <p class="mt-1 text-gray-700">我之前以為……，後來發現……</p>

  <h3 class="mt-4 font-semibold">輸入與輸出範例</h3>
  <p class="text-sm">Input: <code>…</code></p>
  <p class="text-sm">Output: <code>…</code></p>

  <div class="mt-4 rounded-lg bg-gray-900 text-gray-100">
    <div class="flex justify-between px-4 py-2 text-xs">
      <span>demo_name.py</span>
      <button type="button" aria-label="複製程式碼">一鍵複製</button>
    </div>
    <pre><code class="language-python"># 程式碼放這裡</code></pre>
  </div>
</article>
```

---

## 5. 內容撰寫規範 (Content Style Guide)

### 5.1 心得的寫法
- 用**第一人稱**與口語繁體中文：「我之前以為…，後來發現…」「我現在的習慣是…」。
- 至少包含一項：**為什麼這樣寫 / 我的理解 / 和其他寫法的比較 / 踩過的坑**。
- **禁止**：整段複製官方文件、教科書式定義、空泛形容（「非常強大」「十分方便」）、純翻譯式語句。
- **禁止留下 AI 工具的引用標記**，例如 `[cite: 2]`、`[1]`、`【來源】`。新增或修改後請搜尋 `cite` 確認沒有殘留。
- 長度 3–5 句。

### 5.2 程式碼的寫法
- 必須是**可直接複製執行**的完整片段（含必要的 `import`），並用 `print()` 或註解標示預期輸出。
- 遵守 PEP 8：4 空格縮排、`snake_case` 命名；單段建議 ≤ 25 行。
- 註解用繁體中文，說明「為什麼」而不是重複「做什麼」。
- 不得包含真實個資、API Key、密碼或本機絕對路徑。
- 檔名使用 `xxx_demo.py` 格式。

### 5.3 語言與用字
- 介面與內容一律**繁體中文**；專有名詞保留英文（如 class、list、decorator）。
- 中英文之間加半形空格。

---

## 6. UI / 設計規範 (UI Guidelines)

- **版面**：頂部標題與一句副標 → 卡片區 → 頁尾；卡片以 Grid 排列（手機 1 欄、桌機 2 欄以上）。
- **視覺**：沿用 Tailwind 預設色票，主色固定為 `indigo`；程式碼區塊使用深色背景。
- **互動**：每張卡片的程式碼區塊都要有可用的「一鍵複製」按鈕。
- **無障礙**：按鈕需有 `aria-label`；文字與背景對比足夠。
- **頁尾**：維持現有格式，不要隨意更動。

---

## 7. AI 作業流程 (Workflows)

### 7.1 新增一張卡片
1. 打開 `index.html`，找到最後一張卡片，確認目前的最大編號。
2. 複製最後一張卡片的完整 HTML，貼在其後，替換成新內容。
3. 編號 +1，依 §5 撰寫心得與程式碼，並更新本文件 §4「目前已有的卡片」清單。
4. 確認「一鍵複製」按鈕對新卡片也有效。
5. 回報：新增了哪張卡片、編號為何。

### 7.2 修改既有卡片
1. 以編號與標題定位，只改使用者指定的部分。
2. 不得更動其他卡片，也不要改變既有編號。

### 7.3 新增功能（如搜尋、分類篩選、深色模式）
1. 先在本文件 §6 補上規則，再實作。
2. 保持零建置原則，不引入新框架。

### 7.4 提交前檢查清單 (Pre-commit Checklist)
- [ ] 雙擊 `index.html` 可正常開啟，瀏覽器 Console 沒有錯誤
- [ ] 所有路徑為相對路徑
- [ ] 卡片編號連續、區塊順序符合 §4
- [ ] 頁面中沒有 `[cite: …]` 之類的殘留標記
- [ ] 程式碼可執行，「一鍵複製」按鈕有效
- [ ] 手機寬度排版正常
- [ ] 心得語氣符合 §5.1（第一人稱、口語）
- [ ] 本文件的卡片清單與實際頁面一致

---

## 8. 禁止事項 (Do's & Don'ts)

**✅ 請這樣做**
- 小步修改、每次只處理一件事，並說明改了哪些檔案。
- 內容不確定時，詢問使用者，而不是自行編造心得。
- 保持現有風格一致（命名、縮排、配色、卡片結構）。

**❌ 請不要**
- 不要引入 npm、打包工具或前端框架。
- 不要新增需要伺服器的功能（如 `fetch` 外部 API、後端）。
- 不要刪除或重寫使用者既有的心得內容（除非被明確要求）。
- 不要把官方文件原文貼進心得。
- 不要在程式碼或文件中寫入任何金鑰或個資。

---

## 9. 部署與版本控管 (Deployment & Git)

- **部署**：GitHub → Settings → Pages → Source 選 `main` / `(root)`，網址為 https://yyyyyy-kc.github.io/python-snippet-wiki/ 。
- **Commit 訊息**（繁體中文，前綴分類）：
  - `新增：#03 檔案讀寫卡片`
  - `修改：調整卡片間距`
  - `文件：更新 AGENTS.md 卡片清單`
  - `修正：移除殘留的 cite 標記`
- **分支**：個人專案可直接使用 `main`。

---

## 10. 延伸與重複使用 (Extensibility)

- 本規範可平移到其他主題（如 SQL 筆記、JavaScript 碎片庫）：複製專案，修改 §1 專案目的與 §4 的分類與卡片清單，保留 §2、§5–§8 的規則即可。
- 內容變多時，可依序升級：加入搜尋與分類篩選 → 把卡片資料抽成 `data/snippets.js`。**升級前必須先更新本文件**，AI 才能依新結構繼續維護。
