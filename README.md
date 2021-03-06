# SoundTest
先輩が提供してくれた音声再生ライブラリの使用方法説明用サンプルです。

## 音声再生ライブラリ使用手順
### 事前準備
1. DirectSound.hとSoundManager.hを自身のプロジェクトディレクトリ内に配置する。  
  本サンプルではプロジェクトファイルと同階層にSoundLibフォルダを作成し、その中に置きました。
1. Sound.lib(Debug用、Release用両方)を自身のプロジェクトディレクトリ内に配置する。  
  本サンプルでは手順1.で作成したSoundLibフォルダの中にDebugとReleaseのフォルダを作成しました。
1. ヘッダファイルとライブラリファイルのpathを通す  
  本サンプルではライブラリファイルのpathだけを設定し、ヘッダファイルはinclude時に相対pathを指定しています。  
  その辺りはお好みで設定して下さい。  
  ライブラリについては、Debugビルド時にはDebug用を、Releaseビルド時にはRelease用をリンクするようpathを設定して下さい。
1. リンクするライブラリにSound.libを追加  
  本サンプルではプロジェクトのプロパティから追加しましたが、ソースコード内で`pragma comment(lib, "Sound.lib")`としても良いと思います。
1. 音声ファイルを用意する  
  wavファイルにしか対応していないので、mp3等の圧縮ファイルはwavに変換して使用して下さい。  
  BGMは[フリーBGM・音楽素材MusMus](http://musmus.main.jp/music_game.html)様から、SEは[無料効果音で遊ぼう！](http://taira-komori.jpn.org/index.html)様からDLしました。  
  いずれもmp3形式だったので[Online Audio Converter](https://online-audio-converter.com/ja/)でwavに変換しました。

### プログラム内でのライブラリ使用方法
1. DirectSound.hとSoundManager.hをinclude (SoundTest.cpp L.7～11参照)
1. 音声再生ライブラリの初期化 (SoundTest.cpp L.117～121参照)
1. 必要な音声ファイルのロード (SoundTest.cpp L.123～130参照)  
  本サンプルではウィンドウ生成のタイミングで全てロードしていますが、シーン切り替え時に次のシーンで必要なものだけをロードする等、工夫して下さい。
1. 音声ファイルのロード (SoundTest.cpp L.180～205参照)  
  PでBGMの再生、Sで停止、上下左右カーソルキーでSEの再生をするようなプログラムにしています。  
  BGMはループON、SEはワンショットにしています。  
  こんな感じで、必要なタイミングで必要なファイルを再生するプログラムを書けば音が鳴ります。  
  サンプルではファイル名を直接指定していますが、実際にプログラムする際はテクスチャと同様にファイル名の配列を作ってenumで管理する等、工夫して下さい。

### Releaseビルド時にリンクエラーが出る場合
```
エラー	C1047	他のオブジェクトよりも古いコンパイラで作成されました。古いオブジェクトおよびライブラリをリビルドしてください
```
のようなリンクエラーが発生する場合は、`プロジェクトのプロパティ→全般→プログラム全体の最適化`で`プログラム全体の最適化なし`に設定するとリンクが通ると思います。
