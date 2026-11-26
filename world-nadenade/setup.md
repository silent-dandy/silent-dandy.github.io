---
title: 導入する
description: World Nadenade をワールドに入れて、動作を確かめるまでの手順です。
---

## 1. World Nadenade を入れる

次のどちらかで入れます。中身は同じで、どちらで入れても以後の更新は VCC / ALCOM の **Manage Project** から行えます。

### A. BOOTH の自動インストーラーで入れる

1. [BOOTH の配布ページ](https://silent-comfort.booth.pm/items/9171198)からダウンロードした zip を解凍します（無料版・支援版とも中身は同じです）。
2. ワールドのプロジェクトを Unity で開き、中の unitypackage をインポートします（Project ウィンドウへのドラッグ＆ドロップでも可）。
3. VPM リポジトリの追加と、World Nadenade のインストールが自動で行われます。日本語表示用の **tmp-fallback-fonts-jp** も一緒に入ります。

### B. VCC / ALCOM にリポジトリを追加して入れる

1. VCC / ALCOM の **Settings > Packages > Add Repository** で、次の URL を追加します。[リポジトリのページ](https://silent-dandy.github.io/vpm/)の **Add to VCC** ボタンからも追加できます。
   ```
   https://silent-dandy.github.io/vpm/index.json
   ```
2. 同じ画面で、フォントのパッケージ（tmp-fallback-fonts-jp）のリポジトリ `https://vpm.narazaka.net/index.json` も追加します。
3. プロジェクトの **Manage Project** から **World Nadenade** を追加します。tmp-fallback-fonts-jp は依存パッケージとして一緒に入ります。

## 2. 初回の準備（日本語の表示）

1. **Window > TextMeshPro > Import TMP Essential Resources** で TMP Essentials を入れます（入れてあれば不要です）。
2. tmp-fallback-fonts-jp の **Tools メニューにある設定**を実行します。TMP の初期フォントが Empty SDF になります。

> パネルの文字は、中身の無いフォント（Empty SDF）で作り、日本語は VRChat に内蔵のフォントで表示します。**文字に日本語フォントを直接指定しないでください。** そのフォントがワールドに含まれ、容量が増えます。

## 3. ワールドに置く

Prefab は Project ウィンドウの **Packages > World Nadenade** の中にあります。次の3つを置けば使えます。

1. **本体**：`WorldNadenade.prefab` を Hierarchy の好きな場所に **1個だけ**置きます。**パネルやタブレットより先に置いてください。**
2. **壁の操作パネル**：`Prefabs/ControlPanel` から選んで、壁など操作パネルを出したい場所に置き、表示面を部屋の側に向けます（例：`NadeControlPanel_Smoke_TabletNote`）。何枚でも置けます。
   - 置くと、NadeControlPanel の `Manager` 欄に WorldNadenade が**自動で入ります**（[パネルの接続](#connect)）。
3. **タブレット**（任意）：`Prefabs/Tablet` から選んで置きます（例：`NadeTablet_Smoke_Gray_CradleWoodLight`）。置き台つきは、置き台の原点（背板の裏面）を壁の表面に合わせ、床から 1.0〜1.2 m 程度の高さにします。
   - タブレットの `Manager` 欄にも、WorldNadenade が自動で入ります。

色違い・大きさの変え方、タブレットを置かない場合のパネルの選び方は、[操作パネルとタブレット](panel.html)にあります。

> **パッケージの中の Prefab は直接編集しないでください。** パッケージを更新すると元に戻ります。シーンに置いたものを変更してください。

### パネルの接続 {#connect}

操作パネル・タブレット・デバッグ表示パネル・NadeSwitch は、`Manager` 欄に WorldNadenade が入っていると使えます。v1.1.0 から、この欄は自動で埋まります。

- **置くと自動で入る**：シーンに WorldNadenade が1個あれば、パネルを置いた（ドラッグ＆ドロップ・複製・貼り付け）ときに、空の `Manager` 欄に入ります。Console に `[World Nadenade] 1 個のパネルを「WorldNadenade」に接続しました` と出ます。
- **WorldNadenade を後から置いても入る**：先に置いてあったパネルが、まとめて接続されます。
- **空になったときも入り直す**：パッケージの更新などで `Manager` 欄が空になったときも、シーンを開いたときなどに自動で接続し直します。シーンを保存すると残ります。
- **入っている欄は書き換えません。** すべて接続済みなら何もしないので、シーンを開いても「変更あり」にはなりません。

自動で入らなかったときや、まとめて確かめたいときは、次の方法もあります。

| 方法 | 内容 |
|---|---|
| パネルのインスペクター | `Manager` 欄が空のときに警告と **シーンの WorldNadenade に接続** ボタンが出ます |
| WorldNadenade のインスペクター | パネルの接続の状況（接続済み / 未接続）と、**未接続のパネルをこの WorldNadenade に接続** ボタンが出ます |
| **Tools > Silent Comfort > World Nadenade > Connect Panels** | シーンの未接続のパネルを、すべて接続します |
| ビルドの前の確認 | Build & Test・アップロードの前に未接続のパネルがあると、「接続して続ける / 中止する / 接続せずに続ける」を選べます |
| 手で指定する | 今までどおり、`Manager` 欄に WorldNadenade をドラッグしても構いません |

- 設定し忘れたパネルには、ワールドで「未接続」と表示され、Console にも `[World Nadenade] 操作パネルの Manager が未設定です` と出ます。
- 自動接続をやめたいときは、**Tools > Silent Comfort > World Nadenade > Auto Connect Panels** のチェックを外します（この PC の設定として保存されます）。オンの間は、`Manager` 欄をわざと空にしても入り直します。
- 非表示（非アクティブ）の WorldNadenade には接続しません。

### 置くときの注意

- **WorldNadenade は1ワールドに1個だけ**にしてください。2個あると音が二重に鳴ります。2個目を置くと「今置いた方を削除 / そのままにする」のダイアログが出ます。2個以上あるあいだは、パネルの自動接続は行わず、インスペクターにエラーが出ます。アップロードの前にも、中止するか尋ねます。
- **WorldNadenade のルートの Scale は 1 のまま**にしてください。頭の判定の大きさが Scale の影響を受けます。位置と回転は自由です。
- **WorldNadenade を非アクティブにしないでください。** 非アクティブの間に入室した人が判定の対象から外れます。なで音のオン・オフは、訪れた人がそれぞれパネルやタブレットで行います。
- 操作パネルは、壁の表面から **2〜3cm 手前**に出してください。壁のコライダーに隠れると、レーザーが届きません。

## 4. 人数と同時発音数を合わせる

### Heads（頭の判定）

`Heads` の下の Head は、1人に1つ使います。**32 人分入っています。**ワールドの定員が 32 人より多いときは、シーンに置いた WorldNadenade の `Heads` の直下で Head を複製（Ctrl+D）して足します。多すぎても負荷は増えません。

- 名前は自由で、配列への登録は要りません（起動時に直下の子を自動で集めます）。
- 数を減らすときは、無効にするのではなく削除してください。

### Voices（同時に鳴る数）

`Voices` の下の Voice 1つで、1つの手の音を鳴らします。**6 個入っていて、これが推奨の数**です（自分なでの両手 2 ＋ 2人から両手でなでられる 4）。他人同士のなでなでは自分の端末では鳴らないので、数に入りません。

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

起動時の Console に `[World Nadenade] Presets 4 / Heads 32 / Voices 6` のように数が出るので、想定どおりかも見ておきます。

## 8. 公開する前に

- [ ] NadeManager の `Debug Mode` をオフにする（デバッグ表示パネルは自動で隠れるので、削除しなくて構いません）
- [ ] NadeManager の `Force Language` を空欄にする（入れたままだと、全員の表示がその言語に固定されます）
- [ ] **Tools > Silent Comfort > World Nadenade > Check Presets** で警告が出ない
- [ ] WorldNadenade のインスペクターで、パネルが「未接続 0」になっている（ビルドの前の確認でダイアログが出ない）
- [ ] 自分で足した音源が、ワールドで使ってよいものか確かめた（[音源を用意する](soundpack.html)）
- [ ] Android 向けにもビルドし、Quest 単機で日本語の表示と負荷を確かめた

## 9. 更新する {#update}

VCC / ALCOM の **Manage Project** で、World Nadenade の新しいバージョンを選びます。BOOTH から入れた場合も同じです。

- シーンに置いた Prefab の変更（Manager の指定、追加した音色など）は、更新しても残ります。
- 万一 `Manager` 欄が空になっても、シーンを開いたときに自動で接続し直します（v1.1.0 以降。[パネルの接続](#connect)）。
- 各版の変更点は[はじめに](index.html)の更新履歴にあります。
- 変更内容は BOOTH の配布ページと、このマニュアルでお知らせします。
