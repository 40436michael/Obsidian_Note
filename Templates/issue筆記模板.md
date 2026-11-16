<%*
// 專案：在 raw/projects/<專案>/ 裡建立就自動帶入，否則從現有專案選
const projectFolders = (app.vault.getAbstractFileByPath("raw/projects")?.children ?? [])
  .filter(f => f.children).map(f => f.name);
let project = tp.file.folder(true).match(/^raw\/projects\/([^/]+)$/)?.[1];
if (!project) {
  if (projectFolders.length === 0) {
    new tp.obsidian.Notice("還沒有任何專案，請先用「專案模板」建立專案資訊卡");
    throw new Error("no project");
  }
  project = await tp.system.suggester(projectFolders, projectFolders, true, "這個 issue 屬於哪個專案？");
}

// 編號：從網址自動判斷，判斷不出來才問
const url = ((await tp.system.prompt("issue 或 PR 網址（Jira、GitHub 都可以）")) ?? "").trim();
let id = url.match(/\/browse\/([A-Z][A-Z0-9]*-\d+)/)?.[1];          // Jira：KAFKA-21500
const gh = url.match(/github\.com\/[^/]+\/[^/]+\/(issues|pull)\/(\d+)/);
if (!id && gh) id = `${gh[1] === "pull" ? "pr" : "issue"}-${gh[2]}`;  // GitHub：issue-123、pr-24252
if (!id) id = await tp.system.prompt("編號（例：KAFKA-21500、issue-123、pr-24252）", "", true);
await tp.file.move(`raw/projects/${project}/${project} ${id}`);
-%>
---
type: issue-note
project: "[[<% project %>]]"
issue: <% url %>
pr: <% gh?.[1] === "pull" ? url : "" %>
status: 進行中  # 進行中、等待 review、已合併、放棄
started: <% tp.date.now("YYYY-MM-DD") %>
finished:
---
# <% project %> <% id %>

## 一句話教訓
<!-- 結案時寫。下次遇到類似的 issue，你會提醒自己什麼？一年後忘了這個 issue，還看得懂這句嗎？ -->


## 問題
<!-- 開始時寫。這個 issue 要解決什麼？用自己的話寫一兩句；看不懂的地方也寫下來 -->


## 下一步
<!-- 隨時更新，做完就打勾。例：等 ci-approved、Jira 按 Submit Patch、回覆 review -->
- [ ] 

## 過程記錄
<!-- 邊做邊寫，不要等做完才回想。每天一個日期標題（Alt+E 選「今天的記錄」會自動插入），記下查了什麼、試了什麼、卡在哪。
附證據：檔案路徑、commit、PR、KIP 的連結或指令。
走錯的路也留著，加上「後來發現…」，那是最好的學習材料 -->
### <% tp.date.now("YYYY-MM-DD") %>
- 

## AI 協助
<!-- 先自己想好假設再問 AI，問完自己驗證（讀原始碼、跑測試、查 git log、找前例）。
AI 說錯的地方一定要記：它說了什麼、實際是什麼、你怎麼發現的。
例：AI 說 Ctrl+Shift+N 被輸入法攔截 → 實際是 IntelliJ keymap 設成 VSCode → 用 Find Action 查快捷鍵發現的 -->
- ❌ AI 說錯：
- ✅ 驗證過：

## 決定與理由
<!-- 結案時寫。至少列一個「沒選的」做法，也寫這個決定的缺點。
改了哪些檔案看 PR 就好，這裡只寫「為什麼」 -->
| 選擇 | 沒選的 | 理由 |
|---|---|---|
|  |  |  |

## Review 回饋
<!-- reviewer 說了什麼、你怎麼回應。屬於這個專案的習慣，也記到專案資訊卡的「貢獻觀察」 -->


## 驗證自己
<!-- 把學到的事寫成 1–2 個問題，`複習` 時 Claude 會拿來考你。
例：「為什麼 __cluster_metadata 不在 INTERNAL_TOPICS？」 -->
1. 
