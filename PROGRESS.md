# Words for Soul 進捗ログ

記録形式: `## YYYY-MM-DD` の見出しの下に、担当・内容を簡潔に記載する。新しい日付を上に追加していく。

## 2026-09-06(確定、確認日時 2026-09-06 03:39頃JST)
- 担当: Claude(Cowork)+ Browser Claude、ChatGPTと相互確認
- ［確認方法の教訓］外部からページを取得しAIが要約する方式の確認(Claude側のWebFetch)は、同一ページを短時間で取得し直すだけで結果が食い違うことが判明し、信頼できないと判断した。以後、本文中の文字列パターンの有無は、WordPress管理画面のコードエディタで生データを機械的に検索する方法(Browser Claude)、および公開ページのDOMからhref属性を機械的に抽出する方法(ChatGPT)を、共に信頼できる一次情報として扱う。
- ［保存データ確認・公開HTML確認、両方一致］投稿15・41・44・46・48のリンク出現回数を、他4記事へのリンクパターンごとに数えた結果、全投稿・全パターンで「/ja/なし」は0件だった。詳細(投稿15・46の内訳):
  - 投稿15→他4記事へのリンクはそれぞれ3箇所ずつ出現、全て/ja/付き
  - 投稿46→hokusai-mount-fuji-koshu-wine-journey・dazai-fugaku-hyakkei-misaka-pass・kawaguchiko-fuji-view-hotel-guideへのリンクがそれぞれ1箇所ずつ出現、全て/ja/付き(hokusai-thirty-six-views-fuji-guideへの言及は本文中になし)
  - 投稿41・44・48も同様に該当パターン0件(前回確認済み)
- ［保存データ確認・公開HTML確認、両方一致］トップページのmeta descriptionは次の3値が一致した。
  - 管理画面設定値(Cocoon設定→タイトル→サイトの説明):「物語から始まる、大人の知的な旅」
  - 公開HTMLの`<meta name="description">`:「物語から始まる、大人の知的な旅」
  - OGP・Twitter用description(`og:description`/`property="twitter:description"`):いずれも「物語から始まる、大人の知的な旅」
- ［公開HTML確認］`/sitemap.xml`・`/wp-sitemap.xml`は正常に表示される。
- ［認証画面確認・Claude未検証、本人またはChatGPT報告のみ］Search Console所有権確認、インデックス拒否設定の解除、6URLのインデックス登録申請。ログイン情報を伴うためClaude・Browser Claudeでは直接確認していない。
- ［公開検索確認・未実施］Google検索結果への実際の表示状況は今回未確認。次回以降の課題とする。

## 2026-09-05

- 担当: Claude(Cowork)
- 投稿15・41・44・48の本文内にある内部リンクの`/ja/`プレフィックス抜けを特定した。投稿46は確認の結果、既に修正済みだった。ハブ記事(投稿15)自身へのリンクパターンが、従来の修正リストに含まれていなかったことも判明。Browser Claude向けの修正指示書を作成した。
- トップページのmeta descriptionは「物語から始まる、大人の知的な旅」で設定済みであることを再確認した(外部チェックツール側の誤検知だった)。
- Google Search Console登録・サイトマップ送信・主要URLのインデックス登録申請の手順書を作成した。
- Claude / ChatGPT / Geminiの役割分担、GitHub進捗ログの運用方針、Codexの位置づけについて整理した(詳細は非公開の運用ルール文書を参照)。
