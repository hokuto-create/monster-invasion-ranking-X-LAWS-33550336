# X-LAWS 個人スコアランキング — 作業メモ

- `data.json` の `entries` に `{"date","player","score"}` を1行1プレイヤーで追記する
- **集計時刻は記録しない。** `timestamps` は空のまま（`{}`）にしておき、日次データ追加時にも日付を追加しない
- 途中参加のメンバーは `joined` に `"名前": "参加開始日"` を追加する（参加チェックでそれ以前の日は「−」扱い）

## Git

- 日次データの追加は、検証で問題がなければ PR を作成して main にマージまで行う（都度の依頼は不要）
  - マージ前に PR の mergeable 状態を確認する
  - スコアの疑わしい値など、ユーザー確認が必要な点がある場合はマージせずに確認を取る

## サイトの構成

- 開くとホーム（入口メニュー）を表示し、各画面へ進む。画面は URL の `#ranking` / `#graph` / `#check` / `#expedition` / `#airship` で直接開ける
- メニュー項目を増やすときは `index.html` の `MENU` に追加し、`SECTIONS`（画面名 → 表示する要素）と `VIEWS` にも登録する
- **`index.html` を変更したら `APP_VERSION` も必ず更新する**（形式: `'YYYYMMDD-連番'`）

## クラン遠征（`expedition.json`、金・土・日）

- `battles` に1日1件 `{"date","opponent","result","lanes","note"}` を追加する
  - `result`: `"win"` / `"lose"` / `"draw"`。分からなければ `""`
  - `lanes`: `{"左": [...], "中": [...], "右": [...]}`。各レーンは画面の並び順のまま1人1行
  - 1行: `{"player","dmg","dmgPct","time","timePct","taken","takenPct","heal","healPct"}`
    - `dmg`＝火力、`time`＝生存時間（秒）、`taken`＝被ダメージ、`heal`＝回復量。値は数値（`3.62M` → `3620000`）、`〜Pct` は画面の % をそのまま
- 記録するのは X－LAWS 側のみ。値はスクショの表示どおりに転記し、丸めや補正はしない

## クラン飛空艇（`airship.json`、毎日）

- `days` に1日1件 `{"date","captain","image","note"}` を追加する
  - `captain`: 船長。名前はランキング（`data.json`）の表記に揃える（例: 画面の「ほくと」→ `ूほくとू`）
  - `image`: 報酬欄のスクショを切り抜いたもの。`airship/YYYY-MM-DD.jpg` に保存する（幅 300px 前後の JPEG に縮小）
