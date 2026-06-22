# Read VRC Unity Project

一个用于 Codex 的 VRC SDK Unity 项目读取 Skill。它帮助 Codex 在不破坏项目的前提下，定位 Avatar 场景、解析 Unity 资源引用，并检查 VRC Avatar 的层级和配置。

## 功能

- 识别 Unity、VRC SDK、Modular Avatar、NDMF 和 Avatar Optimizer 等版本。
- 读取 `.unity`、`.prefab`、`.asset`、`.controller`、`.anim`、`.mat` 和 `.meta`。
- 通过 `guid` 与 `fileID` 追踪场景、Prefab、菜单、参数和 Animator 引用。
- 使用 Unity 批处理模式检查真实对象层级、组件、激活状态及序列化字段。
- 区分源场景状态、Unity 解析状态和 NDMF 构建后的最终状态。
- 默认只读，不保存场景、不修改资产，也不会上传 Avatar。

## 工作方式

Skill 按三个层级读取项目：

1. **静态文件层**：快速搜索 Unity 序列化文件和 GUID 引用。
2. **Unity 对象层**：通过 Unity Editor API 展开 Prefab、读取组件和对象层级。
3. **构建结果层**：在需要确认最终行为时，检查 Modular Avatar 或 NDMF 处理后的结果。

## 安装

将整个仓库克隆或解压到 Codex 的全局 Skills 目录：

```text
%USERPROFILE%\.codex\skills\read-vrc-unity-project
```

使用 Git 克隆的 PowerShell 示例：

```powershell
git clone https://github.com/USER/read-vrc-unity-project.git `
  "$env:USERPROFILE\.codex\skills\read-vrc-unity-project"
```

安装完成后，新开 Codex 会话。确保上述目录中直接包含 `SKILL.md`，不要多嵌套一层压缩包目录。

## 使用

显式调用：

```text
$read-vrc-unity-project 读取这个 VRC 项目，找出 Avatar 主场景、菜单、参数和 FX Controller
```

也可以直接提出相关任务，例如：

```text
检查这个 Avatar 的眼镜开关为什么没有生效
确认 Modular Avatar 合并后是否还存在某个参数
读取所有 PhysBone 和 Contact 配置
追踪这个 Expression Menu 引用了哪些子菜单
```

## 环境要求

- Codex
- 完整的 Unity 项目目录
- 与 `ProjectSettings/ProjectVersion.txt` 匹配的 Unity Editor
- 需要语义检查时，项目必须能够正常导入和编译

如果同一个项目正在 Unity 图形界面中打开，批处理检查可能因项目锁而失败。

## 项目结构

```text
read-vrc-unity-project/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    └── unity-editor-inspection.md
```

`SKILL.md` 是 Codex 的实际执行入口；`references/` 中包含 Unity 批处理检查模式和 Editor 脚本模板。

## 注意事项

- Unity 序列化文件不是普通 YAML，不能仅靠通用 YAML 解析器完整还原项目。
- 使用 Modular Avatar、NDMF 或 Avatar Optimizer 时，源场景不等于最终上传结果。
- 公开分享前不要加入 Avatar 资源、Unity 日志、账号信息、密钥或其他无权分发的内容。
