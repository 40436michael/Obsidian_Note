# Obsidian_Note

我的個人知識庫：讀書筆記、開源專案的學習與貢獻紀錄。

採用 [LLM Wiki](https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f) 模式：**我自己寫原始筆記，Claude Code 負責把它們整理成互相連結的 wiki**。Obsidian 用來閱讀和瀏覽，Claude Code 用來整理和維護。

## 資料夾結構

```
raw/                  我寫的原始筆記（Claude 只讀不改）
  books/<書名>/        書籍資訊卡 + 章節筆記
  articles/           網路文章
  projects/<專案>/     專案資訊卡 + 原始碼筆記 + issue 筆記
wiki/                 Claude 維護的 wiki（我只看不寫）
  index.md            所有頁面的目錄
  log.md              操作紀錄
  books/              書籍摘要
  projects/<專案>/     code wiki（概覽、快速開始、貢獻指南、各主題）
  concepts/           跨書、跨專案的概念
  people/             作者與人物
  syntheses/          從提問得到的比較與分析
Templates/            Templater 模板
書單.base              書單總表
CLAUDE.md             給 Claude 的規則（結構、格式、操作流程）
```

完整規則見 [CLAUDE.md](CLAUDE.md)。

## 讀書流程

1. **新增一本書**：新增筆記，套用「書籍模板」，依提示輸入書名、類別、狀態、作者。筆記會自動搬到 `raw/books/<書名>/`。
2. **讀完一章**：在該書的資料夾新增筆記，套用「章節模板」，輸入編號和章名。用自己的話寫「一句話總結」和「我的想法」。
3. **整理進 wiki**：對 Claude 說 `ingest <書名> <章節編號>`，例如 `ingest Clean Code 03`。Claude 會先列出重點和要更新的頁面，確認後才寫入。
4. **查看書單**：打開 `書單.base`，可以切換「全部／閱讀中／想讀／依類別」四個檢視。

## 開源專案流程

| 想做什麼 | 對 Claude 說 | 會發生什麼 |
|---|---|---|
| 開始認識一個專案 | `code-wiki <repo 網址>` | 規劃 code wiki 目錄，確認後先寫概覽、快速開始、貢獻指南三頁 |
| 深入某個主題 | `寫 <頁面名稱>` | 補寫該主題頁和需要的子頁 |
| 專案有更新 | `code-wiki update <專案>` | 比對 commit，只更新受影響的頁面 |
| 處理一個 issue | `issue <issue 網址>` | 找出相關程式碼、提出修法和取捨；**修改由我自己寫**，Claude 負責 review |

原始碼預設在線上閱讀；要貢獻而需要 clone 時，Claude 會先徵求同意，並放在 vault 以外的地方。

## 其他指令

| 指令 | 用途 |
|---|---|
| 直接提問 | Claude 先查 `wiki/index.md` 再回答並附出處；值得保存的答案可存進 `wiki/syntheses/` |
| `lint` | 健康檢查：矛盾、孤立頁面、缺少的概念頁、尚未 ingest 的筆記、過時的 code wiki |
| `新書 <書名>` / `新專案 <專案名>` | 由 Claude 建立資訊卡 |

## 環境設定

**插件**
- 社群插件：Templater、Obsidian Git、Excalidraw、Omnisearch、Advanced Tables
- 核心插件：Bases（書單總表）

**設定**
- Templater → Template folder location：`Templates`
- 快捷鍵：`Templater: Open insert template modal` 綁定 `Alt+E`

**同步**
Obsidian Git 會在停止編輯 10 分鐘後自動 commit 並推送到 GitHub。`.obsidian/workspace*.json`、`.trash/`、系統暫存檔已列入 `.gitignore`。

**在新電腦上使用**
1. clone 這個 repo，用 Obsidian 開啟資料夾。
2. 在「設定 → 社群插件」啟用社群插件（插件程式碼已在 repo 中）。
3. 用 Claude Code 開啟同一個資料夾，Claude 會自動讀取 `CLAUDE.md`。
