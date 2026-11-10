# せどり一括検索（sedori-multi-search）

店舗せどりの現場で、1回の入力で複数サイトをまとめて検索するためのWebツール。
`index.html` 1ファイルだけで動く（サーバー・ライブラリ不要）。

## 機能

| 機能 | 内容 |
|------|------|
| 一括検索 | メルカリ / ヤフオク / Yahoo!フリマ / ラクマ / オークファン |
| 売り切れ検索 | チェックONで「売り切れ・落札済み」の相場を表示（Yahoo!フリマのみURL非対応→サイト上で絞込） |
| 音声入力 | 🎤ボタン（Web Speech API）。非対応ブラウザはキーボードのマイクで代用 |
| メーカー簡単入力 | カテゴリ別ブランドボタン。タップ＝追加、長押し＝置き換え。「編集」で追加・削除 |
| 検索履歴 | 直近30件。タップで再検索 |
| サイトON/OFF | 使わないサイトを非表示 |

設定・履歴はブラウザ（localStorage）に保存される。

## iPhoneでの使い方

音声入力ボタンは **https で開いたときだけ** 動く。おすすめは GitHub Pages：

1. GitHubで新規リポジトリ（例：`sedori-multi-search`、Public）を作成
2. `index.html` をアップロード
3. Settings → Pages → Branch: `main` / `(root)` → Save
4. 数分後 `https://<ユーザー名>.github.io/sedori-multi-search/` をSafariで開く
5. 共有ボタン →「ホーム画面に追加」でアプリのように起動できる

## 注意

- iPhone Safariは「まとめて開く」で1タブしか開かないことがある。その場合は各サイトのボタンを順にタップ（開いたサイトは枠が付く）
- PCのChromeで「まとめて開く」を使うには、このページのポップアップを許可する
- オークファンは検索語をEUC-JPの16進数でURLに埋め込む仕様（`q-~a5eda5f3...`）。変換できない文字（絵文字等）は除外される

## 検索URL（2026-11-09 動作確認）

| サイト | 販売中 | 売り切れ |
|--------|--------|---------|
| メルカリ | `jp.mercari.com/search?keyword=…` | `&status=sold_out` |
| ヤフオク | `auctions.yahoo.co.jp/search/search?p=…` | `closedsearch/closedsearch?p=…` |
| Yahoo!フリマ | `paypayfleamarket.yahoo.co.jp/search/…` | （URL指定不可） |
| ラクマ | `fril.jp/s?query=…` | `&transaction=soldout` |
| オークファン | `aucfan.com/search1/q-~<EUC-JP hex>/` | 同左（過去相場） |
