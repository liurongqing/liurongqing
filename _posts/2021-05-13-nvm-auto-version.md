---
title: nvm 根据项目自动切换版本
author: liurongqing
categories: [nvm]
tags: [nvm, 'node']
---

## 正常切换

1. 项目中创建 `.nvmrc`，并写入版本号

```bash
echo '14.15' > .nvmrc
```

2. 切换版本

> 这样就会进入到 node 14.15 版本

```bash
nvm use
```
## 自动切换

> 可以使用avn、nvs、zshrc 命令，这边使用的是 zshrc

```bash
# 在 ~/.zshrc 文件最后加入这个，并 source ~/.zshrc
autoload -U add-zsh-hook
load-nvmrc() {
  if [[ -f .nvmrc && -r .nvmrc ]]; then
    nvm use
  elif [[ $(nvm version) != $(nvm version default)  ]]; then
    echo "Reverting to nvm default version"
    nvm use default
  fi
}
add-zsh-hook chpwd load-nvmrc
load-nvmrc
```
