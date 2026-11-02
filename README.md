# expert-thinking-partner

把 AI 从"有问必答"变成"先把问题搞对，再给能直接用的答案"的 Agent Skill。

> Turn an AI from a passive Q&A tool into an active problem-solving partner — one that defines the problem correctly first, then delivers something you can actually use.

## 它解决什么问题

多数 AI 回答有两个通病：

- **照字面执行**——你问 A，它答 A，不管 A 是不是你真正要解决的问题
- **显得专业 > 真的有用**——堆框架、上表格、拉多视角，最后给一堆分析而不是成品

这个技能给 AI 装一套资深搭档该有的工作习惯：先对齐真实目标 → 按问题大小配方法 → 结论标注依据与不确定性 → 交付能直接用的成品。

## 什么时候触发

- 复杂问题、模糊或开放式问题
- 重要决策（该不该 / 选哪个 / 要不要砍）
- 研究、创作、设计、规划、复盘
- 找方案盲点、挑战现有观点
- 优化提示词

**不触发**：翻译、润色、格式转换、基础解释——简单任务直接完成，不绕弯子。

## 核心设计

| 原则 | 含义 |
|---|---|
| 任务驱动，而非框架驱动 | 只用能实质改善结果的分析工具，不为显得全面而硬套 |
| 角色是视角，不是质量保证 | "顶级专家"标签不能替代事实、方法和验证 |
| 区分事实、推断与假设 | 高影响判断必须标注不确定性 |
| 交付优先 | 给成品，不只给分析 |
| 深度 ≠ 长度 | 输出深度匹配任务风险，不匹配"看起来复杂" |

七条工作原则（先理解目标 / 任务驱动而非框架驱动 / 角色是视角 / 区分事实推断假设 / 结论可检查 / 交付优先 / 具体高效诚实）是全部依据，步骤只引用不重述。

八步工作流 **Understand → Scope → Clarify → Plan → Solve → Verify → Deliver → Iterate**，但不默认走完——开头的**分级→选步**表按任务强度决定走哪几步，跳过是设计而非例外。Verify 用一份红旗自查清单（"我是不是在用漂亮框架掩盖信息不足？"）代替抽象的"检查质量"。

## 安装

**Hermes Agent**

```bash
mkdir -p ~/.hermes/skills/expert-thinking-partner
cp SKILL.md ~/.hermes/skills/expert-thinking-partner/SKILL.md
```

**Claude Code / Codex**

```bash
mkdir -p ~/.claude/skills/expert-thinking-partner
cp SKILL.md ~/.claude/skills/expert-thinking-partner/SKILL.md
```

**其他支持 Agent Skills 的客户端**：把 `SKILL.md` 放进该客户端的 skills 目录即可，需要 `name` 与 `description` 两个 frontmatter 字段。

> 安装后新开会话生效——技能索引在会话启动时缓存。

## 文件结构

```
expert-thinking-partner/
├── SKILL.md      # 技能本体（frontmatter + 正文）
├── README.md
└── LICENSE
```

## 设计说明：description 为什么这么写

技能索引只把 `description` 前 60 个字符喂给模型做路由，正文要等触发之后才加载。所以：

- **触发词必须前置**，不能埋在正文里（否则是 "invisible trigger"）
- **写用户真会打出来的词**（"盲点"、"优化提示词"），不是书面表述（"发现盲点"、"提示词工程"）
- **带反向边界**（"简单任务直接做"），避免劫持琐碎请求

当前 description 55 字符，完整覆盖 13/20 个正文承诺的触发概念。

## License

MIT
