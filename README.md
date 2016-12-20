# これはなに？

Windows7でElectronの開発環境を構築するための手順をまとめたものです。

と言っても、ElectronはNode.jsアプリなので、実質的にNode.jsの環境構築手順です。

# 環境

Windows7 Professional Service Pack 1 (64bit)

# インストール手順

Node.jsのインストール手順は「[Windows の Node.js 開発環境構築 最小手順 - qiita.com/okamoai/](http://qiita.com/okamoai/items/a875b26abab7f18da7d1)」を参考にやります。

## 1. Git for Windows 2.11.0のインストール

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

## 2. Node.js 6.5.0のインストール

Electron内蔵のNode.jsと同じバージョンをインストールします。

[Electron公式サイト](http://electron.atom.io/)を見ると以下のバージョンでした。

* Electron: 1.4.12
* Node: 6.5.0
* Chromium: 53.0.2785.143
* V8: 5.3.332.47

[Node.js v6.5.0のリリースページ](https://nodejs.org/en/blog/release/v6.5.0/)から、`node-v6.5.0-x64.msi`をDL&インストールします。

インストールウィザードは全てデフォルトを設定しました。

## 3. .NET Framework ~~4.5.1~~ 4.6.1のインストール

「[Windows Vista SP2、Windows 7 SP1、Windows 8、Windows Server 2008 SP2、Windows Server 2008 R2 SP1、および Windows Server 2012 用 Microsoft .NET Framework 4.5.1 (Web インストーラー)](https://www.microsoft.com/ja-JP/download/details.aspx?id=40773)」をインストールします。

と思ったら、既に 4.6.1 がインストール済みでした。

バージョンが高い分には問題ないかな？
そのままにします。

## 4. Visual C++ Build Tools 2015のインストール

[Visual C++ Build Tools公式ページ](http://landinghub.visualstudio.com/visual-cpp-build-tools) より、最新版をDL&インストールします。

インストールウィザードは全てデフォルトを設定しました。

（超長かった！）

## 5. Python 2.7.13のインストール

[pythonの公式ページ](https://www.python.org/downloads/)より、2.7系の最新版をDL&インストールします。

2016-12-20現在「Python 2.7.13」でした。

## 6. npm標準オプションの変更

npmにpytonとVisual C++ Build Toolsのバージョンを教えます。

PowerShellで以下を実行してください。

```cmd
> npm config set python python2.7
> npm config set msvs_version 2015
```

設定されたか確認します。

```cmd
> npm config list
; cli configs
user-agent = "npm/3.10.3 node/v6.5.0 win32 x64"

; userconfig C:\Users\h-morishita\.npmrc
msvs_version = "2015"
python = "python2.7"

; builtin config undefined
prefix = "C:\\Users\\h-morishita\\AppData\\Roaming\\npm"

; node bin location = C:\Program Files\nodejs\node.exe
; cwd = C:\Users\h-morishita
; HOME = C:\Users\h-morishita
; "npm config ls -l" to show all defaults.
```

# ElectronのQuick Startを試してみる

[Electronの公式サイト](http://electron.atom.io/)に、とりあえず試せる手順が書いてあるので、それを実施してみます。

PowerShellで以下を実行してください。

```cmd
> cd /path/to/work/directory/
> git clone https://github.com/electron/electron-quick-start
> cd electron-quick-start
> npm i
> npm start
```

# Visual Studio Codeでデバッグする

## Visual Studio Codeのインストール

[VSCodeの公式ページ](https://code.visualstudio.com/)から最新版をDL＆インストール。

2016-12-20現在「VSCodeSetup-1.8.1.exe」でした。

### プラグインのインストール

VSCodeに、以下のプラグインをインストールします。

* npm - npm commands for VSCode

## フォルダーを開く

VSCodeで、先ほどの`electron-quick-start`フォルダを開きます。

## デバッグの設定

VSCodeでElectronアプリケーションをデバッグできるように設定します。

1. 「デバッグ」ボタンを押しデバッグの設定画面を開きます。
2. 「歯車」ボタンを押して`launch.json`を作成します。
3. 以下のとおりに修正してください。
   `runtimeExecutable`と`console`がポイントです。
   
    ```json
    {
      "version": "0.2.0",
      "configurations": [
        {
          "type": "node",
          "request": "launch",
          "name": "プログラムの起動",
          "program": "${workspaceRoot}\\main.js",
          "cwd": "${workspaceRoot}",
          "runtimeExecutable": "${workspaceRoot}\\node_modules\\.bin\\electron",
          "runtimeArgs": [
            "--enable-logging"
          ],
          "args": [
            "."
          ],
          "console": "integratedTerminal"
        },
        {
          "type": "node",
          "request": "attach",
          "name": "プロセスに添付",
          "port": 5858
        }
      ]
    }
    ```
    
4. 「デバッグの開始」ボタンでElectronアプリケーションが起動します。
