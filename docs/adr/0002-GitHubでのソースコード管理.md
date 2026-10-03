# ADR-002: ソースコード管理に GitHub を採用し、リポジトリ名を dontokoi-pochitto-radio-app とする

- **ステータス**: 採用
- **背景**: 変更履歴を残し、英単語アプリ・集中トマトと同じ運用で管理したい。
- **決定**: GitHub にリポジトリ `tekkahosomaki/dontokoi-pochitto-radio-app` を作成する(初期ファイルなしの空のリポジトリ)。ローカルの作業フォルダは `C:\Users\<ユーザー名>\Documents\github\20261003_dontokoi-pochitto-radio-app\` とし、このフォルダ自体をリポジトリのルートにする。アプリの表示名は「ポチッとラジオ」。
- **検討した代替案**: リポジトリ名の候補として `dontokoi-web-radio-app`、`dontokoi-net-radio-app`、`dontokoi-radio-app`、`dontokoi-radio-tuner-app` も挙がった。表示名の候補には「どんとこいラジオ」「ながらラジオ」もあった。ボタンを押すだけで聴ける手軽さが伝わる「ポチッとラジオ」を表示名に選び、リポジトリ名もそれに合わせて `pochitto` を入れた。
- **結果・影響**: GitHub 上のリポジトリは空の状態で作ったため、ローカルの最初のコミットがそのまま履歴の始まりになる。
