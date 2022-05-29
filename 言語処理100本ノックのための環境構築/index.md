# 言語処理100本ノックのための環境構築


# はじめに
みなさんは言語処理100本ノックを知っていますか？
言語処理100本ノックとは東工大の岡崎直観先生らによって言語処理を楽しく学ぶことを目的として作成された問題集です。

https://nlp100.github.io/ja/

私の所属している研究室でも初学者向けの教材として利用されていますが、環境構築で躓いている人がかなりいたため、研究室内のページで環境構築の解説を作成しました。
しかし研究室内向けだけでは勿体ないと思い、この度Qiitanに投稿することにしました。
検索しても言語処理100本ノックのためのまとまった環境構築方法がなかったというのも大きな理由です。

# 注意
本記事で紹介している環境構築方法は言語処理100本ノックを解くことを主目的としているため、ほかの用途には適さなかったり、無駄が多かったりしますので、予めご了承ください。
また、本記事はWindowsユーザ向けなのでMacユーザの方は適宜読み替えたりしてください。
要望が上がればMac端末で動作を検証してからMac向けの記事を書くかもしれません。

# 環境構築
## まずはWSLを入れよう！
言語処理100本ノックを解く上で一番簡単かつ解きやすい環境としてWSLというものがあります。
これはubuntuと呼ばれるLinux系のOSをWindows内に仮想的に作れるようにしたツールで、2ステップで簡単に導入できます。
### ステップ1
Windows側でWSLが使用できるように機能を有効化します。
wiindowsボタンを押してから`windows`と検索して、`Windowsの機能の有効化または無効化`という項目をクリックしてください。
画像で言うと赤枠の部分です。
![Screenshot 2022-05-26 203219.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/842766/dba961af-7bfd-dcd2-920b-6249fe7d5b7b.png)
すると様々な項目が表示されるので、`Linux用Windowsサブシステム`にチェックを入れてください。
こちらも画像で言うと赤枠の部分です。
![Screenshot 2022-05-26 203608.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/842766/9d446ff4-3eb7-71ee-5e7d-4b4b54069027.png)
これでステップ1は完了です。

### ステップ2
続いてWSL本体のダウンロードです。
スタート画面などからMicrosoft Storeにアクセスして`ubuntu`と検索してください。
様々なバージョンが表示されますが、ここでは`Ubuntu20.04LTS`をダウンロードしましょう。（ちななみにLTSはLong Time Supportの略、つまり安定板のようなものです）
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/842766/55293614-3402-10a2-e5c0-40423295044d.png)
ダウンロード出来たらスタート画面などから先ほどダウンロードしたUbuntu20.04LTSを起動してください。

## Pyenvの導入
Pythonのバージョン管理に便利な`Pyenv`を導入します。
なぜバージョンなんて管理するの？と思われるかもしれません。
言語処理100本ノックを解く上では１つのバージョンで事足りますが、Pythonを使っていると使いたいライブラリが一定のバージョンにしか対応していないなどということがかなりの頻度で現れます。
そんなときにPyenvでバージョンを管理しておくと1つのコマンドを打つだけで好きなバージョンのPythonに切り替えることができます。よって本記事ではPyenvの使用を**強く推奨**します。
Pyenvの導入は簡単で、WSL上で以下のコマンドをすべて打つだけで終わりです。
```bash
# 依存パッケージの導入
$ sudo apt install -y build-essential
$ sudo apt install -y libffi-dev
$ sudo apt install -y libssl-dev # openssl
$ sudo apt install -y zlib1g-dev
$ sudo apt install -y libbz2-dev libreadline-dev libsqlite3-dev # sqlite3, bz2, readline
$ sudo apt install -y git
$ cd
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv
# .bashrcの更新
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
$ echo 'eval "$(pyenv init --path)"' >> ~/.bashrc
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc
$ source ~/.bashrc
 
# pyenvがインストールできたかを確認
$ pyenv -v 
```

以上のコマンドをすべて打ち終えた段階で、勝手にPyenvが導入完了しているはずです。
出来ていないようであればコメントください。

## Pyenvの使い方
```bash
# インストール可能なpythonのバージョンを表示
$ pyenv install --list
# pythonのインストール(3.8.10をインストールする場合)　
$ pyenv install 3.8.10
# 使うPythonのバージョンを3.8.10に切り替え
$ pyenv global 3.8.10
# 切り替わっているかの確認
$ python -V 
```

## 必要な諸ライブラリの導入
ダウンロードしたばかりのPythonには何のライブラリも入っていません。ですが、一から必要なライブラリをすべて羅列するのもなと思ったので、簡単にダウンロードできるようにファイルを用意しました。
[こちらのページ](https://github.com/Ryutaro-A/nlp-nock100-env/tree/main)に必要なライブラリが記載されたファイルがあるのでダウンロードして、`requirements.txt`のある場所で以下のコマンドを実行してください。
```bash
$ pip install -r requirements.txt
```
なお、私自身が解いた時に使用したライブラリであるため、このファイルには解き方によっては必要がないものもありますが、ご了承ください。
これで言語処理100本ノックに必要なPythonのライブラリに関してはすべて導入完了です。

## MeCabの導入(第4章で必要)
これに関してもコマンド2つで導入ができます。サクサク行きましょう！
```bash
$ sudo apt update
$ sudo apt install mecab mecab-ipadic-utf8 libmecab-dev swig
```

## CaboChaの導入(第5章で必要)
CabocChaは第5章で必要になる係り受け解析用ツールです。
まずは依存パッケージであるCRF++を導入します。
[このページ](https://drive.google.com/drive/folders/0B4y35FiV1wh7fngteFhHQUN2Y1B5eUJBNHZUemJYQV9VWlBUb3JlX0xBdWVZTWtSbVBneU0?resourcekey=0-NW5cPRv1Xr2-Vfo_xlDTLQ)から最新のものをダウンロードする（wgetでも出来なくはないけど上手くいかないこともある？）
`CRF++-0.58.tar.gz`のあるディレクトリで以下のコマンドを使う
```bash
$ tar xzvf CRF++-0.58.tar.gz
$ cd CRF++-0.58
$ ./configure
$ make
$ sudo make install
```
続いてCaboCha本体の導入です。
[このページ](https://drive.google.com/drive/folders/0B4y35FiV1wh7cGRCUUJHVTNJRnM?resourcekey=0-ym0BJTHMkjw3y1AEgwwaxA)からから最新のものをダウンロードする（wgetでも出来なくはないけど上手くいかないこともある？）
`cabocha-0.69.tar.bz2`のあるディレクトリで以下のコマンドを使う
```bash
$ tar xjvf cabocha-0.69.tar.bz2
$ cd cabocha-0.69
$ ./configure --with-charset=utf8
$ make
$ sudo make install
```
# おわりに
以上で言語処理100本ノックのための環境構築はすべて完了です！
それぞれのコマンドの意味の解説はしていないので知らずのうちに環境構築ができてしまったという感じだと思います。
その辺に関してもし知りたい場合は調べてください...w
もし分からない部分や「実行したのに動かない！」などがあれば気軽にコメントやTwitterのほうに連絡をください。
Twitterのほうが反応が早いです。



