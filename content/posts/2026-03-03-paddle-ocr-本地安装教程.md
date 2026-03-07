---
title: Paddle OCR 本地安装教程
description: ""
date: 2026-03-03T14:48:07.236Z
preview: ""
draft: true
tags: []
categories: []
---

## GPU 判断

windows 环境下, 可以使用 `nvidia-smi` 命令来判断是否有可用的 GPU
如果有可用的 GPU, 会显示 GPU 的信息, 否则会显示 `No devices were found`

```shell
C:\Windows\System32>nvidia-smi
Tue Mar  3 22:53:59 2026
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 566.26                 Driver Version: 566.26         CUDA Version: 12.7     |
|-----------------------------------------+------------------------+----------------------+
| GPU  Name                  Driver-Model | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 4060 ...  WDDM  |   00000000:01:00.0  On |                  N/A |
| N/A   48C    P4              9W /   80W |    1277MiB /   8188MiB |      5%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI        PID   Type   Process name                              GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
xxxxxx
+-----------------------------------------------------------------------------------------+
```

NVIDIA GeForce RTX 4060 Laptop GPU

查看显卡型号的三种方式:

- `Ctrl + Shift + P` 打开命令面板, 点击 `性能` 选项卡, 左侧找到并点击 `GPU 0` 或 `GPU 1` 等, 右侧会显示该 GPU 的信息, 包括型号, 内存, 显存等;
- 此电脑或我的电脑->管理->设备管理器, 显示适配器, 列出显卡型号;
- DirectX 诊断工具 (DxDiag), 在 `win+r` 输入 `dxdiag`, 点击 `显示` 选项卡, 会显示显卡型号等信息;

## 基于 pip 安装 PaddlePaddle

```shell
python -m pip install paddlepaddle-gpu==3.0.0 -i https://www.paddlepaddle.org.cn/packages/stable/cu126/
```

检查是否安装成功

```shell
python -c "import paddle; paddle.utils.run_check()"
python -c "import paddle; print(paddle.__version__)"
```

运行 python 命令检查是否正确识别了 GPU

```python
import paddle
print("编译时是否支持 CUDA：", paddle.is_compiled_with_cuda())
print("当前可用的 GPU 数量：", paddle.device.cuda.device_count())
```

## 安装 PaddleX

安装 PaddleX 基础功能需要的全部依赖

```shell
pip install "paddlex[base]
```

## 通用表格识别v2产线

```shell
paddlex --pipeline table_recognition_v2 \
        --use_doc_orientation_classify=False \
        --use_doc_unwarping=False \
        --input table_recognition_v2.jpg \
        --save_path ./output \
        --device gpu:0
```

## 参考资料

- [飞桨PaddlePaddle本地安装教程](https://paddlepaddle.github.io/PaddleX/latest/installation/paddlepaddle_install.html)
