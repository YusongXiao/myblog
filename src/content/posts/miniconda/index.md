---
title: 安装和使用miniconda创建虚拟环境
published: 2025-12-31
description: 本文讲述如何安装和使用miniconda创建虚拟环境
# image: ./cover.png
tags: [技术分享]
category: Blog
draft: false
---


## 安装
```
cd ~
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
```

```
bash Miniconda3-latest-Linux-x86_64.sh
```
一路回车，注意：
- 安装路径：**默认 `~/miniconda3`**
- 最后问 `initialize Miniconda?` → **yes**
```
source ~/.bashrc
```

> 可选：不想每次自动进入 (base) 🤏
> ```
> conda config --set auto_activate_base false
> ```

如果输入`conda`没反应，说明conda不在环境变量，需要🔧修复一下
```
~/miniconda3/bin/conda init bash
source ~/.bashrc
```

## 使用
创建一个名字是envname的python3.11环境
```
conda create -n envname python=3.11
```

激活
Windows
```
conda activate envname
```
Linux/Macos
```
source activate envname
```

退出虚拟环境
```
conda deactivate
```