# Words for Soul プロジェクト概要(セッションが変わっても最初に読むファイル)
最終更新: 2026-09-06。方針・体制に変更があった場合は、このファイルも都度更新すること。

## このファイルの目的
Claude(Cowork)は会話が長くなると内容が要約(圧縮)されることがあり、要約の粒度によっては細かい経緯が
失われる。実際に本セッション中、以前作成したサイトアイコンの経緯が一時的に思い出せなくなったことが
あった。次にセッションが変わった際、この1ファイルを読めば体制・確立した方法・現在地がすぐ分かるように
しておく。

## 体制・役割分担
- Claude(Cowork): 戦略検討、記事執筆、Browser Claude/ChatGPTへの指示文の作成、進捗ログ内容の起草、
  GitHubのraw取得による独立検証を担当。ログイン情報を要する操作(WordPress管理画面、Google Search
  Console、GitHubへのコミット)は直接実行できないため、指示文を作成してAndo様に中継してもらう。
- Browser Claude: Ando様が既にログイン済みの実ブラウザ上で動く、別セッションのClaude。WordPress管理
  画面での実装・GSCの確認・GitHubへのコミットなど、認証を伴う操作を実行する。Cowork側の会話内容を
  一切記憶していないため、依頼する指示文は毎回自己完結させる必要がある。
- ChatGPT: ファクトチェック・SEOキーワード分析・相互レビュー(独立検証)を担当。特に、Browser Claudeが
  設定した内容(meta description、構造化データ等)を、自身のブラウジング機能で別経路から再検証する
  役割を担う。
- 本人(Ando様): 最終承認、および3者間のテキストのコピー&ペーストによる中継。
作業の実行はClaude(Browser Claude経由)に一本化し、同じ記事・設定を複数のAIが同時に触らないこと。
公開・大幅な変更は必ず本人が最終承認する。詳細は`ai_collaboration_workflow.md`を参照。

## 確立した検証方法・教訓
- 外部からページを取得してAIが要約する方式(Claude側のWebFetchツールなど)は、同一ページを短時間で
  再取得しただけで結果が食い違うことが複数回確認されている(WebFetch自体に15分間のキャッシュがある
  ことも判明済み)。この方式は一次情報として信頼しない。
- 信頼できる一次情報として扱うのは次の2つ。(1)Browser Claudeによる、WordPress管理画面のコード
  エディタでの生データ検索、またはページソース/DOMの直接確認。(2)ChatGPTによる、公開ページのDOMから
  の属性値の機械的な抽出。
- GitHub上のファイル内容を確認する際は、Claude側のWebFetchではなく、`curl -s -H "Cache-Control:
  no-cache" "https://raw.githubusercontent.com/<owner>/<repo>/main/<file>?nocache=$(date +%s)"`
  のようにキャッシュを回避したcurl直接取得を使う。words-for-soul.com本体(サイトドメイン)は、この
  サンドボックスの通信制限で直接curlできないため、そちらはWebFetchを使うしかないが、結果は単発では
  鵜呑みにせず、疑わしい場合は再取得や別経路(Browser Claude/ChatGPT)での確認を優先する。
- 公開ページへの変更(meta description、構造化データ、サイトアイコン等)は、Browser Claudeの確認に
  加えて、可能な限りChatGPTにも独立に再検証してもらう(2経路が一致すれば確度が高いと判断する)。
- 長文のテキストをBrowser Claude/ChatGPTに渡す際、コピー&ペーストの途中で文章が切れる事故が実際に
  複数回発生している。長い文言は1件ずつ渡す、貼り付け後に文字数を確認してもらう、といった対策を
  徹底する。

## 進捗ログ(PROGRESS.md、このリポジトリ)の運用ルール
- 見出しは`## YYYY-MM-DD`。同じ日に複数回追記する場合は`## YYYY-MM-DD 追記N(概要)`として、Nを
  1つずつ増やす。
- 新しいブロックは、ファイル冒頭の説明文のすぐ下、既存の一番上のブロックの直前に追加する(既存内容は
  削除・書き換えしない、上に積み増していく形)。
- 箇条書きは`［ラベル］内容`の形式(例:`［確認完了］`「経緯」「留保点」「結論」「独立検証・完了」等)
  で、既存のログで使われているラベルの語感に合わせる。
- コミットメッセージは既定のまま(「Update PROGRESS.md」)でよく、mainブランチに直接コミットする
  運用としている。
- コミット後は、Browser Claudeによるプレビュー確認に加えて、Claude(Cowork)側でも上記のcurl直接
  取得により独立に内容を確認する。

## サイトの基本情報(2026-09-06時点)
- 対象記事: 投稿15(ハブ、`hokusai-mount-fuji-koshu-wine-journey`)、投稿41(`hokusai-thirty-
  six-views-fuji-guide`)、投稿44(`dazai-fugaku-hyakkei-misaka-pass`)、投稿46(`koshu-wine-
  yamanashi-beginners-guide`)、投稿48(`kawaguchiko-fuji-view-hotel-guide`)。
- カテゴリー階層: 日本を旅する(親、投稿15はここに直接分類)→ 美術・浮世絵(投稿41)/ 文学(投稿44)/
  食・ワイン(投稿46)/ 宿・滞在(投稿48)。
- 著者ペルソナ: 「響」。詳細は`persona_style_guide.md`。
- URL構造は`/ja/%postname%/`。permalinkに`/ja/`プレフィックスあり。

## 2026-09-06時点で完了している項目
- 内部リンクの`/ja/`表記統一、トップページのmeta description設定(いずれも確認済み)。
- Google Search Console: 所有権確認済み、サイトマップ2件とも成功、6URL(トップページ+5記事)とも
  インデックス登録済み・canonical一致。
- 5記事それぞれの個別meta description設定(ChatGPTのSEOレビューを反映した最終版で確定)。
- Article構造化データ(JSON-LD、著者・日付・画像あり)、パンくずリスト構造化データ(JSON-LDではなく
  Microdata形式で出力、Googleはどちらも構造化データとして認識するため対応不要と判断)。
- 見出し画像は5記事とも1600×1064〜1096pxで、1200×630px以上の基準を満たす。
- サイトアイコン(favicon)を、羽根ペン+開いた本のロゴ(白背景)に更新済み。

## 現在進行中・未解決の課題
- `site:words-for-soul.com`検索で、`koshu-wine-yamanashi-beginners-guide`と`hokusai-mount-
  fuji-koshu-wine-journey`の2件が、Search Console上は「インデックス登録済み」にもかかわらず
  ヒットしない状態が続いている(30分後の再確認でも変化なし)。反映には時間がかかる可能性が高いため、
  数時間〜半日以上空けての再確認が必要。
- パンくずリストの表示が、記事タイトル自体を最後の階層に含めていない(カテゴリーまでで止まる)。
  軽微な改善余地だが優先度は低いため未着手。
- `seo_strategy_2026.md`の「中期的な施策(1〜3ヶ月)」「中長期的な施策(3ヶ月〜半年)」(E-E-A-Tの
  経験の書き込み強化、本文内での内部リンク強化、被リンク獲得、SNS発信)は未着手。
- Claude(Cowork)側の「claude-in-chrome」接続は現在失敗状態。接続できれば、Browser Claudeへの
  手動中継を介さず直接ブラウザ操作が可能になる見込みだが、Ando様側での拡張機能・連携設定の確認が
  必要。
