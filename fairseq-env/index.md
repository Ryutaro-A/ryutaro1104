# Google Colabでfairseq入門


## はじめに
こんにちは！りゅうです。<br><br>
今日は最近？流行っているfairseqをColabを使って簡単に動かす方法を紹介します。<br>
私が指導教授や研究室の同期に触発されて、Colabで動かそうと思ったときにそのままでは動かなかったので備忘録としてその手順をここに書いておこうと思います。（ちなみに1回動かして以降使ってない・・・）<br>

ちなみにfairseqとは、Facebookの人工知能研究チームが開発した機械学習用(主にTransformer)のフレームワークです。<br>
Pytorchで作成されていることから有志によって確立された改造方法も存在し、論文でも見かけたりと、研究でも使われるようになっていると思います。<br>
以下公式GitHub↓<br>
<iframe class="hatenablogcard" style="width:100%;height:155px;max-width:680px;" title="facebookresearch/fairseq: Facebook AI Research Sequence-to-Sequence Toolkit written in Python." src="https://hatenablog-parts.com/embed?url=https://github.com/facebookresearch/fairseq" width="300" height="150" frameborder="0" scrolling="no"></iframe><br>

## 参考
<iframe class="hatenablogcard" style="width:100%;height:155px;max-width:680px;" title="importlib_metadata.PackageNotFoundError: No package metadata was found for fairseq · Issue #2546 · facebookresearch/fairseq" src="https://hatenablog-parts.com/embed?url=https://github.com/facebookresearch/fairseq/issues/2546" width="300" height="150" frameborder="0" scrolling="no"></iframe><br>

## fairseqの導入
fairseqのインストールは公式Githubにあるものをそのままコピーして使います。<br>
```sh
git clone https://github.com/pytorch/fairseq
cd fairseq
pip install --editable ./
```
上記コマンドでインストールしてから<br>
```sh
fairseq-train

#エラー文
No package metadata was found for fairseq
```
コマンドを試しに打ってみた際に発生したエラーです。<br>
公式githubのissueによるとパスが通っていないことが原因のようでした。<br>
そこで以下のように`PYTHONPATH`にfairseqがある場所を追加してあげます。<br>
```py
import os
os.environ['PYTHONPATH'] += ":/content/fairseq/"

! echo $PYTHONPATH
```
この操作でパスが通って`fairseq-train`などのコマンドが使えるようになります。<br>
fairseq本体ディレクトリのパスさえ通せばいいので、パスの部分は適宜書き換えて使ってみてください。<br>
それでは良きfairseqライフを。<br>






