#!/bin/bash

# 检查是否是root用户，如果不是，提示并退出
if [[ $(id -u) -ne 0 ]]; then
    echo "请以root身份运行此脚本。"
    exit 1
fi

# 克隆Git仓库
git clone https://github.com/Horizen5/nodepay-new.git
cd nodepay-new

# 检查当前Python版本
PYTHON_VERSION=$(python3 --version 2>&1 | awk '{print $2}')
MIN_VERSION="3.11"

# 比较版本
if [[ "$(printf '%s\n' "$MIN_VERSION" "$PYTHON_VERSION" | sort -V | head -n1)" != "$MIN_VERSION" ]]; then
    echo "当前Python版本低于3.11，正在安装Python 3.11..."

    # 更新包列表
    apt update

    # 安装Python 3.11
    apt install -y python3.11 python3.11-venv python3.11-dev

    # 设置Python 3.11为默认Python版本
    update-alternatives --install /usr/bin/python3 python3 /usr/bin/python3.11 1

    # 更新pip
    python3 -m pip install --upgrade pip
fi

# 安装依赖
echo "正在安装依赖..."
pip install -r requirements.txt

echo "完成！"
