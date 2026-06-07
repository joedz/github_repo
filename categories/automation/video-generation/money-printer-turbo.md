---
title: MoneyPrinterTurbo
source_type: github
repo_url: https://github.com/harry0703/MoneyPrinterTurbo
local_path: ""
category: automation
feature: video-generation
secondary_features: ["ai-tools", "frontend", "backend"]
tags: ["video-generation", "automation", "ai-video", "python", "streamlit", "fastapi", "short-video", "content-automation"]
added_at: 2026-06-07
status: active
---

# MoneyPrinterTurbo

## 项目概览

MoneyPrinterTurbo 是一个 AI 视频生成自动化工具，用户只需提供一个视频主题或关键词，即可全自动生成视频文案、视频素材、视频字幕、视频背景音乐，然后合成一个高清短视频。支持竖屏（9:16, 1080x1920）和横屏（16:9, 1920x1080）两种尺寸，提供 Web 界面和 API 接口两种接入方式。

## 特点

- **MVC 架构**：代码结构清晰，Python 主导，FastAPI 后端 + Streamlit 前端，支持 API 和 WebUI 双入口。
- **多 LLM 接入**：支持 OpenAI、AIHubMix、Moonshot、Azure、gpt4free、one-api、通义千问、Google Gemini、Ollama、DeepSeek、MiniMax、文心一言、Pollinations、ModelScope 等多种模型。
- **TTS 方案**：默认使用 Edge TTS（免费，不需要 API Key）；可选 Azure TTS V2（付费，声音质量更高）。
- **字幕生成**：支持 edge 模式（快速，无需 GPU）和 whisper 模式（使用 faster-whisper，更准确但需要下载模型）。
- **视频素材**：来自 Pexels 的高清无版权素材，也支持本地素材。
- **背景音乐**：支持随机或指定音乐文件，可调节音量。
- **批量生成**：可一次生成多个视频，选择最满意的一个。
- **Docker 支持**：提供 docker-compose 一键部署。
- **Windows 一键启动包**：百度网盘和 Google Drive 提供免配置压缩包。

## 工作流位置

- **内容创作自动化**：从主题到成片的全自动化 pipeline
- **短视频生产**：批量生成 TikTok/抖音/YouTube Shorts 风格的短视频
- **AI 辅助创作**：文案生成、语音合成、字幕处理的多模型协同

## 接入方式

```bash
# 方式1: Docker 部署
git clone https://github.com/harry0703/MoneyPrinterTurbo.git
cd MoneyPrinterTurbo
docker-compose up

# 方式2: uv 本地部署
git clone https://github.com/harry0703/MoneyPrinterTurbo.git
cd MoneyPrinterTurbo
uv python install 3.11
uv sync --frozen

# Web 界面
uv run streamlit run ./webui/Main.py --browser.gatherUsageStats=False

# API 服务
uv run python main.py
```

访问 WebUI：http://127.0.0.1:8501
访问 API 文档：http://127.0.0.1:8080/docs

**Windows 一键启动包**（v1.2.6）：百度网盘 / Google Drive 下载，解压后执行 `update.bat` 更新代码，再执行 `start.bat` 启动。

## 参考方式

- **MVC 架构设计**：Python 项目结构（app/config, app/services, webui, main.py），配置与代码分离，services 模块化拆分
- **多 provider 接入模式**：llm_provider 抽象，支持多种模型服务的统一接口封装
- **Streamlit + FastAPI 双入口**：WebUI 用 Streamlit，API 用 FastAPI，职责分离清晰
- **字幕 pipeline**：edge TTS 时间戳方案 vs faster-whisper 转写方案的对比与选型
- **视频合成 pipeline**：MoviePy 2.x 驱动，ffmpeg 底层，字幕渲染用 Pillow（已移除 ImageMagick 依赖）

## 简单预览

- 项目地址：https://github.com/harry0703/MoneyPrinterTurbo
- 在线体验（录咖）：https://reccloud.cn（基于该项目提供的免费 AI 视频生成器）
- Colab 快速体验：https://colab.research.google.com/github/harry0703/MoneyPrinterTurbo/blob/main/docs/MoneyPrinterTurbo.ipynb
- WebUI 截图：docs/webui.jpg
- API 截图：docs/api.jpg

## 已确认

- MIT 许可证
- Python 为主（97.8%），少量其他语言
- v1.2.9（2026-05-30 最新 release）
- 80.9k stars，11.5k forks，505 watching
- 支持 Windows / MacOS / Linux
- GPU 非必需（CPU 可跑，云端 LLM + 在线素材场景）；有 GPU 则 faster-whisper 和批量生成更快
- Whisper 模型（large-v3 约 3GB）国内下载困难时提供百度网盘和夸克网盘备选下载
- 项目内含 resource/songs（背景音乐）和 resource/fonts（字幕字体）

## 待验证

- 多模型同时接入的稳定性和成本控制
- 批量生成多个视频的实际耗时和资源占用
- Whisper 模式在无 GPU 机器上的转写速度
- Azure TTS V2 的实际语音质量提升幅度
- 视频素材的版权风险（声称无版权但未经验证）

## 备注

- 部署路径不要有中文、空格或特殊字符
- 建议 VPN 打开全局模式以访问 HuggingFace（下载 whisper 模型）
- 感谢 AIHubMix 赞助，提供 700+ 模型的一站式接入