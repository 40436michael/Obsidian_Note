# 個人知識庫規則

這個 Obsidian vault 採用 LLM Wiki 模式（參考 Karpathy 的 llm-wiki）：
使用者自己寫原始閱讀筆記，Claude 負責把它們整理成互相連結的 wiki。
每次在這個 vault 工作前都要先讀這份檔案。

## 三層結構

| 層    | 位置          | 誰寫     | 說明                               |
| ---- | ----------- | ------ | -------------------------------- |
| 原始筆記 | `raw/`      | 使用者    | 書籍、文章、開源專案的閱讀筆記。**Claude 只讀不改。** |
| Wiki | `wiki/`     | Claude | 摘要、概念、人物、比較分析。使用者只看不寫。           |
| 規則   | `CLAUDE.md` | 雙方     | 本檔。結構或流程改變時一起更新。                 |

```
raw/
  books/<書名>/<書名>.md               書籍資訊卡（type: book）
  books/<書名>/<書名> NN 章名.md        章節筆記（type: chapter）
  articles/                           網路文章
  projects/<專案>/<專案>.md            專案資訊卡（type: project）
  projects/<專案>/<專案> NN 主題.md     原始碼閱讀筆記（type: code-note）
  projects/<專案>/<專案> issue-NNN.md   issue 處理筆記（type: issue-note）
wiki/
  index.md        所有 wiki 頁面的目錄
  log.md          操作紀錄（只新增，不修改舊紀錄）
  books/          <書名> 摘要.md
  projects/<專案>/ code wiki（見「Code Wiki」章節）
  concepts/       跨來源的概念
  people/         作者與人物
  syntheses/      從提問得到、值得保存的比較與分析
Templates/        Templater 模板（使用者手動建立筆記用）
書單.base          書單總表（Obsidian Bases）
```

開源專案的原始碼：
- **學習**：預設在線上閱讀（GitHub 網頁、raw.githubusercontent.com、`gh api`）。
- **貢獻**：需要在本機執行與測試，可以 clone，但**每次 clone 前都要先取得使用者同意**。
- clone 一律放在 vault 外（例如 `C:\Users\michael\code\<專案>`），絕不把原始碼放進 vault。
- 不執行專案的安裝腳本或 build（如 `npm install` 的 postinstall），除非使用者同意。

## 命名規則

- Obsidian 以檔名連結，檔名必須全 vault 唯一。
- 章節筆記前綴書名：`Clean Code 03 函式`；原始碼筆記前綴專案名。
- wiki 書籍頁加「摘要」：`Clean Code 摘要`。
- code wiki 頁前綴專案名與編號：`claudian 11 執行抽象層`（編號規則見「Code Wiki」）。
- 概念頁用中文命名，英文原名放在 `aliases`。

## Wiki 頁面格式

每頁都有 frontmatter：

```yaml
---
type: book-summary | concept | person | synthesis   # code wiki 頁另見下方格式
aliases: []
sources: ["[[Clean Code 03 函式]]"]
updated: YYYY-MM-DD
---
```

## 寫作規則

1. **每個論點附出處**：連回 raw 筆記，例如 `（[[Clean Code 03 函式]]）`。
2. **區分觀點**：作者的主張與使用者在「我的想法」寫的內容分開，後者標示為「我的看法」。
3. **擴充優先於新增**：先查 `index.md` 有沒有相近頁面，有就擴充，避免近似重複的頁面。
4. **標示矛盾**：不同來源說法衝突時用 `> [!warning] 矛盾` 並列兩方說法與出處，不自行選邊。
5. **程式碼引用固定版本**：引用開源專案程式碼時使用專案資訊卡記錄的 commit，
   連結格式 `https://github.com/<owner>/<repo>/blob/<commit>/<path>#L<行>`。
6. **不修改 `raw/`**：發現原始筆記有錯或不清楚，告訴使用者，由使用者修改。
7. 使用繁體中文。

## 操作

