---
title: "Raspberry Pi５で電子工作を始めるときに読む記事"
emoji: "🔧"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["RaspberryPi", "電子工作", "初心者向け"]
published: true
---

## 本稿の目的

Raspberry Piを使った電子工作を始めてみたい初心者に、電子工作スターターキットをお勧めし、電子工作を始められるようにすることが目的です。
（私自身が電子工作をよく理解しておらず、いきなりはんだ付けが必要なセンサーを単体で買って3,000円使ってしまったため…）
今回は、SunFounder の Raphael Ultimate Kit を使って、パーツとRaspberry Piを接続する基本部品を準備します。

## 前提

- Raspberry Pi 5 を所持している

## 1. Raphael Ultimate Kit とは

SunFounder が販売している Raspberry Pi 向けの電子工作学習キットです。LED、抵抗、センサー、モーターなど、様々な電子部品がセットになっており、これ1つで多くの電子工作プロジェクトを体験できます。
日本語の公式オンラインマニュアルがあるので、何から始めるか迷うこともありません。

公式オンラインマニュアル: [Raphael Kit - SunFounder](https://docs.sunfounder.com/projects/raphael-kit/ja/latest/)

## 2. Raphael Ultimate Kit を注文する

Raphael Ultimate Kit は Amazon で購入できます。

@[card](https://www.amazon.co.jp/dp/B09BMSS41D)

:::details 他のキットも検討したい場合

### SunFounder スターター電子工作キット（Raspberry Pi 対応）

Ultimate に比べてパーツ数は少ないですが、その分安価なスターターキットです。Raphael Kit より小規模でコスパよく試したい場合に。Raspberry Pi メインボードは別売りです。

@[card](https://www.amazon.co.jp/dp/B083SJQXCL)

### SunFounder スターターキット究極版（Raspberry Pi Pico W 対応）

450点以上のパーツと117プロジェクトを収録した大容量キットです。Raspberry Pi Pico W が入っているので、Raspberry Piを持っていない場合にも〇。

@[card](https://www.amazon.co.jp/dp/B0BDFVL6FX)

:::

## 3. Raphael Ultimate Kit の内容物

キットには多くの電子部品が含まれていますが、今回のセットアップで使う部品は以下です。

- ブレッドボード
- GPIO拡張ボード（T型）
- 40ピン GPIO フラットケーブル（リボンケーブル）

## 4. Lチカに必要な重要部品

![ブレッドボードとGPIO拡張ボード](/images/rapael-kit-1/breadboard_and_gpio_board.jpg)
*左がブレッドボード、右がGPIO拡張ボード。この2つをセットで使う。*

### ブレッドボード

電子工作とは、電子回路を組むことです。ブレッドボードは、はんだ付けなしで電子回路を組むことができる基板です。穴に部品やワイヤーを差し込むだけで回路を構成できます。

ブレッドボードは内部で電流の通り道ができています。

- **中央エリア**（部品を挿す主な領域）: 同じ行の穴が**横方向**に5つずつつながっています。例えば a1〜e1 は内部でつながっており、f1〜j1 も同様です。真ん中の溝を挟んで左右は**つながっていません**。
- **電源ライン**（両端の赤・青のライン）: 穴が**縦方向**にすべてつながっています。赤（+）に電源、青（−）にGNDを繋いで使います。

以下の回路図（LEDを例）で確認してみます。
![ブレッドボードの回路図](/images/rapael-kit-1/blinking_led_circuit.jpg)
*出典: [1.1.1 Lチカ — SunFounder Raphael Kit](https://docs.sunfounder.com/projects/raphael-kit/ja/latest/python_pi5/pi5_1.1.1_blinking_led_python.html)（原図を時計回りに90度回転）*

- **中央エリア**
  - LEDの右の線と抵抗の上側の、中央エリアの横方向が一致しているので**つながっている**
- **電源ライン**
  - 抵抗の下側と黒線の下側の、電源ラインの縦方向が一致しているので**つながっている**

このように、中央エリア・電源ラインがつながることで回路を組みます。

### GPIO拡張ボード

Raspberry Pi の 40ピン GPIO ヘッダーを物理的に延長し、ブレッドボードとの接続を容易にする周辺機器です。
先ほどの回路図の赤色T字の部分がGPIO拡張ボードです。
![ブレッドボードの回路図](/images/rapael-kit-1/blinking_led_circuit.jpg)
*出典: [1.1.1 Lチカ — SunFounder Raphael Kit](https://docs.sunfounder.com/projects/raphael-kit/ja/latest/python_pi5/pi5_1.1.1_blinking_led_python.html)（原図を時計回りに90度回転）*

つまり、

- 青線の左端とGPIO拡張ボードの「GPIO17」が、中央エリアの横方向で一致しているのでつながっている
- GPIO拡張ボードはRaspberry Piとつながっているため、結果として青線とRaspberry Piがつながっている

### 40ピン GPIO フラットケーブル

Raspberry Pi と GPIO拡張ボードを接続するためのリボンケーブルです。

![40ピン GPIO フラットケーブル（リボンケーブル）](/images/rapael-kit-1/kit_packing_list.jpg)
*リボンケーブルの外観*

## 5. セットアップ手順

### ブレッドボードに GPIO拡張ボードを挿す

1. ブレッドボードの**真ん中の溝をまたぐ**ように GPIO拡張ボードを配置する
2. **GPIO拡張ボードのピンが見えなくなるまで**しっかり押し込む（結構力が必要。ビビって手に持ちながら押し込んだらブレッドボードが曲がった）

![GPIO拡張ボードのピン部分](/images/rapael-kit-1/gpio_board_pins.jpg)
*押し込んだ状態。見えなくなるまでしっかり押す。*

### Raspberry Pi とブレッドボードを繋ぐ

1. 40ピン GPIO フラットケーブルで GPIO拡張ボードと Raspberry Pi を接続する
2. ケーブルの向きに注意して、**しっかり奥まで差し込む**（こちらも力が必要）

![GPIO拡張ボードにフラットケーブルを挿しているところ](/images/rapael-kit-1/gpio_board_insert.jpg)
*拡張ボードの真ん中の溝とケーブルの挿し口の溝を合わせて、しっかり奥まで押し込む。*

![Raspberry Pi にリボンケーブルを接続した状態](/images/rapael-kit-1/raspi-cable.jpg)
*Raspberry Pi側も同様にしっかり奥まで差し込む。*

## あとがき

これで Raphael Ultimate Kit とRaspberry Piが接続されている状態まで準備できました。次回の記事では、実際に LED を点灯させていきます。

![セットアップ完了後の状態](/images/rapael-kit-1/complete.jpg)
*次回はこの状態を作って、LEDを点灯させます。*

## 参考

- [SunFounder Raphael Kit 公式ドキュメント](https://docs.sunfounder.com/projects/raphael-kit/ja/latest/)
- [Raspberry Pi で L チカ - Qiita](https://qiita.com/RyoWakabayashi/items/bda56ee6987b30857266)
- [ブレッドボードとは？仕組みと使い方をざっくり解説](https://zakkuri-kaisetsu.com/breadboard/)
