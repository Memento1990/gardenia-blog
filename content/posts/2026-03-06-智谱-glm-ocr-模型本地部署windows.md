---
title: 智谱 GLM-OCR 模型本地部署(windows)
description: ""
date: 2026-03-06T03:55:47.551Z
preview: ""
draft: true
tags: []
categories: []
---

## 模型介绍

智谱的 GLM-OCR 模型是一个基于 OCR 技术的模型，用于识别图片中的文本。

![alt text](image-8.png)

![文档解析与信息抽取](image-5.png)
![真实场景测试](image-6.png)
![速度测试](image-7.png)

从官方文档可以看出, 支持 VLLM 和 SGLang 部署, 成本约为传统 OCR 方案的 1/10;

## VLLM 部署(生产环境推荐)

```shell
# 安装 vLLM
pip install -U vllm --extra-index-url https://wheels.vllm.ai/nightly

# 安装 transformers(需要源码版本)
pip install -U git+https://github.com/huggingface/transformers.git

# 启动服务
vllm serve zai-org/GLM-OCR --allowed-local-media-path / --port 8080
```

## SGLang 部署

## Ollama 部署

```shell
# 下载 GLM-OCR 模型
ollama pull glm-ocr

# 直接运行模型进行交互式对话
ollama run glm-ocr

# 识别图片中的文本
ollama run glm-ocr "请识别图片中的文本" image.png

# 指定输出格式
ollama run glm-ocr "请识别图片中的文本, 并以 JSON 格式输出" image.png
```

## 参考资料

[Github](https://github.com/zai-org/GLM-OCR)
[阿里云 ModelScope 平台 模型链接](https://www.modelscope.cn/models/ZhipuAI/GLM-OCR)

[GLM-OCR README.md](https://github.com/zai-org/GLM-OCR/blob/main/README_zh.md#%E6%96%B9%E5%BC%8F-2%E4%BD%BF%E7%94%A8-vllm--sglang-%E8%87%AA%E9%83%A8%E7%BD%B2)
[0.9B 小模型，OCR 大能力——GLM-OCR 模型实战教程](https://developer.aliyun.com/article/1712888)
[GLM-OCR 部署全攻略：0 基础搭高性能文字识别服务](https://blog.csdn.net/iFisher666/article/details/158616088)

如果遇到下载速度慢的问题, 可以设置环境变量 `HF_ENDPOINT` 为 `https://hf-mirror.com`

```shell
export HF_ENDPOINT=https://hf-mirror.com
```