### `ingest <來源>`（例：`ingest Clean Code 03`）
1. 讀對應的 raw 筆記（原始碼筆記需要時在線上讀對應 commit 的原始碼）。
2. 先向使用者簡短列出這篇的重點與打算更新哪些頁面，取得確認。
3. 更新或建立：書籍／專案摘要、相關概念頁、人物頁，加上互相連結。
4. 更新 `index.md`。
5. 在 `log.md` 尾端新增紀錄。

### 提問
1. 先讀 `index.md` 找相關頁面，再深入閱讀。
2. 回答並附出處。
3. 若答案有保存價值，詢問使用者是否存成 `wiki/syntheses/` 頁面（存了就更新 index 與 log）。

### `lint`
檢查並列出清單，由使用者決定如何處理：
- 頁面間互相矛盾的說法
- 沒有任何連入連結的孤立頁面
- 被多次提及但沒有自己頁面的概念
- 缺少的交叉連結、`index.md` 漏列的頁面
- raw 中已有但尚未 ingest 的筆記
- code wiki 的 commit 落後上游太多（提示可執行 `code-wiki update`）

### `新書 <書名>` / `新專案 <專案名>`
依 `Templates/` 的格式在 `raw/` 建立資料夾與資訊卡（frontmatter 填好已知資訊，其餘留空）。

## Code Wiki

參考 zread.ai 與 Google Code Wiki：Claude 為開源專案產生互相連結、固定在某個 commit 的程式碼 wiki，
放在 `wiki/projects/<專案>/`。使用者讀程式碼時的疑問與理解仍寫在 `raw/projects/<專案>/`，ingest 時連到對應頁面。

**目的是幫使用者學習並貢獻開源專案**，因此：
- **用到再寫**：不一次產生整份 wiki。先寫 00 概覽、01 快速開始、02 貢獻指南，
  其他頁面在使用者閱讀、提問或處理 issue 時才補。
- **程式碼由使用者寫**：處理 issue 時 Claude 負責解釋、指路、review，不代寫修改；
  使用者明確要求時才提供範例程式碼，並說明每一行的理由。

### 結構與編號

兩層：主題頁（hub）→ 子頁。資料夾維持扁平，用編號表達層級：

```
wiki/projects/<專案>/
  <專案> 00 概覽.md          敘述式概覽，每段介紹一個主題並連到該主題頁
  <專案> 01 快速開始.md      安裝、執行、目錄樹（0x = 入門）
  <專案> 02 貢獻指南.md      見下方「貢獻指南頁」
  <專案> 10 <主題>.md        主題頁：總覽並導向子頁（十位數 = 主題，個位數 0 = 主題頁）
  <專案> 11 <子題>.md        子頁（個位數 1–9）
  <專案> 20 <主題>.md
  ...
```

主題的分法：小專案依閱讀順序（入門 → 架構 → 內部實作 → 功能 → 橫切關注點，zread 式），
大專案依功能領域（Code Wiki 式）。規劃目錄時提出建議，由使用者決定。

### 頁面格式

```markdown
---
type: code-wiki
project: "[[<專案> 00 概覽]]"
repo: https://github.com/<owner>/<repo>
commit: <完整 hash>
sources: [src/a.ts, src/b.ts]     # 本頁依據的檔案，供 update 判斷影響範圍
updated: YYYY-MM-DD
---
# <標題>
> [!info] 依據 commit `<短 hash>`（YYYY-MM-DD）。由 Claude 產生，可能有誤。

（內文）

## 設計觀察
（為什麼這樣設計；連到 [[concepts]] 概念頁，例如依賴反轉、單一職責）

## 接下來讀
- [[<專案> NN 下一頁]]
```

概覽頁（00）另外列出：專案一句話說明、技術棧表、主題目錄與建議閱讀路徑。
尚未撰寫的頁面在目錄中列出標題但不加連結，標示「（未寫）」。

### 貢獻指南頁（02）

