# ADR-005: アーティファクトをやめて GitHub Pages で公開する

- **ステータス**: 採用([ADR-001](0001-HTMLファイル1つで動くブラウザアプリ.md) のうち「アーティファクトで公開する」部分を置き換える)
- **背景**: 最初は Claude のアーティファクトで公開した(`https://claude.ai/artifact/GQggZrmxbhPJrZAGiwKs7z`)。ところが Chrome で開くと全局が再生できなかった。Console には ``Loading media from '<URL>' violates the following Content Security Policy directive: "media-src 'self' data: blob:"`` と出ており、アーティファクトのページはページの外にある音声を読み込めない決まりになっていた。アーティファクト側の設定で許可する方法はない。一方、同じ HTML をダブルクリックで開くと全局が再生できた。
- **決定**: GitHub Pages で公開する。公開 URL は `https://tekkahosomaki.github.io/dontokoi-pochitto-radio-app/apps/pochitto-radio.html`。無料プランで Pages を使うためにリポジトリを公開(Public)にした。公開の前に、コミット履歴の作成者を「どんと来い！ガジェットラボ」と GitHub の匿名アドレス(`…@users.noreply.github.com`)に書き換え、資料からローカルのユーザー名を外した(履歴を書き換えて強制 push した)。
- **検討した代替案**: HTML ファイルを配ってダブルクリックで開いてもらう案(全局が聴けるが、渡す手間がかかり、スマホで開きにくいため、公開の主な方法にはしない。ダブルクリックでも動くことは引き続き守る)。リポジトリを非公開のまま有料プランで Pages を使う案(費用がかかるため不採用)。
- **結果・影響**: URL を開くだけで PC でもスマホでも聴ける。2026-10-03 に公開ページで SomaFM 以外の19局が再生できることを確認した(Intergalactic FM は鳴り始めるまで4秒ほどかかる)。SomaFM は参照元が `github.io` だとアクセスを断るため、公開ページでは SomaFM の4局は流れない見込み(Claude の内蔵ブラウザは SomaFM に断られるため、ふつうの Chrome で確認する)。リポジトリが公開になったため、ソースと資料、コミット履歴は誰でも見られる。今後のコミットも匿名の作成者で行う(git のグローバル設定を変更済み)。
