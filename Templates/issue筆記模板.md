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
---
# <% project %> <% id %>

## 問題
<!-- 這個 issue 要解決什麼？用自己的話寫一兩句 -->


## 怎麼查的
<!-- 讀了哪些檔案、KIP、相關 issue／PR；用了哪些指令（例：git log -S） -->


## 決定與理由
<!-- 考慮過哪些做法，最後選哪個，為什麼。寫你自己相信的理由 -->


## 改了什麼
<!-- 改了哪些檔案、加了哪些測試，寫重點就好，不用貼整段程式碼 -->


## 踩到的坑
- 

## Review 回饋
<!-- reviewer 說了什麼，你怎麼回應或修改 -->


## 下次會怎麼做
- 
