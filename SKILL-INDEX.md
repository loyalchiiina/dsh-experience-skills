# SKILL-INDEX — 共享技能包注册表

> 本文件是 `~/.codex/skills`（Codex / OpenCode / Hermes / LobsterAI / DSH 五端共享）的**唯一索引**。
> 新技能必须先在本表登记，再投入使用。治理规则由 `skill-organizer` 与 `shared_skill_sync.py` 共同执行。

## 一、命名规范（前缀 = 域，后缀 = 层级）

- **前缀标"域"**：`fluent-*`（CFD）、`codex-*`（Codex）、`hermes-*`（Hermes）、`excel-*`（表格）、`stock-*`（股票）、`voice-*`（语音）……
- **后缀标"层级"**（同一域内）：
  | 后缀 | 含义 | 例子 |
  |---|---|---|
  | （无后缀/分项直名） | 阶段分项 | `fluent-mrf-torque`、`fluent-pbm-export` |
  | `-law` | 铁律（不可违） | `fluent-process-approval-law` |
  | `-discipline` | 纪律（命名/保存/步骤规范） | `fluent-case-save-discipline`、`fluent-step-plan-discipline` |
  | `-workflow` | 总流程入口 | `fluent-muti-rpm-equal-air-workflow2` |
  | `-monitor` | 监控/看门狗 | `fluent-operation-monitor` |
  | `-troubleshooting` | 故障经验库 | `fluent-run-failure-troubleshooting` |
  | `-reference` / `-quick-reference` | 路由/速查 | `fluent-quick-reference` |
- **命名硬规则**（Codex 格式，五端统一）：`name == 目录名`、小写字母数字连字符、无 UTF-8 BOM、有 `description`。

## 二、域索引（域 → 前缀 → 入口/路由技能）

| 域 | 前缀 | 入口/路由技能 |
|---|---|---|
| Fluent/CFD | `fluent-*`、`ansys-*`、`pbm-*`、`torque-*` | 唯一入口 `fluent-control-laws` → 路由 `fluent-quick-reference` → 知识库 `fluent-cfd` |
| SpaceClaim/几何 | `spaceclaim-*` | `spaceclaim-stirrer-tank-geometry-params`（搅拌釜尺寸识别/几何参数提取，网格前必先汇报几何信息）；引用关系见 `SKILL-REFERENCES.md` |
| Codex | `codex-*` | `codex-core-skill-sync`（同步/兼容） |
| Hermes | `hermes-*` | `hermes-config` |
| DSH/LobsterAI | `dsh-*`、`lobster-*`、`skin-*` | `dsh-lobsterai-integration`（运行/积分/技能库接入）；`dsh-desktop-config`（桌面端 2.0+ 安装/升级/profile 切换经验库，经验台账 EXPERIENCE-LOG.md 持续更新）；`dsh-taskboard-create`（对话/需求自动整理格式 → UIA 注入 GUI 任务看板，创建/执行）；`dsh-message-push`（QQ+微信双通道消息推送，任意内容远程推送，2026-08-16 由 dsh-qq-report 泛化而来）；`dsh-taskboard-recovery`（任务看板记录丢失排查恢复：端口漂移致 localStorage origin 隔离，leveldb 解析提取 + 固定端口修复，2026-08-16 建） |
| Excel/表格 | `excel-*`、`xlsx` | `excel-generation-standard`（统一走 spreadsheets 插件；PBM 例外走 `pbm-data-analysis`）；交付前显示校验 `excel-display-verify` |
| 语音/媒体 | `voice-*`、`volcengine-*`、`seedance`、`seedream` | `voice-alert`（提醒）、`voice-input-and-tts`（朗读） |
| 图片/视觉 | `image-*`、`markdown-to-image`、`code-explanation`、`canvas-design`、`frontend-design` | 按具体任务直取 |
| 文档 | `docx`、`pdf`、`pptx`、`xlsx` | 按文件类型直取 |
| 股票 | `stock-*` | `stock-analyzer`（唯一入口：analyze 深度报告 / quote 快速行情，合并自 stock-explorer）、`stock-announcements`（公告） |
| 搜索/资讯 | `web-search`、`daily-trending`、`technology-news-search`、`media-search`（影视+音乐，合并自 films-search+music-search） | 按内容类型直取 |
| 数据分析/可视化 | `analyze`、`explore-data`、`create-viz`、`build-dashboard`、`data-visualization`、`statistical-analysis`、`validate-data`、`write-query`、`sql-queries` | 问答入口 `analyze`、画图入口 `create-viz`、SQL 入口 `write-query`；`sql-queries`/`data-visualization`/`statistical-analysis` 为 user-invocable: false 参考库 |
| 系统/工具 | `windows-close-other-windows`、`windows-desktop-setup`、`windows-junk-cleanup`、`local-tools`、`browser-favorites-organize`、`archive-generator`、`download-mirror-first`、`weather`、`printer-driver-install`、`github-publish`（上传/发布到 GitHub，2026-08-16 建，配套 DSH 预设 github-publisher） | 按任务直取：压缩→`archive-generator`、垃圾清理→`windows-junk-cleanup`、关闭任务栏其他窗口→`windows-close-other-windows`、天气→`weather`、上传/发布到 GitHub→`github-publish` |
| 邮件/笔记 | `imap-smtp-email`、`youdaonote` | 按工具直取 |
| 设计/UX | `design-critique`、`design-handoff`、`design-system`、`ux-copy`、`accessibility-review` | 按场景直取（评审/交付/规范/文案/无障碍） |
| 内容/研究 | `article-writer`、`content-planner`、`research-synthesis`、`user-research` | 按场景直取 |
| 开发 | `develop-web-game`、`playwright`、`remotion`、`hatch-pet`、`frontend-design`、`computer-use` | 按场景直取 |
| Token/输出治理 | `concise-output-discipline`（总纲·唯一入口）、`caveman`（语气主场）、`deepseek-v4-flash-token-saver`（省 token 策略）、`new-topic-new-session` | 默认全局极简→`concise-output-discipline`（2026-08-15 建，DSH 默认预设 standard-concise 与 Codex AGENTS.md 已内联引用）；极简腔调规则→`caveman`（lite/full/ultra/文言文，2026-08-15 安装自 yibie/caveman-codex，已核验）；省 token 行为→`deepseek-v4-flash-token-saver`；话题切换提醒→`new-topic-new-session` |
| 技能治理 | `skill-*`、`codex-core-skill-sync` | **`skill-master`（技能生成与管理大师·总纲，唯一入口）** → `skill-organizer`（整理流程）/ `skill-creator`（创建）/ `skill-vetter`（安全）/ `skill-packaging`（打包）→ 本索引 |