依專案的 CONTRIBUTING、AGENTS.md／CLAUDE.md、PR 模板、CI 設定整理，固定段落：
1. 開發環境（語言版本、安裝、啟動）
2. 提交前的驗證指令（測試、lint、型別檢查、build）
3. 程式碼規範（命名、風格、架構限制）
4. PR 流程（分支、commit 格式、PR 模板、review 要求）
5. **AI 輔助政策**（是否允許、是否需揭露；找不到就寫「未明文規定」）
6. 適合新手的 issue 標籤與入口
每點附出處連結。

### 依內容選擇呈現方式

| 內容 | 呈現方式 |
|---|---|
| 職責說明 | 敘述文字，路徑與符號直接寫進句子並連到原始碼 |
| 列舉（指令、設定、模組清單） | 表格 |
| 有先後順序的流程 | 編號清單 |
| 模組間依賴 | Mermaid `graph TD` |
| 核心抽象（介面、實作、繼承） | Mermaid `classDiagram` |
| 跨元件的呼叫順序 | Mermaid `sequenceDiagram` |

圖只在有助理解時才畫，不為每頁硬塞。

### 出處

- 連到符號層級，文字寫符號名稱、網址固定在 commit：
  `` [`ClaudeExecutionSession.steer()`](https://github.com/<owner>/<repo>/blob/<commit>/<path>#L267) ``
- **寫完每頁後驗證出處**：逐一確認引用的檔案與行號在該 commit 存在、內容與敘述相符；對不上就修正或刪除該句。

### `code-wiki <repo 網址>`
1. 在線上讀 README、目錄樹、進入點、各資料夾的說明文件（不 clone）。
2. 提出兩層目錄規劃：每頁標題與一句話說明，並建議分法（閱讀順序／功能領域）→ 等使用者確認。
3. 只寫 00 概覽、01 快速開始、02 貢獻指南。其他頁面等使用者說「寫 <頁面>」或在提問／issue 中需要時再寫，
   一次一個主題（主題頁 + 需要的子頁）。
4. 若 `raw/projects/<專案>/` 尚無專案資訊卡，詢問是否建立。
5. 更新 `index.md`、`log.md`。

### `issue <issue 網址>`
1. 讀 issue 與討論串，用一兩句話說明問題本質；確認是否已有人認領或有關聯 PR。
2. 找出相關檔案與呼叫路徑，連到對應 wiki 頁面；缺的頁面依需要補寫。
3. 提出 2–3 種可能修法與取捨，對照 02 貢獻指南指出要注意的規範與測試。不代寫修改。
4. 使用者寫完修改後，依專案規範 review：正確性、測試、風格、PR 描述。
5. 建議使用者寫 `raw/projects/<專案>/<專案> issue-NNN.md`（學到什麼、為什麼這樣修），之後可 ingest。
6. 更新 `log.md`。

### `code-wiki update <專案>`
1. 比對概覽頁記錄的 commit 與上游最新 commit，列出變動的檔案。
2. 依各頁 frontmatter 的 `sources` 找出受影響的頁面，列給使用者確認。
3. 只重寫受影響的頁面並重新驗證出處，更新各頁 `commit` 與 `updated`。
4. 更新 `index.md`、`log.md`。

## log.md 格式

```
## [YYYY-MM-DD] ingest | Clean Code 03 函式
- 更新：[[Clean Code 摘要]]、[[函式只做一件事]]
- 新增：[[Robert C. Martin]]
```
動作類型：`setup`、`ingest`、`update`（修正既有 wiki 頁）、`query`、`lint`、`new`、`code-wiki`、`code-wiki-update`、`issue`。

## 書籍類別（category）

商業與創業、個人成長、品牌與行銷、職場工作、閱讀筆記與寫作、
投資理財、人文與科學、提高生產力、自傳與小說、程式設計與技術

## 閱讀狀態（status）

想讀、閱讀中、已讀、重讀、參考書
