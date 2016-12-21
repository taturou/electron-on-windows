# これはなに？

Windows7でElectronの開発環境を構築するための手順をまとめたものです。

と言っても、ElectronはNode.jsアプリなので、実質的にNode.jsの環境構築手順です。

---

# 環境

Windows7 Professional Service Pack 1 (64bit)

---

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

## PowerShell 5.0のインストール

~~あとでVSCodeによるデバッグ環境を整えるときに、シェルとしてPowerShellを使用します。~~
~~Windows7にはPowerShellがデフォルトでインストール済みですが、最新版ではない可能性があるので最新版をインストールします。~~

1. ~~https://msdn.microsoft.com/en-us/powershell/ へアクセス~~
2. ~~「Download WMF」から最新版のダウンロードページへ飛ぶ~~
    * ~~2016-12-21時点では「Download WMF 5.0」が最新でした~~
3. ~~「Windows Management Framework 5.0」ページで [Download] ボタンをクリックする~~
4. ~~「Win7AndW2K8R2-KB3134760-x64.msu」をチェックして [Next] ボタンをクリックする~~
5. ~~Win7AndW2K8R2-KB3134760-x64.msuを実行する~~

「インストーラーはエラーを検出しました: 0xc80003f3」エラーがでてインストールできず。

あとでPSReadLineを導入するときに`Import-Module PSReadLine`を使いたいので5.0にしたかったのですが、手動でもインストールできるので4.0でもOKです。

ちなみに、これを試したときのバージョンは以下の通りです。

```cmd
PS> $psversiontable

Name                           Value
----                           -----
PSVersion                      4.0
WSManStackVersion              3.0
SerializationVersion           1.1.0.1
CLRVersion                     4.0.30319.42000
BuildVersion                   6.3.9600.16406
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0}
PSRemotingProtocolVersion      2.2
```

## PowerShellでUNIXツールを使えるようにする

PowerShellで`grep`、`sed`、`awk`などを使えるようにします。