## 三、Fluent 域层级明细（用户主域）

- **入口/总纲**：`fluent-control-laws`（唯一入口）、`fluent-quick-reference`（路由）、`fluent-cfd`（知识库）
- **铁律**：`fluent-process-approval-law`（进程审批/暂停三次确认/无人值守时段判定）
- **纪律**：`fluent-case-save-discipline`（保存命名）、`fluent-step-plan-discipline`（分步安排）
- **总流程**：`fluent-muti-air-equal-rpm-workflow1`（同转速多通气量 PBM）、`fluent-muti-rpm-equal-air-workflow2`（多转速相同通气量）
- **分项**：`fluent-mrf-torque`、`fluent-aeration-stabilization`、`fluent-pbm-calculation`、`fluent-pbm-export`、`fluent-setfile-management`、`fluent-session-connect`、`fluent-gui-open`、`fluent-animation-organization`、`fluent-case-backup`、`fluent-mesh-packaging`、`fluent-meshing-automation`、`fluent-meshing-project-a-workflow2`、`fluent-meshing-project-b-workflow1`、`fluent-junk-cleanup`、`fluent-liquid-surface-volume-query`、`fluent-shear-analysis`、`fluent-data-postprocess-comparison`
- **监控/进程**：`fluent-operation-monitor`（看门狗）、`fluent-midrun-save`（密码/中间保存）、`fluent-detached-process-rule`（独立进程启动，禁挂 DSH job）
- **预防/前置**：`fluent-path-check`（路径空格）、`fluent-run-continuity`（续算对齐）、`fluent-prev-run-vdisplay-cleanup`（关虚拟显示）
- **故障**：`fluent-run-failure-troubleshooting`（通用判断经验库，案例下沉 references）
- **数据/通用**：`pbm-data-analysis`、`torque-power-compare`、`ansys-local-workflows-skill`

## 四、新技能收尾三步（强制，写进 skill-organizer）

