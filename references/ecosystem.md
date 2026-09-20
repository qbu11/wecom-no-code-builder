# 企微 Agent Skill 生态（2026-09 核实）

在 skill 生态里搜 `wecom`，出来的**全是腾讯官方的 wecom-cli 系列**，装机量 1.6–2.1 万。

它们是**能力型** skill——让 agent 直接调用企微 API 去操作表格、待办、消息。
**本 skill 是引导型**（教人手工搭）。两者互补，不是一回事。

---

## 官方能力型 skill 清单

| skill | 装机量 | 能力 |
|---|---|---|
| `wecomteam/wecom-cli@wecomcli-doc` | 21.6K | 文档 |
| `wecomteam/wecom-cli@wecomcli-todo` | 21.4K | **待办** |
| `wecomteam/wecom-cli@wecomcli-contact` | 21.3K | 通讯录 |
| `wecomteam/wecom-cli@wecomcli-meeting` | 21.3K | 会议 |
| `wecomteam/wecom-cli@wecomcli-smartsheet` | 16.7K | **智能表格** |
| `wecomteam/wecom-cli@wecomcli-msg` | 16.6K | 消息 |
| `wecomteam/wecom-cli@wecomcli-schedule` | 16.4K | 日程 |
| `wecomteam/wecom-unified@wecom-unified` | 11.6K | 上述全覆盖 |
| `wecomteam/wecom-cli@wecomcli-sheet` | 8.2K | 普通表格 |
| `wecomteam/wecom-cli@wecomcli-smartpage` | 8.2K | 智能页面 |
| `wecomteam/wecom-cli@wecomcli-disk` | 4.9K | 微盘 |

安装：`npx skills add wecomteam/wecom-cli`

---

## 什么时候向用户提这条路

**只在用户主动问「能不能自动」「能不能让 AI 直接帮我做」的时候提。**

而且要先讲清两个前提：

1. 需要在企微管理后台创建机器人、拿到 Bot ID + Secret —— **要管理员权限**
2. 官方口径是「优先面向 10 人及以下企业」—— **大企业能否用需要实测**

**对 100 人以上的公司，这条路先别主动推荐**（大概率用不了，白折腾）；
对小团队可以提。

---

## 一条重要的连带结论

`wecomcli-todo` 装机 21.4K，说明**企微待办是可以通过 API 创建的**。

这印证了 `automation-recipes.md` 里的判断：
**待办在「自动化流程」的动作列表里可能没有，但通过 CLI 是能建的**——这是两条不同的路。
用户以后上自动化那一层时，"到点通知到人"这个需求是通的。

---

## 对本 skill 主路径的影响：无

主路径仍然是**手动搭建**。因为目标用户是**非技术负责人**，
不该被要求配置 API 凭证。这一点不因为生态的存在而改变。

引导型 skill 和 cobble 型 skill 解决的是不同问题：
前者解决「他能不能自己改」，后者解决「能不能省掉手工」。
对非技术用户，前者优先级更高——**只有他自己能改的东西，才不会被卡住**。
