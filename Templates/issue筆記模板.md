<%*
const project = tp.file.folder();
const id = await tp.system.prompt("issue 編號（Jira 例：KAFKA-21500；GitHub 例：issue-123）");
const url = await tp.system.prompt("issue 網址");
await tp.file.rename(`${project} ${id}`);
-%>
---
type: issue-note
project: "[[<% project %>]]"
issue: <% url %>
pr:            # 送出 PR 後填網址
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
<!-- 邊做邊寫，不要等做完才回想。每天一個日期標題，記下查了什麼、試了什麼、卡在哪。
     附證據：檔案路徑、commit、PR、KIP 的連結或指令。
     走錯的路也留著，加上「後來發現…」，那是最好的學習材料 -->
### <% tp.date.now("YYYY-MM-DD") %>
- 

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
