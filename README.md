# AI Checker

AI 生成内容检测技能（Claude Code Skill），覆盖文本、图片、视频、音频、文档六大检测场景，含置信度评分框架和完整报告模板。

## 功能概览

| 检测目标 | 核心技术 |
|---------|---------|
| **文本/文章** | 困惑度（Perplexity）、突发性（Burstiness）、N-gram分布、工具集成 |
| **图片** | GAN棋盘格纹、ELA误差分析、FFT/DCT频域、EXIF元数据、C2PA |
| **视频 Deepfake** | 面部特征漂移（FFD）、时域频率伪影、光流分析、嘴唇同步 |
| **音频合成语音** | 梅尔频谱、MFCC、LFCC、SSL特征融合（Wave2Vec2BERT）|
| **PDF文档** | 元数据取证、ELA分析、PDF增量更新检测、字体一致性 |
| **链接/流量** | Bot行为特征、JS指纹、蜜罐检测 |

## 置信度框架

```
置信度得分 = (强证据数 × 3 + 中等证据数 × 1.5 + 辅助证据数 × 0.5)
           ÷ (强证据总数 × 3 + 中等证据总数 × 1.5 + 辅助证据总数 × 0.5)

≥ 0.75 → 高置信度 AI 生成
0.50–0.74 → 中置信度，建议人工复核
0.25–0.49 → 低置信度，存疑但证据不足
< 0.25 → 倾向人类创作
```

## AI 内容现状数据（2025年3月）

- **74.2%** 新发布网页含AI内容（Ahrefs，90万页样本）
- **52%** 在线文章为AI撰写（Graphite SEO 2025）
- **~57%** 综合估算（AI辅助或生成）
- **90%** 预测比例 by 2026（Europol）

## 安装方式

### 方式一：安装 `.skill` 文件

在 Claude Code 中运行：

```bash
# 下载并安装
curl -L https://github.com/chat2dev/ai-checker/raw/main/ai-content-detection.skill \
  -o ai-content-detection.skill
```

然后在 Claude Code 设置中导入 `.skill` 文件。

### 方式二：手动复制 SKILL.md

将 `ai-content-detection/SKILL.md` 复制到你的 `~/.claude/skills/ai-content-detection/` 目录。

## 触发方式

以下类型的问题会自动触发此技能：

- "这篇文章是AI写的吗？"
- "帮我检测这张图片是否是 AI 生成的"
- "这段音频是不是合成语音？"
- "我怀疑这份 PDF 收入证明是伪造的"
- "现在互联网上有多少内容是AI生成的？"
- "我的论文被误判为 AI 写的，怎么证明是我自己写的？"
- Detecting deepfakes, AI writing, synthetic voices, document fraud

## 评测结果

在 8 个场景（含 HC3、ASVspoof、FaceForensics++ 数据集模式）下验证：

| 配置 | 通过率 | Token 用量 |
|------|--------|-----------|
| With Skill | **100%** (40/40) | ~29,320 |
| Without Skill | 85% (34/40) | ~19,385 |
| **Delta** | **+15pp** | +9,935 |

技能独特价值集中在：置信度计算公式、精确统计数据引用、三级证据分类体系、PDF增量更新检测方法。

## 文件结构

```
ai-checker/
├── README.md
├── ai-content-detection.skill        # 打包好的 skill 文件（可直接导入）
└── ai-content-detection/
    └── SKILL.md                      # skill 源文件（415行，中文）
```

## 适用场景

- 内容审核员核查投稿真实性
- 银行/金融合规人员鉴别伪造文件
- 学术机构处理 AI 作弊争议
- 新闻编辑核实疑似 Deepfake 视频/音频
- 研究人员统计 AI 内容占比
- 个人用户自证论文非 AI 生成

## License

MIT
