﻿# EasyLightChatAssistant

EasyLightChatAssistant は軽量で検閲や規制のないローカル日本語モデルの[LightChatAssistant](https://huggingface.co/Sdff-Ltba/LightChatAssistant-2x7B-GGUF) を、[KoboldCpp](https://github.com/LostRuins/koboldcpp) で簡単にお試しする環境です。

## 動作環境

- 最近の NVIDIA ビデオカードを積んだ Windows PC で動作します。
	- RAM・VRAM・ストレージの必要容量は使用するモデルによります。  
	- 最低動作環境としては RAM 16GB と VRAM 4GB 程度でも、`iq3xxs_L0` ならそこそこ動作するはずです。
	- KoboldCpp を直接設定すれば、Radeon や CPU でも動作するはずです。

## インストール

1. [`Install-EasyLightChatAssistant.bat`](https://github.com/Zuntan03/EasyLightChatAssistant/raw/main/Install-EasyLightChatAssistant.bat?v=2) を右クリックからダウンロードして、インストール先のフォルダでダブルクリックして実行します。
	- **`WindowsによってPCが保護されました` と表示されたら、`詳細表示` から `実行` します。**
	- ダウンロードして利用するファイルに問題がなければ `y` を入力します。
1. プログラム起動用の `EasyLightChatAssistant-[量子化レベル]_L[GPU レイヤー数].bat` が複数生成されますので、環境にあった bat を実行します。
	- **VRAM 12GB 以上なら `iq3xxs_L33`(か `q4_k_m_L24`)、6GB~8GBなら `iq3xxs_L11`、4GB以下なら `iq3xxs_L0` を実行します。**
		- GPU レイヤー数を上げると動作が早くなります。
		- 量子化レベルのビット数を `q3` から `q4`, `q6`, `q8` に上げると、必要メモリが増えて動作も遅くなりますが、精度が高くなります。
	- `Windows セキュリティ` のネットワークへのアクセス許可は `キャンセル` でも動作します。
1. Web ブラウザに `Kobold AI Lite` が表示されましたら、画面上部の `Settings` から KoboldCpp の初期設定をします。
	- `Max Ctx. Tokens`: `32768`
	- `Amount to Gen.`: `512`
	![](./img/Settings.png)

## Instruct モードでお試し

KoboldCpp には様々なモードがありますが、今回は Instruct モードで文章の続きを生成します。

初回起動時はすでに Instruct モードになっています。  
もし他のモードにしていた場合は、画面上部の `Scenarios` から `New Instruct` を選択してください。

![](./img/Control.png)

1. **右下の `Submit` ボタンの上にある `Allow Editing` を有効にします。**
1. 出力欄を直接編集して、続きを書かせたい文章を記入します。
1. 右下の `Generate More` で続きの文章が生成されます。

![](./img/Generate.png)

- 生成されている文章の方向性が意図にそぐわない場合は、`[ABORT]` で生成を止めて、`Retry` で再生成します。
- 生成された文章を手直ししたい場合は、出力欄を直接編集します。
- `Generate More` でさらに続きを生成します。

## 『痴人の愛』のあらすじから文章を生成してみる

「痴人の愛 あらすじ」で Google 検索すると、AI があらすじを用意してくれました。

![](./img/StoryLine.png)

これを以下のように入力して生成し、良さげな目次を選びます。  

```
ストーリーライン：
主人公の河合譲治は、カフェで働く15歳のナオミと出会い、妻にします。
しかし、ナオミは予想もしなかった女性へと変貌していきます。
譲治はナオミを自分好みの女性に育て上げようとしますが、
奔放で妖艶さを増すナオミに溺れ振り回されます。

文体：
ハードコアポルノ。おとなしい河合譲治の一人称視点。

目次：
```

良さげな目次を用意できたら、各章を順に生成します。  
意図にそぐわない進行をしたら、直接編集して軌道修正します。  
軌道修正しつつ生成ガチャを回して、良い結果を拾い上げる使い方です。

![](./img/Story.png)

## TIPS

- LightChatAssistant は省サイズで動作が高速ですが、賢いわけでは有りません。
	- それっぽい続きの文章をいくつも出力して、出力結果を人が選ぶ運用が向いています。
	- Geforce RTX 3060 12GB 環境では、`iq3xxs_L33` の速さも良いのですが、`q4_k_m_L24` の文章も良さげです。
- 文体・ルール・章立て・あらすじなどを記載しておくことで、生成文章をある程度コントロールできます。
	- 適当な好みの文章を入力して、雑に続きを生成することもできます。
- ローカル動作のため、検閲や規制がありません。
	- [オンラインサービス向けのプロンプト](https://rentry.org/gpt0721) などから脱獄部分を取り除いても、ちゃんと続きを生成できます。  
	ただし、キャラのパラメータ操作といった賢さを必要とする文章の生成は、得意ではありません。
- KoboldCpp には他にも多数の機能があります。  
直接 `koboldcpp.exe` を起動すれば、自由に利用できます。
	- [Kobold.cppで小説っぽいのを作る](https://w.atwiki.jp/localmlhub/pages/19.html)
	- [Memory, Author's Note and World Info](https://github.com/KoboldAI/KoboldAI-Client/wiki/Memory,-Author's-Note-and-World-Info)
	- ただし、KoboldCpp には短い文章しか生成できなかった頃のための機能もあります。  
	32K コンテキストで長い文章を利用できるため、設定も含めて雑に書き連ねた文章から続きを生成することもできます。

## ライセンス

このリポジトリの内容は [MIT License](./LICENSE.txt) です。
