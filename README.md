# VRChat Avatar Inspector Skill

一个面向 Codex 的 VRChat Avatar Unity 项目检查与文档化 Skill。它先确认项目实际安装的工具，再从玩家可见的 Expressions Menu 出发，追踪参数、控制器、模型对象和生成流程，最终形成可复查的项目文档。

## 工作流

1. **确认 Unity MCP 与工具链**：先连接项目对应的 Unity MCP 实例，再读取 Unity、VRChat SDK、包清单与项目中实际存在的组件；不会假定某个插件已安装。
2. **建立玩家路径**：从 Expressions Menu 的入口和子菜单开始，保留每个功能提供者的菜单边界。
3. **追踪到模型**：沿菜单、参数、Animator、Modular Avatar 或其他生成系统追踪到最终对象、材质、BlendShape、PhysBone、Contact 等目标。
4. **按已确认工具应用经验**：只在项目确实包含对应工具时使用专用检查方法；未知工具使用通用 provider 路径，不套用猜测的结构。
5. **形成文档**：记录工具选择、菜单清单、参数与功能映射、证据层级、未验证项和后续刷新条件。

## 工具选择

Skill 会在检查开始时给出建议，但由用户确认采用什么工具。

| 场景 | 推荐 | 说明 |
| --- | --- | --- |
| 衣服、配件与物品开关 | Lilycal Inventory（LI） | 项目已安装时使用 LI 的库存与菜单检查经验。 |
| 面部表情 | FaceEmo | 项目已安装时使用表情、手势、眨眼与口型相关检查经验。 |
| 通用菜单与参数组合 | Modular Avatar | 适合作为通用组合路径，仍以项目中的实际组件为准。 |

额外支持 DressingTools、Gesture Manager、Avatar Optimizer，以及项目中其他声明自身菜单、参数或构建行为的工具。它们不属于默认推荐；Skill 会先识别实际资产和组件，再选择对应或通用的检查路径。

## 能做什么

- 识别 Avatar 根节点、Descriptor、菜单、参数和 Animator 控制器。
- 从玩家可见菜单追踪到对象开关、材质、BlendShape、PhysBone、Contact 和其他功能。
- 检查 Modular Avatar、NDMF 和优化器等构建期变换。
- 区分静态文件、Unity 已解析状态、生成结果和实际运行验证。
- 生成或维护工具清单、菜单清单、功能映射与审计状态文档。
- 在修改后标记已经失效的高层证据，避免沿用旧的构建或运行结论。

## Unity MCP 是必需条件

涉及 Unity 已解析对象、场景或 Prefab 状态、组件语义、Console、预览、构建或任何项目修改时，必须通过项目对应的 Unity MCP 实例执行。Skill 会在行动前重新发现实例，并核对项目、Unity 版本、活动场景、Dirty/编译/Play 状态和 Console 基线。

如果没有可用的 Unity MCP，Skill 只能继续不依赖 Editor 的静态文件检查，并把后续结论标记为 `MCP_REQUIRED` 或 `BLOCKED`；不会用 Unity 批处理脚本冒充完整的 MCP 检查，也不会在连接不明时修改项目。

## 安装

将仓库克隆到 Codex 的 Skills 目录，并确保仓库根目录直接包含 `SKILL.md`：

```powershell
git clone https://github.com/XiaoboooOvO/VRChatEditorSkill.git `
  "$env:USERPROFILE\.codex\skills\inspect-vrchat-avatar-project"
```

安装后新开一个 Codex 会话。

## 使用示例

```text
$inspect-vrchat-avatar-project 检查这个 Avatar。先让我确认工具选择，再读取玩家菜单并生成项目审计文档。
```

也可以直接提出具体任务：

```text
从衣服菜单追踪每个开关实际控制的模型对象
检查当前表情系统与手势条件是否冲突
确认某个菜单功能经过构建后是否仍然存在
导入新功能后刷新菜单、参数和审计文档
```

## 安全边界

- 检查和诊断默认只读；没有明确授权时不修改 Avatar。
- 预览、构建、运行测试和上传是不同的证据层级，不互相替代。
- 不会因为允许检查或构建就推断用户允许上传。
- Unity 序列化文件、源场景和最终生成的 Avatar 可能不同，结论会注明证据来源。
- 完整审计、Editor 检查和任何 Unity 项目修改都要求连接到目标项目的 Unity MCP。
- 不包含 Avatar 资源、账号信息、密钥或项目专用插件说明。

## 仓库结构

```text
VRChatEditorSkill/
├── SKILL.md
├── README.md
├── agents/
│   └── openai.yaml
└── references/
    ├── toolchain-selection.md
    ├── avatar-feature-routing.md
    ├── audit-documentation-workflow.md
    └── ...
```

`SKILL.md` 是执行入口；`references/` 按任务需要提供工具选择、功能追踪、文档化和证据边界等细化流程。
