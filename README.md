# WSL-emacs 環境構築
基本はここを参考に
* [WSL で emacs を使うための設定 - NTEmacs @ ウィキ - アットウィキ](https://www49.atwiki.jp/ntemacs/pages/69.html)

## 基本

1. とりあえずアップデート

    ```
    $ sudo apt update
    $ sudo apt upgrade
    ```

2. locale変更と日本語マニュアルインストールとタイムゾーン変更

    ```
    $ sudo apt install language-pack-ja language-pack-gnome-ja
    $ sudo update-locale LANG=ja_JP.UTF-8
    $ sudo apt install manpages-ja manpages-ja-dev
    $ sudo dpkg-reconfigure tzdata
    ```

3. emacsインストール

    ```
    $ sudo apt install emacs25 emacs25-el
    ```

4. [vcxsrv](https://sourceforge.net/projects/vcxsrv/)か[X410](https://www.microsoft.com/ja-jp/p/x410/9nlp712zmn9q)をインストール

5. ~/.bashrcに追記

    ```bash
    if [ "$INSIDE_EMACS" ]; then
        TERM=eterm-color
    fi

    export DISPLAY=localhost:0.0
    ```

6. フォント共有設定

    ```
    $ sudo ln -s /mnt/c/Windows/Fonts /usr/share/fonts/windows
    $ sudo fc-cache -fv
    ```

## 日本語入力関連
1. [mozc_emacs_helper](https://github.com/smzht/mozc_emacs_helper)をダウンロードして適当な場所に保存（以下ではC:\Users\cirale\wsl\に保存した前提）

2. mozc_emacs_helper.sh を以下の内容で作成し、実行権を付加(chmod +x)した後、コマンドパスが通ったディレクトリ(/usr/local/bin や ~/bin 等)に格納

    ```bash
    #!/bin/sh

    cd /mnt/c/Users/cirale/wsl/
    ./mozc_emacs_helper.exe "$@"
    ```
