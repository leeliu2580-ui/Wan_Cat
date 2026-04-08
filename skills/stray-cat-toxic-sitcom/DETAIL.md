---
title: 猫猫毒舌漫短剧分镜生成（Stray Cat Toxic Sitcom）
version: 0.1.0
category: 图像类
---

# 作品名称
猫猫毒舌漫短剧分镜生成（Stray Cat Toxic Sitcom）

# 作品简介
把一个“猫猫第一人称毒舌自述”的漫短剧点子，自动完善成可拍的剧情节奏与分镜表（3–12格），并调用 Wan2.7 组图生成连续分镜画面；支持喜剧/催泪权重、竖屏9:16、角色一致性与长耗时 task_id 续查。

# 面向场景 / 解决问题
- 适用人群：短视频/漫短剧创作者、内容号、小红书图文作者、短剧策划
- 核心痛点：点子难落地、分镜耗时、单张生图不连贯、风格难统一
- 目标产出：大纲 + 分镜表 + 可直接用于生成的执行命令 + 连续分镜组图链接

# 核心调用逻辑（输入→处理→输出闭环）
1. 启动询问：点子、金句、模式（更喜剧/平衡/更催泪）、张数n、画幅/清晰度、猫设定、参考图（可选）
2. 剧情加工：把点子改写成“钩子→毒舌→笑点教程→转折→泪点→反转收束”的可拍结构
3. 分镜规划：输出至少6格分镜表（镜头语言/场景/动作/情绪/道具/旁白要点）
4. Prompt组装：把“总风格 + n格画面清单 + 一致性约束”压缩为 user_requirement
5. 参数准备：
   - 若用户给“1K 9:16”等组合，先换算像素
   - 若有参考图，本地上传转成 oss:// URL
6. Wan2.7 出图：用组图模式一次生成 n 张连续分镜
7. 异步续查：如返回 task_id，用脚本查询任务状态并回传结果URL

# 使用到的 Wan 能力
- Wan2.7 图像生成/组图生成（一次生成 3–12 张连续分镜）
- Wan2.7 图像编辑（可选：有参考图时增强角色一致性）

重要说明：本作品所有图片均通过 Wan2.7 能力生成。

# 快速开始（安装与试用）
## 1) 环境变量
- DASHSCOPE_API_KEY：百炼 API Key
- DASHSCOPE_BASE_URL：可选（默认北京；新加坡用 dashscope-intl）

## 2) 安装 Skill
在 AI Agent 对话中指定安装路径：
```text
安装这个目录下的skill  /path/to/Wan_Cat/skills/stray-cat-toxic-sitcom
```

## 3) 一键开始（复制填空）
```text
【点子】（1-3000字）：
【金句】（可选，逗号分隔）：
【模式】更喜剧 / 平衡 / 更催泪（默认：平衡）：
【张数】3-12（默认：8）：
【画幅】9:16 / 16:9 / 3:4（默认：9:16）：
【清晰度】1K / 2K（默认：1K）：
【猫设定】狸花 / 橘猫 / 黑猫 / 奶牛猫（默认：狸花）：
【参考图】无 / 本地路径 / URL（最多9张，默认：无）：
```

# 关键脚本与文档
- Skill 定义：[SKILL.md](SKILL.md)
- 生成/编辑/组图脚本：skills/wan2.7-image-skill/scripts/image-generation-editing.py
- 分辨率换算脚本：skills/wan2.7-image-skill/scripts/parse_resolution.py
- 本地图片上传脚本：skills/wan2.7-image-skill/scripts/file_to_oss.py
- 异步任务续查脚本：skills/wan2.7-image-skill/scripts/check_wan_task_status.py

# 试运行样例（8张，9:16，1K，狸花，无参考图）
- 画幅换算：1K 9:16 → 768*1364
- 结果（有效期24小时，作为演示记录）：
  1. https://dashscope-7c2c.oss-accelerate.aliyuncs.com/1d/ba/20260409/ea4c8ef9/1dedaf15-929a-49ce-a32d-83f2b2fcc380_0.png?Expires=1775751200&OSSAccessKeyId=LTAI5tPxpiCM2hjmWrFXrym1&Signature=KfbNxQP%2FnT7Ke%2BxT7raeKdgJnXE%3D
  2. https://dashscope-7c2c.oss-accelerate.aliyuncs.com/1d/d2/20260409/ea4c8ef9/1dedaf15-929a-49ce-a32d-83f2b2fcc380_1.png?Expires=1775751200&OSSAccessKeyId=LTAI5tPxpiCM2hjmWrFXrym1&Signature=EtYGnvQa9xcR77M76Q1eX9mn08U%3D
  3. https://dashscope-7c2c.oss-accelerate.aliyuncs.com/1d/92/20260409/ea4c8ef9/1dedaf15-929a-49ce-a32d-83f2b2fcc380_2.png?Expires=1775751199&OSSAccessKeyId=LTAI5tPxpiCM2hjmWrFXrym1&Signature=dn8ThkEsHbjGYIqkJ%2Btbmlc0raI%3D
  4. https://dashscope-7c2c.oss-accelerate.aliyuncs.com/1d/cd/20260409/ea4c8ef9/1dedaf15-929a-49ce-a32d-83f2b2fcc380_3.png?Expires=1775751199&OSSAccessKeyId=LTAI5tPxpiCM2hjmWrFXrym1&Signature=r5RfqItqH1nBIst1veKz%2BgZmekA%3D
  5. https://dashscope-7c2c.oss-accelerate.aliyuncs.com/1d/9a/20260409/ea4c8ef9/1dedaf15-929a-49ce-a32d-83f2b2fcc380_4.png?Expires=1775751200&OSSAccessKeyId=LTAI5tPxpiCM2hjmWrFXrym1&Signature=dEOtxt7pIXbEoESzwoOPrJt6DwU%3D
  6. https://dashscope-7c2c.oss-accelerate.aliyuncs.com/1d/05/20260409/ea4c8ef9/1dedaf15-929a-49ce-a32d-83f2b2fcc380_5.png?Expires=1775751199&OSSAccessKeyId=LTAI5tPxpiCM2hjmWrFXrym1&Signature=8a6IMVR%2BQ3Fu1zOiuc9854bssy0%3D
  7. https://dashscope-7c2c.oss-accelerate.aliyuncs.com/1d/87/20260409/ea4c8ef9/1dedaf15-929a-49ce-a32d-83f2b2fcc380_6.png?Expires=1775751200&OSSAccessKeyId=LTAI5tPxpiCM2hjmWrFXrym1&Signature=XnC6%2BTTTDji0%2FDdSoEdKm%2FVKExc%3D
  8. https://dashscope-7c2c.oss-accelerate.aliyuncs.com/1d/e6/20260409/ea4c8ef9/1dedaf15-929a-49ce-a32d-83f2b2fcc380_7.png?Expires=1775751200&OSSAccessKeyId=LTAI5tPxpiCM2hjmWrFXrym1&Signature=gmALx8sy9KSOsbKmzDXL3WYRozc%3D
