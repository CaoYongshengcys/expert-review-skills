# Expert Review Skills

> 学术论文审阅与期刊分析技能库

## 目录

| 技能 | 说明 |
|------|------|
| `expert-paper-review/` | 学术论文审阅技能 |
| `journal-scope-review/` | 期刊匹配分析技能 |

## expert-paper-review

电力系统与能源领域的学术论文审阅技能，提供：

- 7维度评估体系（创新性、技术严谨性、方法论、结果验证、文献综述、写作质量、重要性影响）
- 双模式审阅（Reviewer Mode / Self-Check Mode）
- 结构化审阅报告模板
- 知识库索引系统
- 问题交叉引用分类

### 核心功能

1. **论文审阅**: 对学术论文进行系统性专家级评审
2. **知识积累**: 审阅结果持久化为可检索知识库
3. **问题分类**: 按问题类型（Critical/Major/Minor/Suggestion）归档

## journal-scope-review

期刊匹配分析与投稿建议技能，提供：

- Scope对齐矩阵分析
- 贡献层次定位（Device/System/Planning/Application）
- 修改成本评估（Reframing/Augmenting/Rebuilding）
- 期刊推荐与风险评估

### 核心功能

1. **期刊匹配**: 评估论文与目标期刊的匹配度
2. **修改建议**: 提供针对性修改方案
3. **替代方案**: 推荐备选期刊列表

## 使用方式

在 Agent 对话中加载技能：

```
/skill expert-paper-review
/skill journal-scope-review
```

## 评分标准

| 平均分 | 推荐结果 |
|--------|----------|
| 4.5 - 5.0 | Accept |
| 3.5 - 4.4 | Minor Revision |
| 2.5 - 3.4 | Major Revision |
| 1.5 - 2.4 | Reject (major rework) |
| 1.0 - 1.4 | Reject |

## 审阅维度

1. **Novelty & Originality** - 创新性与原创性
2. **Technical Rigor** - 技术严谨性
3. **Methodology** - 方法论
4. **Results & Validation** - 结果与验证
5. **Literature Review** - 文献综述
6. **Writing Quality** - 写作质量
7. **Significance & Impact** - 重要性与影响

## 文件结构

```
expert-review-skills/
├── expert-paper-review/
│   ├── SKILL.md              # 技能定义
│   ├── common-issues.md      # 常见问题列表
│   ├── index-template.md     # 索引模板
│   └── review-template.md    # 审阅报告模板
└── journal-scope-review/
    ├── SKILL.md              # 技能定义
    ├── README.md             # 使用说明
    └── LICENSE              # 许可证
```
