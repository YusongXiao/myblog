---
title: 无root权限使用ollama
published: 2025-12-18
description: 本文讲述了无root权限使用ollama的方法
# image: ./cover.png
tags: [人工智能, 技术分享, AI]
category: Blog
draft: false
---


> 之前跑论文的代码时，老师给我分配了内网一个8卡4090的机器的账号，但是没有root权限，今天想着跑一下本地大模型试试


```bash
# 下载（下载慢的可以在自己电脑下载然后传过去）
cd /tmp
curl -fL https://ollama.com/download/ollama-linux-amd64.tgz -o ollama-linux-amd64.tgz
```

```bash
mkdir -p ~/.local
mkdir -p /tmp/ollama-extract
tar -xzf /tmp/ollama-linux-amd64.tgz -C /tmp/ollama-extract
```

```bash
mkdir -p ~/.local/bin
mkdir -p ~/.local/lib
cp -a /tmp/ollama-extract/bin/* ~/.local/bin/
cp -a /tmp/ollama-extract/lib/* ~/.local/lib/
```

```bash
echo $PATH | grep "$HOME/.local/bin"
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH="$HOME/.local/lib:$LD_LIBRARY_PATH"' >> ~/.bashrc
source ~/.bashrc
```

```bash
which ollama
ollama --version
```

使用第8张显卡在11434端口运行
```bash
CUDA_VISIBLE_DEVICES=7 OLLAMA_HOST=0.0.0.0:11434 ollama serve
```