Git for Windowsの中にMinGW/MSYS2が入っているので、それを使います。
詳細は「[Mingw-w64/MSYS2 を入れなくても Git for Windows で間に合うみたい - 檜山正幸のキマイラ飼育記](http://d.hatena.ne.jp/m-hiyama/20151013/1444704189)」を参照。

ただ、環境変数PATHにパスを通すとMSYS1を使っている他のビルド環境と競合するので、PowerShellを使った時だけパスを通すようにします。
PowerShellの起動時にPATHを変更すればOK。

やり方は以下の記事を参照。

* [PowerShell/PowerShellで環境変数PATHにパスを追加する方法 ](http://win.just4fun.biz/PowerShell/PowerShell%E3%81%A7%E7%92%B0%E5%A2%83%E5%A4%89%E6%95%B0PATH%E3%81%AB%E3%83%91%E3%82%B9%E3%82%92%E8%BF%BD%E5%8A%A0%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95.html)
* [PowerShell/PowerShellコンソール起動時にスクリプトを実行する方法 ](http://win.just4fun.biz/PowerShell/PowerShell%E3%82%B3%E3%83%B3%E3%82%BD%E3%83%BC%E3%83%AB%E8%B5%B7%E5%8B%95%E6%99%82%E3%81%AB%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%97%E3%83%88%E3%82%92%E5%AE%9F%E8%A1%8C%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95.html)

以下を実施します。

1. PowerShellで `PS> $profile` を実行し、初期化スクリプトのパスを得る。
2. 初期化スクリプトに以下を記載する。

   ```cmd
   # Path to MSYS commands of Git for Windows
   $env:path += ';C:\Program Files\Git\mingw64\bin'
   $env:path += ';C:\Program Files\Git\usr\bin'
   ```

## PowerShellでemacsキーバインドを使えるようにする

PowerShellはemacsキーバインドが使えない（マジか！）ので、PSReadLineを導入する。

1. 「[github/lzybkr/PSReadline](https://github.com/lzybkr/PSReadLine)」から最新版をダウンロード。

    * 2016-12-21時点では[v1.2](https://github.com/lzybkr/PSReadLine/releases/download/v1.2/PSReadline.zip)でした。

2. zipを解答したものを以下にコピーする。

    * C:\Users\[User]\Documents\WindowsPowerShell\modules\PSReadline

3. 初期化スクリプトに以下を記載する。

    ```cmd
    # for PSReadLine
    if ($host.Name -eq 'ConsoleHost')
    {
        Import-Module PSReadline

        # emacsキーバインド
        Set-PSReadlineOption -EditMode Emacs

        # ベルを表示しない
        Set-PSReadlineOption -BellStyle None

        # 同じコマンドはhistoryに記録しない
        Set-PSReadlineOption -HistoryNoDuplicates
    }
    ```

---

# ElectronのQuick Startを試してみる

準備が長すぎて目的を忘れそうになりましたが、このドキュメントはElectronの環境構築でしたね。

やっと環境構築が終わったので、実際に動くか試してみます。

[Electronの公式サイト](http://electron.atom.io/)に、とりあえず試せる手順が書いてあるので、それを実施してみます。

PowerShellで以下を実行してください。

```cmd
PS> cd /path/to/work/directory/
PS> git clone https://github.com/electron/electron-quick-start
PS> cd electron-quick-start
PS> npm i
PS> npm start
```

ウィンドウがひとつ開き、「Hello World」が表示されれば成功です。

---

# Visual Studio Codeでデバッグする

ElectronのGUIはChroniumなので、Chromeの「デベロッパーツール」でデバッグできます。
しかし、エディタでコード書いてブレイクポイント貼って実行してデバッグできたほうが楽ですよね。
デベロッパーツールだと、ウィンドウが出た後しかデバッグできないし。

そこで、Microsoft社製「Visual Studio Code（VSCode）」でデバッグできるようにします。

## Visual Studio Codeのインストール

[VSCodeの公式ページ](https://code.visualstudio.com/)から最新版をDL＆インストール。

2016-12-20現在「VSCodeSetup-1.8.1.exe」でした。

## プラグインのインストール

VSCodeに、以下のプラグインをインストールします。

* npm - npm commands for VSCode

（`Ctrl+Shift+p`からnpmが叩けるのは良いんだけど、npmを知らない人向けにコマンドがラッパーされてて素のコマンドが通らないので使いづらい…）

## 統合シェルをPowerShellに変更する

本当はbashを使いたいけど、MSYSもCygwinも重いのでしょうがなくPowerShellを使います。
CMDよりは随分マシなので。

「[Visual Studio CodeのターミナルをPowerShellに変える際に注意すべきこと - 素敵なおひげですね](http://stknohg.hatenablog.jp/entry/2016/06/10/180732)」を参考に以下を設定します。

VSCodeの「ファイル」メニュー→「基本設定」→「ユーザ設定」で、settings.jsonを開いて、以下を追加します。

```json
"terminal.integrated.shell.windows": "C:\\Windows\\Sysnative\\WindowsPowerShell\\v1.0\\powershell.exe"
```
## PowerShellでemacsのキーバインドを使えるようにする

なんだかデジャヴ。

さっきやったきがしますが、VSCodeからPowerShellを使うときにはもう一段階の設定が必要です。
PowerShellのキーバインドは変更されていても、VSCodeのキーバインドが競合するためです。
具体的には`Ctrl+p`、`Ctrl+n`、`Ctrl+k`などが別の機能に割り当てられており、それがPowerShellに渡りません。

以下の手順を実施します。

1. 「ファイル」メニュー→「基本設定」→「キーボードショートカット」で`keybindings.json`を開く。
2. `keybindings.json`に以下を追記する。

    ```json
    // ターミナルでemacsキーバインドと競合するのを解消する
    { "key": "ctrl+k", "command":"", "when": "terminalFocus"},
    { "key": "ctrl+p", "command":"", "when": "terminalFocus"},
    { "key": "ctrl+n", "command":"", "when": "terminalFocus"},
    { "key": "ctrl+e", "command":"", "when": "terminalFocus"}
    ```

## プロジェクトフォルダーを開く

VSCodeで、先ほどの`electron-quick-start`フォルダを開きます。

## デバッグの設定

VSCodeでElectronアプリケーションをデバッグできるように設定します。

1. `Ctrl+Shift+D`でデバッグ画面を開きます。
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

## デバッグ
 
1. `Ctrl+Shift+D` でデバッグ画面を開きます。
2. 「デバッグの開始」ボタンでElectronアプリケーションが起動します。
