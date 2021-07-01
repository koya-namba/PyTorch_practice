# PyTorch_practice
このリポジトリは，PyTorchの勉強，実装を記録したものである．

深層学習を知っている状態から使える状態にするためにこのリポジトリを作成した．

## 勉強内容
- オリジナルデータを用いて，線形回帰の実装
- MNISTデータを用いて，MLPの実装
  - モデルの保存
- CIFAR10を用いて，CNNの実装
  - データ拡張
- 転移学習
  - データのダウンロードとフォルダの扱い方
- オートエンコーダー
- ResNet
  - 残差学習
- カスタムデータセットの作成
- LSTM
  - RNN

## 実装
- 275 Bird Species also see 73 Sports Dataset
  - CNN(自分で作ったモデル)
  - VGG(転移学習)

## 勉強日記
2021/6/26
- オリジナルデータを用いた線形回帰の実装
  - データの入力の順番には気をつける必要がある．(バッチ数，チャネルファースト）
  - modelに与えたデータを図示するときは，detach
  - 学習中は，optimizerの初期化を忘れないように

- MNISTデータを用いたMLPの実装
  - gpuを使うときは，デバイスの確認
  - DataLoaderでミニバッチの作成
  - dataloaderはiterできる
  - データを表示するときは，numpyや配列，次元に気をつける必要がある．
  - 学習するときは，モデル，画像，ラベルをGPUに送ること

2021/6/27
- CIFAR10のデータを用いたCNNの実装
  - 画像には，Normalizeが必要である．
  - モデルを構築するときは，CNNと全結合層で分ける必要がある．
  - 全結合層に入れる前には，データの型に気をつける．
  - 学習・検証では，変数名に気をつける．
  - 簡単にデータ拡張を実装することができるため，過学習の時は試す価値がある．

2021/6/28
- ResNetを用いて，転移学習の実装
  - modelをtorchvisionからダウンロード可能
  - 画像サイズが異なるときは，transforms.Resizeで揃える．
  - フォルダにラベルがついているときは，dataset.ImageFolderで簡単にデータセットを作成可能
  - モデルをそのまま使うときは，pretrained=Trueとする．
  - 最後の層だけ変更することも可能．(model.fc=nn.Linear(512, 2)
  - optimizerには，勾配を更新するパラメータだけを与える．

- MNISTデータを用いてオートエンコーダーの実装
  - エンコードするときは，他の学習とほぼ違いなし．
  - デコードするときは，Upsampling(scale_factor)を用いる．
  - 損失関数には，MSELossを用いる．
  - 学習時にはラベルを使わない．
  - データを実際に見るためには，i番目のデータをチャネルラストに変更して，勾配を引き離し，cpuにデータを送り，1個目のチャネルを表示する必要がある．

2021/6/29
- ResNetの実装
  - 畳み込み層が非常に深いため学習に時間を要する．
  - 残差学習とミニバッチの正規化を行うことで，学習を安定させている．
  - モデルの構築の仕方は，ブロックとモデルを分けて構築する．
  - ブロックの中では，スキップの扱い方に注意
  - モデルの中では，いつも通りな感じ

- カスタムデータセットの作成
  - データをgoogle colabに送る方法

- LSTMの実装
  - シーケンスの作成が必要になる．関数を用いて作成．
  - データに対しては，tensorに変換と３次元にする必要がある．
  - 順番は，シーケンス，バッチサイズ，入力の次元（入力の個数とは異なるので注意）

2021/6/30
- 275 Bird Species also see 73 Sports Dataset
  - CNNを用いて実装。
  - ローカルのGPUだとメモリが不足するからバッチサイズには注意が必要。
  - バッチサイズと学習率の考慮が大切

2021/7/1
- 275 Bird Species also see 73 Sports Dataset
  - VGGの実装。
  - 転移学習が見事に失敗。
  - バッチサイズを増やして、明日チャレンジ。

2021/7/2
- 275 Bird Species also see 73 Sports Dataset
  - VGG16を一から学習させることにより、高精度を獲得！
  - 少し過学習が起こっていたので、もう少しエポック数を減らしてもいいかもしれない。
