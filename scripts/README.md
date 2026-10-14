# scripts/

**这里是运行版。正本在 [`research-workflow`](https://github.com/crce-ux/research-workflow) 的 `scripts/`**——开发与测试都在那边。

| 脚本 | 干什么 |
|---|---|
| `check_token_diff.py` | **改写前后的受保护 token 比对**——丢失的必须逐个解释 |
| `check_skill_structure.py` | 结构校验（官方 Agent Skills 规范）+ 声明落地 |
| `selfcheck.py` | 一条命令自检：结构 + 语法 + 依赖 |

## 为什么只有这一个检查器

**本 skill 大部分是判断（C 类），不设机检**——
「这个创新是不是真的」「这条链断在哪」都是语义，不是可判定的格式。

**只有 token diff 这一条是纯比对**，而且手册原文就写着
「**输出前复核 token diff —— 这一项不可省；无脚本时手工列清单**」。这个脚本就是那一项。

```bash
python scripts/check_token_diff.py <原文> <改写后>
```

它提取 LaTeX 命令 / 引用 key / 数字与单位 / 状态 token / 路径 URL，
比对前后两份文本，列出**丢失**与**新增**。

**丢失的必须逐个解释**——丢一个数字，就是改了一个事实。
无法证明零损失 → 恢复原句，并标「人工确认」。
