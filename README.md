# これはなに？

Windows7でElectronの開発環境を構築するための手順をまとめたものです。

# 環境

Windows7 Professional Service Pack 1 (64bit)

# 手順

Node.jsのインストール手順は「[Windows の Node.js 開発環境構築 最小手順 - qiita.com/okamoai/](http://qiita.com/okamoai/items/a875b26abab7f18da7d1)」を参考にやります。

## 1. Git for Windowsのインストール

[git公式サイト](https://git-scm.com/download/win)より、最新版をDL&インストールします。
2016-12-20現在「Git-2.11.0-64-bit.exe」でした。

インストールウィザードは以下のように設定しました。

* Select Components
  * [ ] Additional icons
    * [ ] On the Desktop
  * [ ] Windows Explorer integration
    * [ ] Git Bash Here
    * [ ] Git GUI Here
  * [X] Associate .git configuration files with the default text editor
  * [X] Associate .sh files to be run with Bash
  * [X] Use a TrueType font in all console windows
* Adjusting your PATH environment
  * [ ] Use Git from Git Bash only
  * [X] Use Git from the Windows Command Prompt
  * [ ] Use Git and optional Unix tools from the Windows Command Prompt
* Choosing the SSH executable
  * [X] Use OpenSSH
  * [ ] Use (Tortoise)Plink
* Configuring the line ending conversions
  * [ ] Checkout Windows-style, commit Unix-style line endings
  * [ ] Checkout as-is, commit Unix-style line endings
  * [X] Checkout as-is, commit as-is
* Configuring the terminal emulator to use with Git Bash
  * [ ] Use MinTTY (the default terminal of MSYS2)
  * [X] Use Windows' default console window
* Configuring extra options
  * [X] Enable file system caching
  * [X] Enable Git Credential Manager
  * [ ] Enable symbolic links
* Configuring experimental options
  * [ ] Enable experimental, builtin difftool

gitをインストール後にコマンドプロンプトが文字化け（日本語が全部豆腐になる）するなら、以下の手順を試して下さい。
「[Windows Vista のコマンドプロンプトが文字化けしている場合の対処方法 - drk7.jp](http://www.drk7.jp/MT/archives/001461.html)」

## 2. Node.jsのインストール

Electron内蔵のNode.jsと同じバージョンをインストールします。
[Electron公式サイト](http://electron.atom.io/)を見ると以下のバージョンでした。

* Electron: 1.4.12
* Node: 6.5.0
* Chromium: 53.0.2785.143
* V8: 5.3.332.47

[Node.js v6.5.0のリリースページ](https://nodejs.org/en/blog/release/v6.5.0/)から、`node-v6.5.0-x64.msi`をDL&インストールします。

インストールウィザードは全てデフォルトを設定しました。

