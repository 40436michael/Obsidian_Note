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
wiki/
  index.md        所有 wiki 頁面的目錄
  log.md          操作紀錄（只新增，不修改舊紀錄）
  books/          <書名> 摘要.md
  projects/       <專案> 摘要.md
  concepts/       跨來源的概念
  people/         作者與人物
  syntheses/      從提問得到、值得保存的比較與分析
Templates/        Templater 模板（使用者手動建立筆記用）
書單.base          書單總表（Obsidian Bases）
```

開源專案的原始碼 clone 在 vault 外（例如 `C:\Users\michael\code\<專案>`），
不要把原始碼放進 vault。

## 命名規則

- Obsidian 以檔名連結，檔名必須全 vault 唯一。
- 章節筆記前綴書名：`Clean Code 03 函式`；原始碼筆記前綴專案名。
- wiki 書籍／專案頁加「摘要」：`Clean Code 摘要`。
- 概念頁用中文命名，英文原名放在 `aliases`。

## Wiki 頁面格式

每頁都有 frontmatter：

```yaml
---
type: book-summary | project-summary | concept | person | synthesis
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
1. 讀對應的 raw 筆記（原始碼筆記需要時也讀本機的原始碼）。
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

### `新書 <書名>` / `新專案 <專案名>`
依 `Templates/` 的格式在 `raw/` 建立資料夾與資訊卡（frontmatter 填好已知資訊，其餘留空）。

## log.md 格式

```
## [YYYY-MM-DD] ingest | Clean Code 03 函式
- 更新：[[Clean Code 摘要]]、[[函式只做一件事]]
- 新增：[[Robert C. Martin]]
```
動作類型：`setup`、`ingest`、`query`、`lint`、`new`。

## 書籍類別（category）

商業與創業、個人成長、品牌與行銷、職場工作、閱讀筆記與寫作、
投資理財、人文與科學、提高生產力、自傳與小說、程式設計與技術

## 閱讀狀態（status）

想讀、閱讀中、已讀、重讀、參考書
