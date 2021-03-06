# 0x01: エミュレータを作るために必要な"部品"

とまあ、めっちゃ恥ずかしいポエムはこれくらいにしておいて、具体的にエミュレータを開発するのに何が必要なのか考えて行きましょう。

エミュレータは、対象のコンピュータを模倣するプログラムです。今回はファミコンですが、ファミコン含めてゲーム機は所詮はただのコンピュータです。もうちょっとぼんやりと、一般的なコンピュータも交えながら、考えてみましょうか。

コンピュータは、何でできているでしょう。それらを全部ソフトウェアで再現することができれば、エミュレータができ上がるはずではないでしょうか…？

まずまっさきに思いつくのは、もちろんCPUです。それから、メモリ（Random Access Memory; RAM）。メモリからCPUが機械語を読みだしてプログラムを実行し、同じメモリ上の値を書き換える…というのが、コンピュータの基本的な動作です。

あと、現在のPCで言うところのHDDやSSDにあたる機構が必要です。メモリは電源を切ったら消えてしまいますから、お目当てのプログラム（今回は、ゲームですね）を読み込んだり、編集したデータ（今回なら、セーブデータですね）を保存したりするための、外部記憶装置が必要です。現在だとHDDやSSDが一般的ですが、昔は音楽テープ（！）とか、フロッピーとかを使っていました。一度書いたら書き換えることができませんが、ROM(Read Only Memory)もこのポジションにいます。他の媒体と比べてROMはデータがいきなり消えたりしにくいので、BIOSやゲームソフトのような、書き換える必要がないデータを格納する用途には適しています。ファミコンのカートリッジでも、プログラムや絵を記録するためにROMが使われています。

ここまではコンピュータの中だけの話ですが、もちろん、コンピュータ、特にゲーム機は人間からの操作に応じて動き、操作の結果起こったゲームの進行を見せてくれます。人間とコンピュータの間の架け橋になるようなパーツも、コンピュータに欠かせない一部分でしょう。

とりあえず、画面出力でしょうか。モニタに文字や画像（ファミコンなら、マリオとか！）を出力してくれなければ、何が起こっているのかわかりません。この画像出力処理はその時々のCPUにとって重い処理であることが多く、別のハードウェアに任せていたりすることが多いようです（現在でも、大体GPUがやっていますよね）。となると、CPU以外にそれらも再現しなきゃ…少し大変です。

あとは、コンピュータを操作できなければどうしようもありません。キーボードやマウス、ゲーム機のコントローラなどの、入力デバイスも必要です。ファミコンはコンピュータと違ってコントローラで操作しますが、コンピュータにはファミコンのコントローラは接続できませんから、パソコン用のUSBコントローラを、エミュレータでも利用できるようにしなきゃいけませんね。

最後に、音楽や効果音といったサウンドによっても、ゲームは私達を楽しませてくれます。サウンドの再生方法は、現在ではレコーディングした音声ファイルを再生することが多いですが、昔は直接音の波形を作るのが一般的で、しかも専用のハードウェアが行なっていることが多いようです。これもちょっと、やっかい。

さて、以上をまとめると、コンピュータを再現するために必要なものは、

- CPU
- メモリ（RAM）
- HDDとかSSD、フロッピー、カセットみたいな外部記憶装置
- ビデオ
- サウンド
- キーボードやコントローラのような入力装置

といった所。これらのパーツを、それぞれファミコンを模倣して実装して纏めあげれば、きっとエミュレータになるはず。
