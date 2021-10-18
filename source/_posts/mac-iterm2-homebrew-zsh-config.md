---
title: "花十分鐘打造好用的 termianl (iterm2 + zsh + oh-my-zsh + powerlevel10k)"
toc: true
tags:
  - zsh
  - mac
  - macos
  - homebrew
  - iterm2 
  - zsh
  - powerlevel10k
  - oh-my-zsh
  - debug
  - vscode
  - 筆記
disqusId: ctsai_1634542899
keywords: zsh, iterm2, mac, macos, homebrew, vscode
date: 2021-10-18 15:39:18
categories: 
  - Note
cover: gallery/cover/cover_mac_iterm2_homebrew_zsh_config.jpg
thumbnail: gallery/cover/cover_mac_iterm2_homebrew_zsh_config.jpg
excerpt: 簡單花 10 分鐘打造好用 mac terminal 設定, 最近因為有電腦重新設定的需求, 而重灌或是使用新電腦的第一件事情通常都會是安裝 terminal 環境, 於是就順手紀錄一下 homebrew, iterm2, zsh 的設定步驟,順便附上 vscode 需要進行對應的設定步驟～
---

簡單花 10 分鐘打造好用 mac terminal 設定
最近因為有電腦重新設定的需求, 而重灌或是使用新電腦的第一件事情通常都會是安裝 terminal 環境, 於是就順手紀錄一下 homebrew, iterm2, zsh 的設定步驟,順便附上 vscode 需要進行對應的設定步驟～

<!-- more -->

## 安裝還境:
- MacOS: Big Sur (11.4)

## Install homebrew

> Mac 使用這必裝的套件管理工具
> 

```bash
$ /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

若安裝時卡在 `download command line tools for xcode` 只須照著以下步驟更新即可

`system preferences` → `Software Update` → `More info` 勾選 xcode tool, 並更新，安裝完成後重新執行 homebrew 安裝指令即可

![](Untitled.png)

## Install iterm2

> 好用的 Terminal
> 

```bash
$ brew cask install iterm2
```

## Install zsh

> Z shell是一款可用作互動式登入的shell及指令碼編寫的命令直譯器。Zsh對Bourne shell做出了大量改進，同時加入了Bash、ksh及tcsh的某些功能。 (擷取自 wiki)
> 

檢查是否有 zsh, 新版的 MacOS 有內建 zsh 若已經安裝過 zsh 可以跳過此步驟

```bash
# check zsh installation status 
$ which zsh

# modify default shell to zsh.
$ chsh -s $(which zsh)
```

## Install oh-my-zsh

> 提供 zsh 配置, 主題, 插件 管理功能
> 

```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
```

## Install zsh theme: powerlevel10k

> 幫妳的 zsh 換上美觀的主題
> 

```bash
# download zsh theme: powerlevel10k
$ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k

# update zsh theme 
$ vim ~/.zshrc

# update config
ZSH_THEME="powerlevel10k/powerlevel10k"

# refresh terminal 
$ exec $SHELL
```

此時應該會請您進行一些基本外觀設定，依照個人喜好選擇即可

到這裡就完成基本的設定了~

## Update VSCode Config (Optional)

若是 VSCode 使用者此時應該會發現當中的 terminal 顯示會怪怪的，必須到 VSCode 中進行簡單的調整，以下擷取自: [https://github.com/romkatv/powerlevel10k/issues/671](https://github.com/romkatv/powerlevel10k/issues/671) 的分享

假設使用 powerlevel10k 預設的字體只需按照下方設定即可正常顯示

1. Open *Settings* in **Visual Studio Code**.
    - On PC: press  `Ctrl+,`
    - On Mac: press  `Cmd +,`

2. Enter `terminal.integrated.fontFamily` in the search box at the top of *Settings* tab and set the value below to `MesloLGS NF`.
    
    ![](https://raw.githubusercontent.com/romkatv/powerlevel10k-media/389133fb8c9a2347929a23702ce3039aacc46c3d/visual-studio-code-font-settings.jpg)
    
    完成設定後就可以看見 vscode 的 terminal 正常顯示了~
    
    ![](Untitled_1.png)
    

若使用其他的字體必須先下載字體再進行設定可以參照[文章](https://github.com/romkatv/powerlevel10k/issues/671)的分享設定。

感謝收看

## Reference

- [https://stackoverflow.com/questions/64310320/difference-between-iterm2-zsh-and-oh-my-zsh](https://stackoverflow.com/questions/64310320/difference-between-iterm2-zsh-and-oh-my-zsh)
- [https://www.onejar99.com/terminal-iterm2-zsh-powerlevel10k/#Step_2_zsh](https://www.onejar99.com/terminal-iterm2-zsh-powerlevel10k/#Step_2_zsh)

