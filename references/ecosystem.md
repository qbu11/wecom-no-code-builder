# 企微 Agent Skill 生态（2026-09 核实）

在 skill 生态里搜 `wecom`，出来的**全是腾讯官方的 wecom-cli 系列**，装机量 1.6–2.1 万。

它们是**能力型** skill——让 agent 直接调用企微 API 去操作表格、待办、消息。
**本 skill 是引导型**（教人手工搭）。两者互补，不是一回事。

---

## 官方能力型 skill 清单

| skill | 用途 |
|---|---|
| `wecomcli-shared` | 公共前置检查：CLI 安装 / 版本 / 授权状态 |
| `wecomcli-contact` | 通讯录：按姓名 / 拼音 / 别名搜人 |
| `wecomcli-calendar` | 日程 |
| `wecomcli-meeting` | 在线会议（含会议号、入会链接）+ 纪要转写 |
| `wecomcli-todo` | **待办增删改查** |
| `wecomcli-email` | 邮件搜索与读取（不支持发送） |
| `wecomcli-disk` | 微盘文件 |
| `wecomcli-media` | media_id 与本地文件搬运 |
| `wecomcli-message` | 向机器人会话推送消息 |
| `wecomcli-doc-manage` | 文档搜索 / 改名 / 权限（跨类型） |
| `wecomcli-doc` | 在线文档正文读写 |
| `wecomcli-sheet` | 在线表格 |
| `wecomcli-smartsheet` | **智能表格**：子表 / 字段 / 记录 / 视图 / 图表 |
| `wecomcli-smartpage` | 智能文档 |

> 清单以实际跑 `npx skills add WeComTeam/wecom-cli --list` 的输出为准（2026-09 实测 14 个）。
> 头部几个的装机量在 1.6–2.1 万区间。

安装：`npx skills add wecomteam/wecom-cli`

### 另外两条相邻路线

- **`WecomTeam/wecom-unified`**（119★）与 **`wecom-openclaw-plugin`**（472★）——
  官方同生态仓库，前者能力全覆盖，后者是 OpenClaw 插件
- **`OmniSocKit/Open-Wecom-Skills`**（30★ / Apache-2.0）——**41 个 skill、550+ API**，
  是给**开发者**用的企微开发知识体系（Python/TS/Go/Java/PHP 代码模板 + 踩坑指南），
  也提供 MCP 接入。跟非技术用户无关，但要做深度集成时是好资料

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
