# Fair Trade Compass — 自動更新ガイド

## サイト概要
- **サイト名**: Fair Trade Compass / フェアトレード羅針盤
- **テーマ**: フェアトレード（生産者、認証、商品、動向）の最新情報を日英バイリンガルで毎日発信
- **URL**: https://musclelove-777.github.io/fair-trade-compass/
- **言語**: 日本語 (/ja/) と 英語 (/en/) の **独立記事**（翻訳ペアではない、それぞれ個別に書く）
- **ブランド**: 中立・学術寄り・エシカル。MuscleLoveブランディングは**出さない**

## 重要: 多言語方針
- JAとENは**独立した記事**を書く。同じニュースでも切り口・強調点を変えてOK
- 1日あたり **JA新記事2本 + EN新記事2本 = 計4本**
- 両言語でhreflangを相互にリンクする（後述のテンプレ参照）
- 同じURLスラグを使う必要はなし（例: JA=`cocoa-minimum-price-2026` / EN=`cocoa-minimum-price-hike` でOK）

## カテゴリー
1. **生産者ストーリー / Producer Stories** — コーヒー、カカオ、コットン、紅茶、スパイス等の生産者・農家・協同組合
2. **認証基準 / Certification** — Fairtrade International、WFTO、Rainforest Alliance、Fair Trade USA等の認証解説
3. **商品情報 / Products** — チョコレート、コーヒー、コットン、ワイン等のフェアトレード商品レビュー・ランキング
4. **動向・政策 / News & Policy** — 最低価格改定、EU規制（CSDDD等）、戦略アップデート、業界ニュース
5. **コラム / Columns** — エシカル消費の考え方、歴史、批判的視点も含む解説

## 記事生成ルール

### ネタ収集（WebSearch対象クエリ例）
**JA向け**
- 「フェアトレード ニュース 2026」
- 「Fairtrade Japan 新商品」
- 「エシカル消費 日本」
- 「フェアトレード認証 コーヒー/カカオ/コットン」

**EN向け**
- "Fairtrade International news"
- "WFTO World Fair Trade Organization"
- "Fair Trade USA certification news"
- "ethical cocoa coffee supply chain"

複数ソースを確認し、公式発表（Fairtrade.net、WFTO.com等）を優先。

### 文字数・スタイル
- **JA**: 1本あたり 800〜1,500文字、見出し3〜5個
- **EN**: 1本あたり 500〜900 words、見出し3〜5個
- トーン: 学術寄りだが読みやすい。断定しすぎず、一次情報への言及を明記
- 推測を書く場合は「〜とみられる / likely to 〜」等で明示

### ファイル命名規則
- JA記事: `ja/articles/YYYY-MM-DD-japanese-slug.html`
- EN記事: `en/articles/YYYY-MM-DD-english-slug.html`
- slugは英小文字ハイフン区切り（例: `fairtrade-strategy-2026-2028`）

### Unsplash画像ルール
- **必須**: 全記事にヒーロー画像＋サムネイル画像
- **絶対禁止**: 特定の実在生産者の顔写真は使わない（肖像権・誤表現リスク）。農村風景、商品、コーヒー豆などの汎用イメージのみ
- フォーマット: `https://images.unsplash.com/photo-XXXXX?w=幅&h=高さ&fit=crop`
- サムネイル（ブログカード用）: `w=600&h=340`
- ヒーロー画像（記事ページ背景用）: `w=1800&h=900`
- OGP画像: `w=1200&h=630`
- 推奨検索キーワード: `coffee farm`, `cocoa pods`, `tea plantation`, `cotton field`, `farmer hands`, `african farmer`, `chocolate`, `fair trade market`, `harvest`, `sustainable agriculture`

### 記事HTMLテンプレート
`ja/articles/2026-04-23-fairtrade-strategy-2026-2028.html` を参考にコピー。以下が必須要素：
1. `<html lang="ja">` または `<html lang="en">`
2. title / description / keywords / canonical / hreflang（必ず対応他言語のパスを指定、なければ`x-default`のみでOK）
3. OGP（og:title, og:description, og:image, og:type=article, og:locale）
4. JSON-LD（Article schema）
5. 共通ヘッダー（ブランド＋ナビ＋lang-switch）
6. `<section class="article-hero">` に背景画像
7. `<article class="content">` に本文
8. `<div class="article-footer">` に参考ソース
9. 共通フッター

### index.html 更新
- `ja/index.html` の `<div class="blog-grid">` 内を**最新3件**に保つ（新記事追加で古いカードを押し出す）
- `en/index.html` も同様
- カード構造（サムネイル画像、カテゴリタグ、日付、タイトルリンク、excerpt）を維持

### sitemap.xml 更新
- `/sitemap.xml` に新記事URLを毎回追加（JA・EN両方）
- `<lastmod>` は記事の公開日（YYYY-MM-DD）
- `<changefreq>weekly</changefreq>`, `<priority>0.7</priority>` 程度で

### コミット＆push
```bash
git add -A
git commit -m "[auto] Add daily articles YYYY-MM-DD"
git push
```

## 毎日の更新フロー（リモートエージェント用）

```
1. git pull（最新を取得）
2. WebSearch でJA向けネタ2本、EN向けネタ2本を決める
   - 重複回避: ja/articles/ と en/articles/ の既存ファイル名を確認
3. Unsplash画像URLを各記事に1〜2枚（ヒーロー + サムネイル）
4. JA記事2本を ja/articles/YYYY-MM-DD-slug.html に保存
5. EN記事2本を en/articles/YYYY-MM-DD-slug.html に保存
6. ja/index.html の blog-grid を最新3件に更新
7. en/index.html の blog-grid を最新3件に更新
8. sitemap.xml に新URLを4件追加
9. git commit & push
```

## 関連公式ソース
- Fairtrade International: https://www.fairtrade.net/
- Fairtrade Japan: https://www.fairtrade.net/jp-jp.html
- WFTO: https://wfto.com/
- Fair Trade USA: https://www.fairtradecertified.org/
- FAO (国連食糧農業機関): https://www.fao.org/
- Rainforest Alliance: https://www.rainforest-alliance.org/

## NGリスト
- 特定企業の誹謗中傷
- 未確認情報の断定的記述
- 実在農家の顔写真（Unsplash含む）
- AdSense広告コード・大手SNS誘導（ブランディング理由）
- アフィリエイトリンク（初期は入れない、将来検討）

## ブランドトーン
- 中立・教育的・実用重視
- 「買う理由」を押し売りせず、「判断材料」を提供
- 数字と公式ソースで信頼感を作る
- 日本語は読みやすい論説調、英語はjournalism style（抑揚あり）
