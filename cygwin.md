# cygwin (+α Visual Studio Code)
## 項目
1. zsh に切替
2. cyg-fast
3. フォント変更
4. .zshrc, .minttyrc, .vimrc をDropboxで管理
5. Visual Studio Code のターミナルで zsh を使う  
6. その他便利な使い方

## 1. zshに切替
 1. zsh インストール
     * setup-x86.exe or cyg-fast(後述) でインストール

 2. bash → zsh に変更
     * chere パッケージをインストール
     * ターミナル起動時に以下のように引数を与える
     ```
     C:\cygwin64\bin\mintty.exe --window max -e /bin/xhere /bin/zsh.exe "C:\Users\username" -
     ```

[つるろぐ: Cygwin の ターミナル起動時のディレクトリを変える方法](http://fbe5c7f2.blogspot.jp/2013/10/cygwin.html)

## 2. cyg-fast
 1. 必要なパッケージをsetup-x86.exeでインストール
    * wget
    * aria2c
    * tar
    * gawk
 2. ソースを取得
 ```
 % git clone https://github.com/tmshn/cyg-fast
 ```
 3. cyg-fast を、パスが通っているディレクトリへ移動し、実行権限を付与
    ```
    % cp -p cyg-fast /bin/
    % chmod +x /bin/cyg-fast
    ```
 4. ミラーサイトを国内のサーバに変更しておく
    ```
    cyg-fast -m ftp://ftp.iij.ad.jp/pub/cygwin/ update
    ```
 5. 使い方一覧
    ```
    % cyg-fast find xxx #パッケージを探す
    % cyg-fast show xxx #パッケージの情報を見る
    % cyg-fast install xxx #パッケージをインストール
    % cyg-fast remove xxx #パッケージを削除
    ```
[Cygwin使うならcyg-fastも | うなすけとあれこれ](https://blog.unasuke.com/2014/cyg-fast-is-faster-than-apt-cyg/)  
[cyg-fastの紹介とknife soloの実行環境の作り方 - Qiita](http://qiita.com/d9magai@github/items/ff867393b7c257135e70)  
[Cygwinのターミナルエミュレータminttyの導入 - Qiita](http://qiita.com/d9magai@github/items/b988f4c881cfa1261512)

## 3. フォント変更
 1. 好きなフォントをOSにインストール
    * Windows の場合
      1. [コントロールパネル] > [デスクトップのカスタマイズ] > [フォント]
      2. フォントのファイル(*.tff)をドラッグ&ドロップ

 2. Cygwin の options で追加したフォントを設定 or .minttyrcに以下を追加

```
Font=Ricty Diminished
```
[edihbrandon/RictyDiminished: Ricty Diminished --- fonts for programming](https://github.com/edihbrandon/RictyDiminished)
## 4. .zshrc, .minttyrc, .vimrc をDropboxで管理
 1. シンボリックリンク作成
   ```
   % cd ~
   % ln -s /path_to_.zshrc .zshrc
   % ln -s /path_to_.minttyrc .mintty
   % ln -s /path_to_.vimrc .vimrc
   ```
[シンボリックリンクの作成と削除 - Qiita](http://qiita.com/colorrabbit/items/2e99304bd92201261c60)

 2. .zshrc, .minttyrc, .vimrc の設定  
 以下を参考に作成。  
[zshは至高の利便性？！Cygwinにzshをインストール＆設定した導入方法まとめ | Futurismo](http://futurismo.biz/archives/1363)  
[mintty ターミナル上の vim で、モードに応じてカーソル形状を変える - Qiita](http://qiita.com/usamik26/items/f733add9ca910f6c5784)

## 5. Visual Studio Code のターミナルで zsh を使う
 1. vscode_zsh.batを作成
 ``` 
 @echo off
 set CHERE_INVOKING=1 set MSYSTEM=MINGW64 & C:\\cygwin64\\bin\\zsh.exe --login -i
 ``` 
 2. Visual Studio Codeを開き、Settingsで以下を追記
  ```
  // コンソールをcygwinに変更
  "terminal.integrated.shell.windows": "C:\\cygwin64\\Cygwin.bat",
  ```
[Visual Studio CodeのIntegrated Terminalでmsys2のzshを使う - 備忘録β版](http://yami-beta.hateblo.jp/entry/2016/06/08/000000)

## 6. その他便利な使い方
 * Cygwin ⇔ クリップボード
    * シェル → クリップボード  
      とにかく、/dev/clipboardに送る
        ```
        % cat xxx > /dev/clipboard
        ```
    * vim → クリップボード  
      以下のコマンドでバッファ全体をクリップボードに送る
        ```
        :w !cat > /dev/clipboard
        ```
      以下のコマンドでビジュアルモードで選択した範囲をクリップボードに送る('<,'>部分は自動中入力される)
        ```
        :'<,'>w !cat > /dev/clipboard
        ```
    * クリップボードからのペースト  
    Ctrl-Shift-V または Shift-Ins

[cygwin vim でクリップボードを使う - Qiita](http://qiita.com/usamik26/items/f27fef5335752a3e37ec)
