---
title: 導入する
description: World Nadenade をワールドに入れて、動作を確かめるまでの手順です。
---

## 1. 必要なパッケージを入れる

World Nadenade の操作パネルは、日本語の表示に **tmp-fallback-fonts-jp** を使います。先にこちらを入れておきます。

1. VCC（VRChat Creator Companion）の **Settings > Packages** で、リポジトリ `https://vpm.narazaka.net/` を追加します。
2. プロジェクトの **Manage Project** から **tmp-fallback-fonts-jp** をインストールします。
3. Unity の **Project Settings > TextMesh Pro** で **TMP Essentials** をインポートします（インポート済みなら不要）。
4. tmp-fallback-fonts-jp の **Tools メニューから設定**を実行します。

> パネルの文字は、中身の無いフォント（Empty SDF）で作り、日本語は VRChat に内蔵のフォントで表示します。**文字に日本語フォントを直接指定しないでください。** そのフォントがワールドに含まれ、容量が増えます。

## 2. World Nadenade を入れる

> 入手方法（BOOTH・VCC）は公開時に追記します。
{: .note-draft}

## 3. ワールドに置く

1. **WorldNadenade** を Hierarchy の好きな場所に **1個だけ**置きます。
2. **NadeControlPanel** を、操作パネルを出したい場所（壁・手持ちメニューなど）に置きます。何枚でも置けます。
3. 置いた各 NadeControlPanel の **`Manager` 欄に WorldNadenade をドラッグ**します。
   - 設定し忘れたパネルには「未接続」と表示され、Console にも `[World Nadenade] 操作パネルの Manager が未設定です` と出ます。
4. 必要なら、タブレット（NadeTablet）も置きます（[操作パネルとタブレット](panel.html)）。

パネルとタブレットの色違い・大きさの変え方は、[操作パネルとタブレット](panel.html)にあります。

### 置くときの注意

- **WorldNadenade は1ワールドに1個だけ**にしてください。2個あると音が二重に鳴ります。
- **WorldNadenade のルートの Scale は 1 のまま**にしてください。頭の判定の大きさが Scale の影響を受けます。位置と回転は自由です。
- 操作パネルは、壁の表面から **2〜3cm 手前**に出してください。壁のコライダーに隠れると、レーザーが届きません。

## 4. 人数と同時発音数を合わせる

### Heads（頭の判定）

`Heads` の下の Head は、1人に1つ使います。ワールドの定員が Head の数より多いときは、`Heads` の直下で Head を複製（Ctrl+D）して足します。多すぎても負荷は増えません。

- 名前は自由で、配列への登録は要りません（起動時に直下の子を自動で集めます）。
- 数を減らすときは、無効にするのではなく削除してください。

### Voices（同時に鳴る数）

`Voices` の下の Voice 1つで、1つの手の音を鳴らします。**推奨は 6 個**です（自分なでの両手 2 ＋ 2人から両手でなでられる 4）。他人同士のなでなでは自分の端末では鳴らないので、数に入りません。

足りないときは、消えかけの音を置き換えるか、その接触だけ鳴らないだけで、エラーにはなりません。

## 5. なでる側の設定の同期（PlayerPreset）

WorldNadenade の子 `PlayerPreset` が、各プレイヤーが選んだ音色と手のひら・手の甲の設定を全員に同期します。シーンに置くのは1つだけで、入室した人の数だけ VRChat が自動で複製します。

- 送るのは設定を変えたときだけなので、通信量はごくわずかです。後から入室した人にも届きます。
- **VRC Enable Persistence** を `PlayerPreset` に付けると、次に同じワールドに入ったとき、前回選んだ音色と手のひら・手の甲の設定が戻ります（任意）。付けない場合は、毎回先頭の音色から始まります。

## 6. 推奨設定

