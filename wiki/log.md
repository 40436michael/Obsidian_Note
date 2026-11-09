---
type: log
---
# 操作紀錄

> 只在尾端新增，不修改舊紀錄。格式見 [[CLAUDE]]。

## [2026-10-17] setup | 建立知識庫結構
- 新增：`CLAUDE.md`、`Templates/`（書籍、章節、專案、原始碼筆記模板）、`書單.base`
- 新增：[[Clean Code]] 書籍資訊卡

## [2026-10-17] setup | 新增 Code Wiki 規則
- 更新：`CLAUDE.md` 新增「Code Wiki」章節（`code-wiki`、`code-wiki update`、頁面格式、出處驗證）
- 更新：原始碼預設線上閱讀，clone 前需使用者同意；`wiki/projects/` 改為每專案一個資料夾
- 更新：`Templates/專案模板.md` 本機路徑改為選填

## [2026-10-17] setup | Code Wiki 改為以學習與貢獻為目的
- 更新：`CLAUDE.md` code wiki 改為「用到再寫」，新增 02 貢獻指南頁與 `issue` 流程
- 更新：clone 規則分為學習（線上讀）與貢獻（同意後 clone）；處理 issue 時程式碼由使用者寫

## [2026-10-18] ingest | Clean Code 01 無瑕的程式碼
- 新增：[[Clean Code 摘要]]、[[童子軍規則]]、[[技術債]]、[[Robert C. Martin]]
- 更新：[[index]]

## [2026-10-18] update | Clean Code 改為第二版
- 更新：[[Clean Code 摘要]] 書籍資訊與章節表改為第二版（37 章、四部分、附錄辯論）；[[Robert C. Martin]] 著作表

## [2026-11-01] new | Coding Interview Patterns
- 新增：[[Coding Interview Patterns]] 書籍資訊卡（狀態：想讀）

## [2026-11-01] ingest | Clean Code 02 清理你的程式碼
- 新增：[[先讓它能動再讓它正確]]
- 更新：[[Clean Code 摘要]]、[[童子軍規則]]、[[index]]

## [2026-11-06] setup | 章節與書籍模板改版
- 更新：`Templates/章節模板.md` 加入各段提示、引文頁碼、`pages` 屬性、「書中提到的資源」，必填段落排前面，`chapter` 加引號
- 更新：`Templates/書籍模板.md` 新增 `pages`、「最值得記住的一句話」；[[使用指南]] 同步

## [2026-11-06] update | 章節模板精簡
- 更新：`Templates/章節模板.md` 移除 `pages` 屬性與「書中提到的資源」段落；[[使用指南]] 同步

## [2026-11-06] new | System Design Interview
- 新增：[[System Design Interview]] 書籍資訊卡（狀態：想讀）

## [2026-11-10] setup | 通用章節模板與學習機制
- 更新：`Templates/章節模板.md` 改為通用模板：核心段落＋6 種章節類型（原則／觀念、案例、教科書／理論、實作／教學、敘事、其他），新增 `chapter_type`
- 更新：`Templates/書籍模板.md` 新增「讀完想產出什麼」、評分說明、精讀／略讀提示
- 更新：`CLAUDE.md` 新增概念頁格式（以使用者原話為主）、寫作規則 8–11、ingest 挑戰問題、`複習`／`挑戰`／`回顧` 指令、章節類型表；lint 孤立頁面改為提醒
- 更新：[[使用指南]]（15 分鐘看結構、精讀／略讀、範例筆記、評分量表）、[[README]]
- 參考：《如何閱讀一本書》、vaultorial/obsidian-templates、閱讀前哨站
