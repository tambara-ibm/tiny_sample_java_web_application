# CSS

## CSSとは

前回、HTMLを勉強してみたところ、ビジネス文書しか書けるようになりませんでした。キャッチーな文句を

<center><span style="font-size:100pt">どーん！</span></center>

と真ん中にでっかい文字で表示する方法など教えてもらえませんでした。だって、ビジネス文書ではそんなことしませんから。

HTMLではあくまで「ここは見出し」とか「ここがヘッダ」のような構造だけを記述します。もちろん、「いやそんなこと言ったって、<span style="color:red;">文字を赤にしたい</span>もん」という要望は最初からあったので、HTMLにもその機能はあります。ありますが、それを使うのは止めて、「ヘッダは、48ポイントで、背景が青で文字の色は白にする」という情報は別に記述しましょうということにしました。そうしないと、画面上に出てくる見出しの1つ1つにその指定をするハメになりますから。画面デザインの指定をする書式のことをCSSといいます。今回は、CSSを学びます。

## CSSの一次資料

前回の続き。MDNのチュートリアルを読んでいきましょう。読むだけじゃなく、自分で触ってみる(写経する)のがベストです。でも、分量が多いので、最初はざっと流し読みでもOKです。どこでどんな話をしていたのか掴んでおけば、後でもう一度見に来ればよいのです。

1. 「[CSSの第一歩](https://developer.mozilla.org/ja/docs/Learn/CSS/First_steps)」は、「[CSSとは何か](https://developer.mozilla.org/ja/docs/Learn/CSS/First_steps/What_is_CSS)」から「[経歴ページのスタイル設定](https://developer.mozilla.org/ja/docs/Learn/CSS/First_steps/Styling_a_biography_page)」まで、全てを読んで下さい。
1. 「[CSS の構成要素](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks)」も全部を読めれば読んで欲しいのですが、ちょっと大変ですよね。以下だけを頑張って読んで下さい。
    * 「[CSS セレクター](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Selectors)」
    * 「[要素型、クラス、ID セレクター](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Selectors/Type_Class_and_ID_Selectors)」
    * 「[結合子](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Selectors/Combinators)」
    * 「[カスケード、詳細度、継承](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance)」
    * 「[ボックスモデル](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/The_box_model)」
    * 「[背景と境界線](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Backgrounds_and_borders)」
    * 「[CSS の値と単位](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Values_and_units)」
    * 「[画像、メディア、フォーム要素](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Images_media_form_elements)」
    * 「[表のスタイル設定](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Styling_tables)」
    * 「[CSS のデバッグ](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Debugging_CSS)」
    * 「[CSS の整理](https://developer.mozilla.org/ja/docs/Learn/CSS/Building_blocks/Organizing)」
* 「[テキストの装飾](https://developer.mozilla.org/ja/docs/Learn/CSS/Styling_text)」は、全部読んで下さい。
* 「[CSS レイアウト](https://developer.mozilla.org/ja/docs/Learn/CSS/CSS_layout)」は、「[CSS レイアウト入門](https://developer.mozilla.org/ja/docs/Learn/CSS/CSS_layout/Introduction)」だけ読んで下さい。

## CSSのパワー

前節の終わりに、ちょっとだけDTPの話をしました。DTPというのは、ページのどこにどんな要素を入れるのか自由にレイアウトできるようなソフトウェアです。日本人は画面上のどこにでも何か書いたり、絵を貼ったりできるのが好きです。小学校のころに作った学級新聞に始まり、何かの申込用紙のようなフォーマットや、ソフトウェアの設計書まで縦書き、横書きを織り交ぜた書式を作ってしまいがちです。「Excel方眼紙」なんてものが使われるのは、「画面上のここに、この長さの文章を置きたい！」という強い欲求を感じます。日本人の書式の好みは非常にDTP的だと言えます。

しかし、横書きしか許されず、文字数ではなく単語単位で文章の長さをカウントする英語文化の人達は、画面上に2次元に配置した枠に文章を流し込むのは苦手です。見出し・本文・図などが縦に一直線に並んだ1次元的なレイアウトを好みます。HTMLで作られたツリー構造の文書を、1次元的に縦にずっと並べていくのが、「CSS レイアウト入門」で学習した通常フローです。しかし、それ以外のグリッドや、フレックスボックス、絶対位置指定などを使えばこのルールを完全に変えることが出来ます。HTML上の特定の構造をセレクターで選んで、好きなように装飾して、サイズも好きなように変えて、画面上に好きなルールで配置する。これがビジネス文書をスーパーのチラシのような見た目にすら変えられるCSSのパワーです。

もちろん、パワーの乱用はよくありません。最終的な画面を作りやすいHTMLと、理解しやすいCSSを作ることは大事です。それを実現するためのツールもいろんなものがあるのですが、まずは普通のHTMLとCSSで様々な試行錯誤をしてみるのが大事だと思います。









