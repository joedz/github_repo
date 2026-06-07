---
title: MarkItDown
source_type: github
repo_url: https://github.com/microsoft/markitdown
local_path: ""
category: cli
feature: documentation
secondary_features: ["plugin-system", "multi-format-conversion", "azure-integration"]
tags: ["markdown", "python", "document-conversion", "llm", "pdf", "docx", "pptx", "excel"]
added_at: 2026-06-07
status: active
---

# MarkItDown

## 项目概述

MarkItDown 是微软 AutoGen 团队开源的轻量级 Python 工具，用于将多种文件格式（PDF、Word、Excel、PowerPoint、图片、音频、HTML、CSV、JSON、XML、ZIP、YouTube、EPub 等）转换为 Markdown，专为 LLM 及文本分析 pipeline 设计。

## 特点

- **多格式支持**：原生支持 10+ 文件格式的读取与结构化转换，保留标题、列表、表格、链接等文档结构。
- **结构化 Markdown 输出**：与纯文本提取不同，输出保留 Markdown 格式，适合直接喂给 LLM。
- **插件架构**：通过 `enable_plugins=True` 启用第三方插件，已有 `markitdown-ocr` 等插件提供 LLM Vision OCR 支持。
- **Azure 云服务集成**：可选接入 Azure Document Intelligence 和 Azure Content Understanding，提供云端布局分析和结构化字段提取（YAML front matter）。
- **多种接入方式**：CLI 命令行、`convert()` Python API、`convert_stream()` 窄 API、`convert_local()` 本地文件专用 API，层次分明。
- **模块化转换器设计**：每种文件格式对应独立 converter，职责分离清晰。
- **安全设计**：强调调用最窄 API（`convert_stream()` / `convert_local()` / `convert_response()`），区分不同 I/O 权限边界。

## 工作流位置

- **文档预处理阶段**：将 PDF、Word、Excel 等非文本格式文档转换为 Markdown，作为 AI 分析 pipeline 的输入。
- **文档知识提取**：在 RAG 或知识库构建流程中，将多种来源文档统一转为文本。
- **Agent 工具链**：作为 agent 的文件读取工具，将各种格式文档转给 LLM 处理。

## 接入方式

**pip 安装（推荐含所有格式依赖）**：

```bash
pip install 'markitdown[all]'
```

**Docker**：

```bash
docker build -t markitdown:latest .
docker run --rm -i markitdown:latest < ~/your-file.pdf > output.md
```

**CLI 基本用法**：

```bash
markitdown path-to-file.pdf > document.md
markitdown path-to-file.pdf -o document.md
cat path-to-file.pdf | markitdown
```

**Python API**：

```python
from markitdown import MarkItDown

md = MarkItDown(enable_plugins=False)
result = md.convert("test.xlsx")
print(result.text_content)
```

**Azure Content Understanding（高质量云端转换）**：

```bash
pip install 'markitdown[az-content-understanding]'
markitdown path-to-file.pdf --use-cu --cu-endpoint "<content_understanding_endpoint>"
```

## 参考方式

- **Converter 模块分离架构**：每种文件格式独立 converter 类，继承统一接口，可作为文件格式转换插件化的参考。
- **插件系统设计**：通过 `enable_plugins=True` + `markitdown --use-plugins` 机制加载第三方扩展，可参考 `packages/markitdown-sample-plugin` 开发自定义插件。
- **最窄 API 调用设计**：提供 `convert_local()` / `convert_stream()` / `convert_response()` 区分不同 I/O 场景，体现安全最佳实践。
- **可选依赖分组**：通过 `[pdf]`、`[docx]`、`[pptx]` 等标签分组可选依赖，用户按需安装，hatch 构建配置清晰。

## 简单预览

暂无（官网即 GitHub 仓库 README，内容详尽）

## 已确认

- 微软 AutoGen 团队出品，MIT 许可证，已开源。
- 要求 Python >= 3.10，使用 hatchling 作为构建后端。
- CLI入口定义在 `markitdown/__main__:main`，通过 `markitdown` 命令调用。
- 原生可选依赖：`[pptx]`、`[docx]`、`[xlsx]`、`[xls]`、`[pdf]`、`[outlook]`、`[audio-transcription]`、`[youtube-transcription]`、`[az-doc-intel]`、`[az-content-understanding]`。
- 已有第三方 OCR插件 `markitdown-ocr`，通过 LLM Vision 提取图片内文字，无需 ML 库或二进制依赖。
- Azure Content Understanding 支持结构化字段提取，输出 YAML front matter。
- 支持 Docker 容器化部署。

## 待验证

- 本地 pip 安装 `markitdown[all]` 并测试 PDF、Word、Excel 实际转换效果。
- 测试插件机制：`pip install markitdown-ocr` 并验证图片 PDF 的 OCR 效果。
- 验证 Docker 部署方式。
- 探索 converter 模块源码，理解如何新增自定义格式支持。