| 対象 | 項目 | 推奨 |
|---|---|---|
| Voice の Palm・Back（AudioSource） | Spatial Blend | 1（3D） |
| | Gain（VRC Spatial Audio Source） | 24 |
| | Near / Far（VRC Spatial Audio Source） | 0.2 / 3（Near が 0 だと、手が少し離れただけで小さくなります） |
| AudioClip | Load Type | Decompress On Load |
| | Preload Audio Data | オン（最初になでたときの出だしの遅れを防ぎます） |
| NadeManager | Default Volume | 0.5（入室時の音量 50%） |

### NadeManager の主な項目

| 項目 | 内容 | 初期値 |
|---|---|---|
| Start Enabled | 入室時に「なで音を聞く」を ON にするか | オフ |
| Default Volume | 入室時の音量 | 0.5 |
| Default Self Pat | 入室時に「自分なで」を ON にするか | オフ |
| Use Hand Side | 手のひら / 手の甲の判別。オフにすると、パネルの手のひら・手の甲の設定も隠れます | オン |
| Sound Palm Blend | 音の位置。0 = 手首、1 = 手のひらの中心 | 0 |
| Head Radius / Head Center Offset | 頭の判定の大きさと位置（身長 1.6m 基準）。顎まで届くよう、少し下・前寄りにしてあります | 0.13 / (0, -0.02, -0.03) |
| Near Distance | この距離以内にいる人の頭だけを判定する | 2.5 |
| Force Language | 表示の言語を固定する（`ja` / `en`）。エディタで日本語の表示を確かめるとき用。公開時は空欄にする（[表示の言語](panel.html#language)） | 空欄 |
| Fallback Language | 表示言語に翻訳が無い人に使う言語 | en |
| Debug Mode | ON のときだけデバッグ表示パネルを出す | オフ |

音色ごとの値（音量の補正、速さと音量の対応など）は、[音色（Presets）](presets.html)にあります。

## 7. 動作を確かめる

> ClientSim ではアバターの手のコンタクトが無いため、**なで音は鳴りません**。VR の Build & Test か、テスト用のアップロードで確認してください。
>
> また、ClientSim では**パネルが英語で表示されます**（ClientSim が表示言語を英語として扱うため）。日本語で確かめたいときは、NadeManager の `Force Language` に `ja` と入れます（[表示の言語](panel.html#language)）。

### 一人で確かめる（VR が必要）

1. NadeManager の `Debug Mode` を ON にし、デバッグ表示パネルを見やすい場所に置きます。
2. VR で Build & Test を実行し、操作パネルの「なで音を聞く」と「自分なで」を ON にします。
3. 自分の頭をなでて、次を確かめます。

- 手を速く動かすほど音が大きくなる
- 手を裏返すと音が切り替わる（手の甲の音がある音色のとき）
- 音が手の位置から聞こえる
- 音色ボタンを押すと試し聴きが鳴り、なでたときの音も変わる

### 二人以上で確かめる

一人では確かめられない「相手の音色で鳴るか」「他人同士のなでなでが鳴らないか」は、最後に誰かと一度確かめれば十分です。

1. 両方で「なで音を聞く」を ON にし、片方がもう片方の頭をなでる → 両方の端末で鳴る
2. それぞれ別の音色を選んでなで合う → なでた人の音色で、両方の端末に同じ音が鳴る
3. 後から入室した人をなでる → 選んだ音色で鳴る

起動時の Console に `[World Nadenade] Presets 3 / Heads 16 / Voices 6` のように数が出るので、想定どおりかも見ておきます。

## 8. 公開する前に

- [ ] NadeManager の `Debug Mode` をオフにする（デバッグ表示パネルは自動で隠れるので、削除しなくて構いません）
- [ ] NadeManager の `Force Language` を空欄にする（入れたままだと、全員の表示がその言語に固定されます）
- [ ] **Tools > Silent Comfort > World Nadenade > Check Presets** で警告が出ない
- [ ] 自分で足した音源が、ワールドで使ってよいものか確かめた（[音源を用意する](soundpack.html)）
- [ ] Android 向けにもビルドし、Quest 単機で日本語の表示と負荷を確かめた
