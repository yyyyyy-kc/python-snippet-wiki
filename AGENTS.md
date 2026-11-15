# AGENTS.md — Python 練習心得與程式碼碎片庫 (Python Snippet & Insight Wiki)

歡迎來到本專案！本文件是用於規範 AI 助手如何理解、維護與擴充本專案的核心指導方針。請所有參與開發與維護的 AI 嚴格遵守本規範。

---

## 1. 專案目的 (Project Purpose)
- **核心定位**：收錄個人在 Python 學習、演算法練習與日常開發中所整理的「實戰心得」與「程式碼碎片 (Code Snippets)」。
- **內容特色**：所有的說明、註解與邏輯拆解，皆必須以**使用者自己的語言與思考脈絡**來描述，拒絕生硬或純理論的官方文件腔調。

---

## 2. 技術架構與限制 (Tech Stack & Constraints)
- **零複雜框架**：採用純 `HTML`、`Tailwind CSS` (透過 CDN 引入) 以及原生 `JavaScript`。
- **部署方式**：無須複雜建置工具（No Build Tools），所有變更直接寫入單一頁面或模組化檔案中，確保可直接推送到 **GitHub Pages** 正常瀏覽。
- **依賴套件**：
  - CSS：Tailwind CSS (CDN)
  - 程式碼高亮：Prism.js 或 Highlight.js (CDN)
  - 圖標：Lucide Icons 或 FontAwesome (CDN，若有需要)

---

## 3. 檔案結構與命名規範 (Directory Structure & Naming)
```text
my-python-wiki/
├── AGENTS.md          # 本專案的 AI 開發規範文件
├── index.html         # 主頁面（採用卡片式看板 Grid 呈現所有工具與碎片）
└── README.md          # 專案說明與 GitHub 呈現簡介