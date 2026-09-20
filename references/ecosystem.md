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

## 和本 skill 的关系：能自动化的就自动化掉

主路径**不是固定的**，取决于用户有没有能力：

| 用户的能力 | 你该怎么做 |
|---|---|
| 装了 CLI + 有机器人凭证 | **直接读表、改表、建视图、建待办**——用户基本不用动手 |
| 缺一部分 | 告诉他补什么，补完再继续 |
| 都没有 | 退化成教练模式：你指路、他手点 |

引导型能力和执行型能力**不冲突**。目标是让用户**能自己改**，
而不是让他**必须亲手搭**——**能自动化的就自动化掉**。

（唯一要记得的是：不管谁动手，表的结构设计原则是一样的，
见 `field-schema.md`。）