1. **选对前缀+后缀**：判定所属域与层级，按本表命名（如 `fluent-xxx-law` / `-discipline` / `-workflow` / `-monitor` / `-troubleshooting` / 分项直名）。
2. **登记进本索引**：在对应域加一行，标入口/路由。
3. **补进路由技能**：更新该域路由技能（如 `fluent-quick-reference`）的阶段表；给 description 写触发词（统一"触发词：…"，**禁 ASCII 冒号 `: `**）。

## 五、7 类病根 → 统一解法（治理经验）

| 病根 | 统一解法 |
|---|---|
| ① 数值口径打架（同一参数多处、数值不一） | 只留一处权威，别处引用 |
| ② 重复定义（同一规则抄 N 份） | 收敛到"总纲/主场"，别处改引用 |
| ③ 引用断链/悬空（名字错、文件缺、frontmatter 坏） | 全库扫描 + 修名 + 补 frontmatter |
| ④ 别名/空壳（转发壳、冗余子技能） | 归档到 `skills-archive` + 台账标"已归档" |
| ⑤ 触发/路由不灵（无触发词、多入口、漏收） | 唯一入口 + 触发词规范 + 路由补录 |
| ⑥ 硬编码/项目耦合（项目数值写进正文） | 下沉 references + "示例"标注 |
| ⑦ 治理缺位（无登记、无索引、归档不彻底） | 本索引 + 同步层归档豁免 |

## 六、归档豁免（治本，杜绝"复活"）

- 归档目录 `~/.codex/skills-archive` 里的技能，`shared_skill_sync.py` 摄入时**一律跳过**（`SKIP-ARCHIVED`）。
- 移除技能 = 移到 `skills-archive` + 台账标"已归档" + 从本索引删除 → 同步不会再复活。

## 七、已核验 · 跳过整理检查（非 Fluent，2026-08-14 批次）

> 以下 83 个非 Fluent 技能已于 2026-08-14 完成全量整改与五端兼容验证（119 技能 incompatible=0、frontmatter 0 失败）。
> **下次整理/检查时跳过全量复查**；标注 ⚠待办 的技能仅复查对应待办项，不重复全量检查。

**⚠待办（仅查待办项）：**
- `docx` — ooxml/ 工具链待抽 `shared/ooxml`（与 pptx 双副本）
- `pptx` — ooxml/ 工具链待抽 `shared/ooxml`；转图流程依赖 docx

**✅ 健康（直接跳过检查）：**
accessibility-review、analyze、archive-generator、article-writer、browser-favorites-organize、build-dashboard、canvas-design、chinese-patent-download、code-explanation、codex-config-backup-law、codex-core-skill-sync、codex-deepseek-direct、codex-green-unread-theme、codex-plugin-zh-localize、computer-use、content-planner、create-plan、create-viz、daily-trending、data-context-extractor、data-visualization、deepseek-v4-flash-token-saver、design-critique、design-handoff、design-system、develop-web-game、download-mirror-first、dsh-lobsterai-integration、excel-charts、excel-display-verify、excel-generation-standard、excel-incremental-update、explore-data、export-highlight-file、file-path-clickable、frontend-design、hatch-pet、hermes-config、hermes-drive-migration、hermes-voice-setup、image-download、image-recognition、imap-smtp-email、lobster-skin-injector、local-tools、love-poem-reader、markdown-to-image、media-search、new-topic-new-session、opencode-install-windows、pdf、playwright、printer-driver-install、remotion、research-synthesis、seedance、seedream、skill-creator、skill-organizer、skill-packaging、skill-vetter、skin-creator、sql-queries、statistical-analysis、stock-analyzer、stock-announcements、technology-news-search、user-research、ux-copy、validate-data、voice-alert、voice-input-and-tts、volcengine-media-gen、volcengine-media-suite、volcengine-voice-clone、weather、web-search、windows-desktop-setup、windows-junk-cleanup、write-query、xlsx、youdaonote

> 说明：① `codex-green-unread-theme` 与 `lobster-skin-injector` **保持独立、永不合并**（2026-08-14 用户决定），仅保留互指路由。② Fluent/CFD 域（fluent-*/ansys-*/pbm-*/torque-*）不在此清单内，单独按 Fluent 流程管理。③ 清单内技能若出现新增问题/新增矛盾，重新纳入检查并更新本清单。
