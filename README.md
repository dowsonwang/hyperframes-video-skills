![AI 代码视频，三套 HyperFrames 制作工作流](assets/cover.png)

# HyperFrames 视频工作流

从产品官网、手头的音视频素材或一段文字出发，用 Codex 把内容做成能预览、能改、能导出 MP4 的视频。本仓库收录了公司培训中使用的三个 Skill，保留各自的脚本、参考资料和分镜工作指引。

[选工作流](#选工作流) · [安装到项目](#安装到项目) · [可以直接复制的提示词](#可以直接复制的提示词) · [上游来源](#上游来源)

## 选工作流

| 你准备的素材和目标 | 选哪个 Skill | 怎么做 | 培训案例 |
| --- | --- | --- | --- |
| 有产品网址或真实界面，要拍宣传片、功能演示 | [`product-launch-video`](skills/product-launch-video/SKILL.md) | 先读产品和受众，抓真实页面和品牌素材。按使用场景写口播和分镜，把功能放进镜头。 | 全球语言服务平台 V2 |
| 有原声、录屏、实拍、数据，或要继续改已有工程 | [`general-video`](skills/general-video/SKILL.md) | 从已有素材和项目状态出发，确定叙事和节奏。把原声、画面、字幕和动效装配到时间轴。 | 《中文值钱了》《1066》 |
| 有文章、主题或提纲，要做一条无人出镜的解说 | [`faceless-explainer`](skills/faceless-explainer/SKILL.md) | 从原文提炼观众要弄懂的问题，安排旁白和讲解顺序，用图形、图表和文字说明。 | 《AI 智能体是工作的盔甲》《云端智能体到底是什么》 |

## 安装到项目

使用 Codex、Git、Node.js 22.20+ 和 FFmpeg。先将仓库克隆到视频项目旁边。

```bash
git clone https://github.com/dowsonwang/hyperframes-video-skills.git
mkdir -p my-video
cd my-video
```

这三个工作流会读取同级目录里的 HyperFrames 核心、动画、设计和素材 Skill。下面先装对应历史版本的依赖，再装本仓库的三个工作流，文件会复制到当前项目的 `.agents/skills/`。

```bash
npx skills add "https://github.com/heygen-com/hyperframes/tree/4e6fcdb3a9f310a9c483622d6a4ca5354a63fb22/skills" \
  -a codex --copy -y --skill \
  hyperframes hyperframes-cli hyperframes-registry hyperframes-core \
  hyperframes-animation hyperframes-creative hyperframes-audio \
  hyperframes-keyframes media-use

npx skills add ../hyperframes-video-skills \
  -a codex --copy -y --skill product-launch-video general-video faceless-explainer
```

用 Codex 打开 `my-video`，启动新会话，然后发下面任意一段。想复现培训用的版本时，可以加一句「先读取项目里的 SKILL.md，按本地版本走，需要更新时先告诉我」。

安装命令与环境说明见 [HyperFrames 技能文档](https://github.com/heygen-com/hyperframes/blob/main/docs/guides/skills.mdx) 和 [Skills CLI 文档](https://github.com/vercel-labs/skills)。

## 可以直接复制的提示词

### 把官网做成宣传片

> 请用 `product-launch-video` 给这个产品做一条 25 秒横屏宣传片。产品官网是【填网址】，受众是第一次接触产品的客户。先看官网，把片子要讲的一个功能和真实使用场景说清楚。用真实页面展示怎么操作。先给我口播稿和逐镜分镜，确认后再出预览。

### 用已有原声和数据做解说

> 请用 `general-video` 把 `voice.wav`、`data.csv` 和 `screens/` 里的素材做成 45 秒竖屏解说。沿用录好的原声，讲到报价时把两组数字放在同一个画面做对照，并写明样本范围。先给我一段带声音的预览。

### 把一段文字做成知识短片

> 请用 `faceless-explainer` 把 `article.md` 做成 40 秒知识短片。开头拿一个生活例子提问，接下来用旁白、图形和字幕讲清原因。每个画面只讲一件事。先给我口播和分镜，让我核对讲法。

看片时可以在同一会话直接说「第 3 秒把标题放大，念到第一个数字时再出图表。给我重看这一段」。确认后请 AI 渲染成 MP4，并发回文件路径。

## 工程里会看到什么

| 文件 | 你可以核对什么 |
| --- | --- |
| `BRIEF.md` | 谁看、讲什么、做多长、在哪播放 |
| `SCRIPT.md` 和 `STORYBOARD.md` | 每句旁白对应哪个画面，画面接在什么位置 |
| `frame.md` | 画幅、字体、颜色、字幕和动画的视觉规范 |
| `index.html` 和场景文件 | 在预览里看到的画面、时间轴和组成素材 |
| `renders/` | 最终渲染交付的 MP4 |

## 上游来源

三个目录是 HyperFrames 工作流的培训快照，逐文件校对了上游版本。保留原始英文说明和脚本，仓库首页补充中文操作示例。许可见 [Apache License 2.0](LICENSE)。

- `product-launch-video` 对应 [HeyGen HyperFrames 上游快照](https://github.com/heygen-com/hyperframes/tree/6f90ca15a7fc937d9d6cf3ec289f2a26eca3724f/skills/product-launch-video)。
- `general-video` 对应 [HeyGen HyperFrames 上游快照](https://github.com/heygen-com/hyperframes/tree/4e6fcdb3a9f310a9c483622d6a4ca5354a63fb22/skills/general-video)。
- `faceless-explainer` 对应 [HeyGen HyperFrames 上游快照](https://github.com/heygen-com/hyperframes/tree/4e6fcdb3a9f310a9c483622d6a4ca5354a63fb22/skills/faceless-explainer)。
