# 五端共用技能库（Shared Skill Library for Codex / OpenCode / Hermes / DSH / LobsterAI）

一份技能库，五个工具共用。把 AI 技能（`SKILL.md`）做成单一共享根目录，Codex、OpenCode、Hermes、DSH、LobsterAI 五端同时读取——**新增/修改技能只需改一处，五端立即生效**，不再每端复制一份导致漂移。

本仓库分享这套**经验与做法**（不是技能文件本身）：架构、各端接入方式、治理机制与踩坑清单。

## 为什么共用

- **单点维护**：一份技能库，五端读取。改一次，全部生效，避免多份副本内容漂移。
- **统一规范**：全部技能遵循 Codex 技能格式（`name == 目录名`、frontmatter 带 `description`、无 BOM），五端原生加载，互不转换。
- **治理集中**：一个注册表（`SKILL-INDEX.md`）+ 一套治理流程（命名规范、触发词、归档豁免），杜绝重复定义与断链。

## 架构

```
                       ┌─────────────────────────────┐
                       │  共享技能根（单一目录）       │
                       │  SKILL.md × N（Codex 格式）  │
                       │  SKILL-INDEX.md（唯一索引）  │
                       └─────────────────────────────┘
        Codex 直接读取      OpenCode 直接读取      Hermes junction 链接
        DSH customSkillDirs 指向        LobsterAI 技能/网关共用
```

### 各端接入方式

| 端 | 接入方式 | 说明 |
|---|---|---|
| Codex | 直接指向技能目录 | 原生支持 Codex 格式技能 |
| OpenCode | 直接读取同一目录 | 与 Codex 共用同一份文件 |
| Hermes | **junction 链接** | 目录链接到共享根，保持单份文件（迁移/换盘后重建 junction） |
| DSH | `skill-filesystem` 的 `customSkillDirs` 指向 | profile patch 配置，DSH 启动/运行中实时扫描，新增技能即时可见 |
| LobsterAI | 技能库/模型网关共用 | 与 DSH 同源读取 |

## 关键机制

- **`SKILL-INDEX.md`（唯一注册表）**：域索引（`fluent-*`/`codex-*`/`hermes-*`/`dsh-*`…）、命名规范（前缀=域、后缀=层级）、7 类病根治理、归档豁免清单。新技能必须先登记再投入使用。
- **同步与兼容校验**：`codex-core-skill-sync` 技能负责外部新增技能自动摄入与规范化，生成五端兼容性报告（frontmatter 0 失败、incompatible=0）与带时间的更新台账。
- **治理总纲**：`skill-master`（唯一入口）→ `skill-organizer`（新增/整理流程）→ `skill-creator`（创建）→ `skill-vetter`（安全审查）→ `skill-packaging`（打包迁移）。
- **归档豁免**：归档技能移入 `skills-archive/` 并在索引中删除，同步层跳过归档目录，防止"复活"。

## 踩坑经验（五端兼容的关键）

1. **命名硬规则**：`name == 目录名`、小写字母数字连字符、**无 UTF-8 BOM**——这是五端兼容的前提，BOM 会导致部分端解析失败。
2. **触发词规范**：description 统一写「触发词：…」且**禁 ASCII 冒号**（`name: xxx: yyy` 会破坏 YAML frontmatter，技能直接不可见）。
3. **PowerShell 5.1 中文脚本必须 UTF-8 BOM**（`WriteAllText(..., (New-Object System.Text.UTF8Encoding $true))`）；任何编辑工具写回后需重新补 BOM。
4. **DSH 技能库实时扫描**：新增技能到共享根后，DSH 会话内即时可见，无需重启；预设/插件类配置变更才需要重启 `dsh web`。
5. **Hermes 用 junction**：`junction <hermes技能路径> <共享根>`，避免真复制导致的双份漂移。
6. **校验自动化**：全库 frontmatter 扫描脚本（`name==目录名`、有 `description`、无 BOM）应纳入收尾步骤，保证 0 失败再交付。

## 快速开始

1. 建技能根目录，按 Codex 格式写第一个 `SKILL.md`（frontmatter 三件套：`name`/`description`/正文）。
2. 登记进 `SKILL-INDEX.md` 对应域行。
3. 各端接入：
   - DSH：在 `~/.dsh/profiles/<profile>/cordis.patch.yml` 配置 `skill-filesystem.customSkillDirs` 指向共享根。
   - Hermes：建 junction 指向共享根。
   - Codex / OpenCode：直接指向共享根。
4. 运行 `codex-core-skill-sync` 校验五端兼容（frontmatter 0 失败 + incompatible=0）。
5. 新增/修改技能只需动共享根一处，五端自动生效。

## 附

- `SKILL-INDEX.md` — 本方案所依托的完整注册表样例（脱敏版，展示域索引与治理结构）。
- 本仓库仅分享经验文档，不含技能文件本体；技能文件请自行维护在各自共享根。

## License

MIT
