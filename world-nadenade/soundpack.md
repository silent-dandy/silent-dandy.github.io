---
title: 音源を用意する
description: 自分の音源を音色にするときの注意、ジェネレーターで音源を作る方法、追加音源パックの作り方です。
---

## 自分の音源を使うときの注意

World Nadenade の音は、ワールドのデータに含まれて**訪れた全員の端末に配られ、誰でも鳴らせる状態**になります。音源を足すときは、その音源の規約が「VRChat のワールドに組み込んで、不特定の訪問者に聞かせること」を認めているか、必ず確かめてください。

> **アバター用のなで音ギミックに付属する音源は、ワールドへの組み込みが禁止されていることが多く、権利者の許可がない限り使えません。** 市販・無料の効果音素材も、配布元の規約を確かめてください。

権利をはっきりさせたいときは、自分で録音した音や、次のジェネレーターで作った音を使うのが確実です。

## ジェネレーターで作る

[なでなで・ASMR音ジェネレーター](../generator/) は、撫で音やオイルなどの音をブラウザの中で合成するツールです。**World Nadenade 用の音色素材を、ボタン1つで書き出せます。** 書き出した音は、個人・商用を問わずワールドに組み込めます（[ジェネレーターの利用規約](../generator/terms.html)）。

### 書き出したものの中身

`WorldNadenade_<名前>.zip` に、次のファイルが入っています。

| ファイル | 内容 |
|---|---|
| `<名前>_palm.wav` | 手のひらの音（Palm Clip）。継ぎ目のないループ |
| `<名前>_back.wav` | 手の甲の音（Back Clip）。初期設定では、手のひらの音のピッチを少し上げたもの |
| `<名前>_settings.json` | この音を作った設定。ジェネレーターの「設定を読み込む」で再現できます |
| `README.txt` | 取り込み方のメモ |

音はモノラル・48kHz・16bit で、どれもピーク -3dBFS にそろえてあります。触れる・離れるときの音量の変化はギミック側が手の速さで付けるので、音源は速さ一定の連続音になっています。

### 取り込み方

1. wav を Unity の Assets に入れます。
2. インポート設定を目安に合わせます：**Force To Mono オン / Load Type: Decompress On Load / Compression Format: Vorbis**。
3. `<名前>_palm` を選んで、**Tools > Silent Comfort > World Nadenade > Add Sound Preset** を実行します。
4. できた音色の **Back Clip** に `<名前>_back` を入れ、**Display Name** を直します。
5. **Check Presets** で確かめます。
6. ほかの音色と並べて聴き、音量の差は音色の **Gain** でそろえます（[音色（Presets）](presets.html)）。

## 追加音源パックを作る

World Nadenade 用の音色を作り、**追加音源パックとして配布・販売できます**（事前の連絡は不要です）。パックは本体（v1.0.0 以降）が入ったプロジェクトで使うもので、パック単体では動きません。v1.x の間は、NadeSoundPreset の項目名・`NadeSoundPreset_Base.prefab`・Base の初期値を変えないようにし、互換性が変わる変更は事前にお知らせします（[利用規約](terms.html)の別紙B）。商品ページには、本体が必要であることと、本体の配布ページへのリンクを載せてください。

### 入れてよいもの・入れてはいけないもの

| 入れてよいもの | 入れてはいけないもの |
|---|---|
| 自分で作った（または権利を持つ）AudioClip | 本体のスクリプトと UdonSharp Program Asset |
| `NadeSoundPreset_Base.prefab` の Prefab Variant | `NadeSoundPreset_Base.prefab` そのもの |
| 説明書・利用規約・サンプルシーン | 本体の Prefab・基本音源・その他のファイル |

unitypackage を書き出すときは **Include dependencies のチェックを外し**、自分のフォルダだけが入っていることを確かめてください。本体のファイルが入ると、受け取った人の本体が古い版で上書きされることがあります。

### フォルダと名前

```
Assets/
  <あなたの屋号>/WorldNadenade_<パック名>/
    Presets/    … 音色の Prefab Variant
    Sounds/     … AudioClip
    README.txt
```

- `SilentComfort/` の下には置かないでください（本体の更新に巻き込まれる恐れがあり、公式の商品と誤解されるため）。
- **Preset Id は `<屋号>_<音色名>`** にしてください（例：`marusound_rain`）。複数の制作者の音色が同じワールドに入るためです。`silentcomfort_` は使わず、公開後は変えないでください。
- Prefab と AudioClip の名前にも、屋号かパック名を頭に付けると見分けやすくなります。

### 作り方

1. **Packages > World Nadenade > Presets** の `NadeSoundPreset_Base.prefab` を右クリック → **Create > Prefab Variant** で作り、自分の `Presets/` フォルダ（Assets の下）へ移します。
2. Variant の Preset Id・Display Name・Palm Clip（・Back Clip）を設定します。鳴り方を固定したい値は、Variant 側で明示的に上書きしておきます（インスペクターで太字になります）。
3. [Sound Tuner](presets.html) で鳴らしながら調整します。
4. 本体だけが入った新しいプロジェクトにパックを入れ、Presets の下に置いて、**Check Presets**・試し聴き・なでたときの音を確かめます。できれば Android 向けにもビルドして、音質と負荷を確かめます。

### 購入者向けの説明書に書いてほしいこと

- 必要なもの：World Nadenade 本体（v1.0.0 以降など、対応バージョン）と、その配布ページへのリンク（[BOOTH](https://silent-comfort.booth.pm/items/9171198)）
- 導入方法：unitypackage を読み込み、`Presets/` の中の Prefab を **WorldNadenade > Presets** の下にドラッグする
- 並び順：Presets の上から順に音色ボタンに並び、先頭が入室時の音色になること
- 購入者に、少なくとも「VRChat のワールドに組み込んで訪問者に聞かせること」「その様子が配信・動画に入ること」を許可していること
- 問い合わせ先：音源の内容はパックの制作者へ、本体の動作は Silent Comfort へ
