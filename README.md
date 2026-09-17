# Codex 创意视频剪辑标准

把一次真正认可的剪辑效果，沉淀成以后可以重复使用、持续优化的 Codex Skill。

这不是独立剪辑软件，也不自带素材库或一键渲染引擎。它指导 Codex 使用已安装、已授权且实际可操作的剪映、ChatCut 等工具，完成剪辑、原生包装、导出检查和交付。

**当前版本：1.0.0。仓库默认私有，文档与技能说明均使用中文。**

## 解决什么问题

- 不再只把口播拼起来，加一层普通静态字幕就交付。
- 长辅助素材先按语义筛选，再精确插入口播，不只看开头或整段堆进去。
- 真正使用原生动态字幕、重点花字、贴纸、BGM、音效和必要转场，并验证导出效果。
- 检查字幕尾词、人物遮挡、镜头接缝、音乐与人声关系，减少“工程看着对，导出有问题”。
- 区分已导出、技术检查、完整视听检查、用户认可和商业用途适用性。

## 默认标准

|维度|要求|
|---|---|
|叙事与声音|真实口播为主线，保留核心原词与原声，不擅自换配音或加速|
|字幕与花字|清晰有层级、动效克制，尾词显示完整，移动端可读|
|辅助镜头|按讲述内容挑片段，避开脸、嘴、字幕及关键产品信息|
|贴纸与音效|围绕疑问、转折、证据或动作使用，不机械凑数|
|BGM|根据当前人声重新混音，低位铺底、进出平顺|
|导出与验片|检查实际完整文件，不能仅凭设置、静帧或媒体头信息宣称验收通过|
|交付边界|不添加无关水印，不自动发布、付费或向未授权目标发送|

复用的是质量，不是固定片长、相同贴纸、同一首配乐或某组增益参数。用户当次的明确要求优先；只截取、转码等窄任务不会被强行加上全套包装。

## 仓库结构

```text
README.md
CHANGELOG.md
skills/
  creative-video-editing/
    SKILL.md
    agents/openai.yaml
    references/
      quality-standard.md
      native-editor.md
      approved-baseline.md
```

- [技能入口](skills/creative-video-editing/SKILL.md)：触发范围、制作路线与交付规则。
- [质量与验片标准](skills/creative-video-editing/references/quality-standard.md)：镜头、字幕、声音及验收清单。
- [原生编辑器执行要点](skills/creative-video-editing/references/native-editor.md)：工程核对、前台操作和坐标失效处理。
- [脱敏基准](skills/creative-video-editing/references/approved-baseline.md)：已认可案例的方法、可调参数和失败经验。

## 安装

私有仓库需要登录有访问权限的 GitHub 账号。可直接对 Codex 说：

```text
使用 skill-installer 安装我的私有仓库
xuliang0147/codex-video-editing-skills
中的 skills/creative-video-editing。
如已有同名技能，先比较并备份，不直接覆盖本机定制。
不要修改其他技能或上传本机素材。
```

在已有 Codex 系统技能的 macOS/Linux 环境，也可使用官方安装脚本：

```bash
python3 "${CODEX_HOME:-$HOME/.codex}/skills/.system/skill-installer/scripts/install-skill-from-github.py" \
  --repo xuliang0147/codex-video-editing-skills \
  --path skills/creative-video-editing \
  --method git
```

安装器遇到已有同名目录会停止，不会自动覆盖。默认安装位置为 `$CODEX_HOME/skills/creative-video-editing`，未设置 `CODEX_HOME` 时为 `~/.codex/skills/creative-video-editing`。安装后下一轮可使用技能；已有长任务建议明确要求重新读取。

## 使用示例

```text
使用 $creative-video-editing 剪辑这批口播素材。
主讲保留原声，辅助视频较长，请筛选真正对应口播的片段。
按原生动态字幕、重点花字、适量贴纸、BGM和音效做完整片。
直接交完整成片，不增加样段审批，不发布，不添加无关水印。
```

要在所有项目默认使用，可在自己的全局或项目 `AGENTS.md` 中加入以下规则，并填写实际安装路径；本仓库不会自动修改全局文件：

```text
视频剪辑、返修和验片前，读取已安装的 creative-video-editing/SKILL.md。
编导派发时携带技能路径和版本，剪辑制作与编导验片沿用同一标准。
当前明确需求优先，纯截取和转码不强加包装。
```

## 工具与授权

- 需要实际可操作的剪辑工具及当前有效授权。技能安装不等于剪映/ChatCut 已连通，也不保证任意设备可全自动完成。
- FFmpeg 可用于精切、转码和技术检查；明确要求原生预设时，不能用代码烧字或生成音调冒充。
- 涉及生成或修改图片时遵循环境中的 `$imagegen` 规则；当前未具备能力时明确报告，不静默换成代码绘图。
- 不自带音乐、字体、贴纸或商业授权。“免费可导出”不等于可商用；内部效果比较授权不自动延续到下一项任务。
- 未接入多角色协作的个人任务可直接执行，不需要另建编导或注册系统。

## 后续怎么优化

给 Codex 指出具体差异，例如：

```text
优化 creative-video-editing skill：以后重点花字减少，字幕保持完整，
音效只用于转折和关键演示。这是通用默认，不仅针对当前视频。
先备份，再更新同一份技能、版本号和变更说明。
```

仅针对某条视频的修改不会默认扩大为全局标准。更新后应同步给正在执行任务的编导和剪辑，并明确要求读取新版本。**更新本机技能不自动推送 GitHub；需要同步时再明确提出。**

## 隐私与验证范围

仓库只包含脱敏技能、中文说明和通用经验，不包含原视频、人物素材、工程缓存、账号凭据、飞书标识、个人本机路径或完整全局配置。本机个性化版本保持独立，不因仓库发布而被覆盖。

本版本已做技能格式校验、链接/资源存在性检查，以及完整片、窄截取、有限视听能力三种决策场景检查。检查的是技能与执行原则，不代表在每种剪辑软件上都已端到端验收，也不承诺输出效果完全相同。
