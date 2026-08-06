# オープンキャンパス WebAR「ARキャラクター図鑑」

QRコードを1つ読み取るだけで起動する、アプリ不要のWebARコンテンツです。
3枚のマーカーカードを並べて置くと、それぞれの上に別のキャラクターが浮かび上がります。

| マーカー | キャラクター | 動き |
|---|---|---|
| ① Hiro（丸っこい模様） | きつね（動物） | 歩くアニメーション + 上下にふわふわ |
| ② Kanji（漢字模様） | 歩行ロボット（おもしろキャラ） | 歩くアニメーション + ゆっくり回転 |
| ③ LetterA（Aの模様） | ドラゴン | 回転 + 上下にふわふわ |

---

## 1. フォルダ構成

```
ar-demo/
├── index.html          ← これがWebARページ本体
├── models/
│   ├── fox.glb          きつね（動物）
│   ├── hero.glb          歩行ロボット（おもしろキャラ）
│   └── dragon.glb       ドラゴン
└── markers/
    ├── hiro_print.png    印刷用マーカー①
    ├── kanji_print.png   印刷用マーカー②
    ├── letterA_print.png 印刷用マーカー③
    └── letterA.patt      マーカー③の認識データ（index.htmlが参照します）
```

このフォルダをまるごとサーバーに置くだけで動きます。

---

## 2. 公開方法（GitHub Pagesが簡単・無料）

1. GitHubに新しいリポジトリを作成
2. `ar-demo` フォルダの中身（index.html, models, markers）をそのままアップロード
3. リポジトリの Settings → Pages → Branch を `main` に設定して保存
4. 数分後、`https://ユーザー名.github.io/リポジトリ名/` でアクセス可能になります
5. **このURLをQRコードに変換**（QRのススメ、qr-code-generator.com など任意のツールでOK）

※ カメラ機能はブラウザの仕様上、`https`（またはlocalhost）でないと起動しません。GitHub Pagesは自動でhttpsになるので安心です。

---

## 3. マーカーカードの印刷・設置

- `markers/hiro_print.png`, `kanji_print.png`, `letterA_print.png` を使用します。
- **推奨サイズ:** 1辺 8〜12cm 程度（大きいほど認識しやすく、離れた位置からも反応します）
- マーカーの周りに **白い余白を必ず残す**（マーカーの黒枠が切れると認識しません）
- 3枚を **重ならない程度に離して並べる**（近すぎると同時に映したとき干渉することがあります）
- 光の反射・影を防ぐため、ラミネート加工したうえで**マット（半光沢）**な素材にするのがおすすめ
- 会場の照明が暗いと認識精度が落ちるため、可能であれば手元灯や自然光がある場所に設置

---

## 4. 当日の案内表示イメージ

QRコードの下に「①②③のカードにカメラを向けてね」のような案内があると親切です。
QRコードは1つだけ、掲示物の目立つ位置に配置してください。

---

## 5. キャラクター・マーカーの差し替え方

- **3Dモデルを変える場合:** `models/` の中の `fox.glb` / `hero.glb` / `dragon.glb` を、同じファイル名で別の `.glb` ファイルに置き換えるだけでOKです（`index.html`の変更は不要）。
- **アニメーションの調整:** `index.html` 内の `animation-mixer` や `animation` の数値（`dur`（速さ）、`scale`（大きさ）など）を変更すると動きの雰囲気を調整できます。
- **マーカーを変える場合:** 独自デザインの画像で試したい場合は、AR.jsの「Marker Training」で画像から `.patt` ファイルを生成し、`markers/` に置き換えます。

---

## 6. 使用モデルのクレジット（自由に使えるライセンスのものを採用）

会場配布物・パンフレット等への記載は不要ですが、Webページなどに載せる場合は下記を明記すると丁寧です。

- **Fox**（きつね）— CC0 / CC-BY 4.0, Khronos Group glTF-Sample-Assets
  (rig: [@tomkranis](https://sketchfab.com/tomkranis), animation: Character Animation All-Stars, model: [PixelMannen](https://opengameart.org/content/fox-and-shiba))
- **CesiumMan**（歩行ロボット役として採用）— CC-BY 4.0, © Cesium / Analytical Graphics, Inc.
- **DragonAttenuation**（ドラゴン）— CC0 1.0, Stanford Graphics Library / Khronos Group glTF-Sample-Assets

いずれも [Khronos Group glTF-Sample-Assets](https://github.com/KhronosGroup/glTF-Sample-Assets) より取得した、商用・非商用問わず自由に利用できるモデルです。

---

## 7. トラブルシューティング

| 症状 | 対処 |
|---|---|
| カメラが起動しない | URLがhttpsになっているか確認。ブラウザのカメラ許可がブロックされていないか確認 |
| マーカーを映してもキャラが出ない | マーカーが画面の枠内に大きく・正面から・水平に見えるようにする／照明を明るくする |
| キャラの表示位置がズレる | マーカーの印刷サイズが小さすぎる可能性。8cm角以上を推奨 |
| 動作が重い・カクつく | ドラゴンモデル（約6MB）の読み込みに時間がかかる場合あり。会場Wi-Fiが弱い場合は事前にモバイル通信で1回開いてキャッシュさせておくと安心 |
| iPhoneで映像が縦に伸びる/おかしい | Safariの「ページの拡大／縮小」をリセット、または一度ページを再読み込み |

当日は本番前に必ず実機（できれば複数台・iOS/Android両方）で最終確認をしてください。
