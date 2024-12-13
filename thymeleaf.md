# テンプレートエンジン

## テンプレートエンジンとは

ブラウザからアクセスされたときに好きなHTMLを返すには

```java
@GetMapping("/greeting")
public String greeting() {
    String html = """
        <html>
            <body>
                <h1>Hello, world!</h1>
            </body>
        </html>        
    """;
	return html;
}
```

このように単純にHTMLを文字列としてプログラムから返してやれば良いことはすでに学習しました。

しかし、ここにHTMLを書いてしまっては、Javaのコードの大部分がHTMLになってしまい、読みづらくなってしまいます。
当然考えるのは、「HTMLは別のファイルに書いておいてそれを読み込んで、必要な部分だけを書き換えて出力すればよいのではないか」ということでしょう。

大枠となるHTMLを「テンプレート」としておいて、そのテンプレートには「ここは書き換えられるところだよ」というマークをしておく。
そして、プログラム側でそのマークの部分を書き換える。上手く行きそうです。

そういうことはみんなが考えるので、それは便利なライブラリとして提供されています。そのようなライブラリのことをテンプレートエンジンといいます。

とはいえ、まずは使ってみないとどういうものか実感出来ないでしょう。今回はThymeleafというライブラリを使います。覚えていますか？Spring Initialzrでbuild.gradleを作ったときに、3つだけライブラリを追加しましたね。その時の3つのうちの1つが、このThymeleafでした。ですから、もう皆さんの手元のコードはThymeleafが使える状態になっています。確認してみたければ、build.gradleのdependenciesの部分を確認してください。以下のような行が書いてあればOKです。

```
implementation 'org.springframework.boot:spring-boot-starter-thymeleaf'
```

## Thymeleafを使ってみよう(1): GreetingControllerの追加

まずはSpring Framework公式のThymeleafに関するGetting started(はじめてみよう！)という種類のガイドを読んでみましょう。

今回の場合は、以下のリンクがそれにあたります。

* [Thymeleaf Web 画面の作成](https://spring.pleiades.io/guides/gs/serving-web-content)

この記事の「Spring Initializrから開始」まではすでにやってあるので大丈夫です。「[Webコントローラーを自作する](https://spring.pleiades.io/guides/gs/serving-web-content#initial)」から始めて下さい。

今まで作ったHelloControllerとは別に、ここに書いてあるおとりのGreetingControllerを作ってみてください。

ただし、ここに書いてある20行足らずのコードを上から書いていってはいけません。プログラマはそんなことはしません。何より、皆さんの手元とパッケージ名が違いますから、そのままでは動きません。

こんな感じで作っていって下さい。これは今後も同じです。

### IDEで新規クラスを作成する

皆さんはVisual Studio Code(VSC)なり、IntelliJなり、EclipseなりJavaの開発に対応したIDEを使っていると思います。そのIDEの機能を使ってHelloController.javaと同じディレクトリで、「新規クラスファイル」を作って下さい。クラス名はガイドのとおり、"GreetingController"です。

すると、新しいファイルにはあらかじめpackage文とclass文が書かれているでしょう。私はVSCを使いました。こんな感じです

```java
package one.tmbrms.readingsns;

public class GreetingController {

}
```

### サンプルを見ながらクラスにアノテーションを書き足す

サンプルを見ると、class文の上にアノテーションで`@Controller`と書いてあります。これを付け足してやりましょう。

```
package one.tmbrms.readingsns;

import org.springframework.stereotype.Controller;

@Controller
public class GreetingController {

}
```

私は`@Controller`しか書いてないのですが、import文が勝手に足されました。皆さんのところでは勝手には足されずに、@Controllerのところに赤線が引かれるなどのなんらかのエラーが表示されているかもしれません。それは、このimportがないからです。手で足しても構いませんが、大抵はそのエラー表示を右クリックすると"Quick Fix"などの表記で「良い感じに直してやろうか？」的な意思表示をIDEがしてきますので、素直に従います。IDE側は、私たちがSpring Frameworkを使おうとしていることを知っていて、Spring Frameworkで`@Controller`と書いたらそれはorg.springframework.stereotype.Controllerのことだなということも推測出来ます。なので、大抵は正しいimportを補ってくれます。もし、違うimportを書こうとしていたら、他の候補の中から正しいのを選んでください。

ともあれ、もうほとんどこのimportを手で書く必要はないです。手で書くとこんな長い名前は間違いますからね。お任せしましょう。これが「上から手で書いてはいけない」理由です。

### メソッドを少しずつ書く

classの中身がからっぽではいけませんから、ガイドのサンプルを見ながらメソッドを書きます。そのときも上から順に書いてはいけません。最小限で動く状態から徐々に書き足します。まずは枠だけ書きます。

```java
(省略)
@Controller
public class GreetingController {

    public String greeting(){
        return "greeting";
    }

}
```

エラーになりませんね。問題ありません。`return "greeting";`は書かないとエラーになりますね。なので、書いておきましょう。常にエラーは出るたびに対処します。

ではこれに少しずつ書き足します。アノテーションを足しましょうか。エラーになったら、エラー修正をIDEにお願いして修正しましょう。

```
@Controller
public class GreetingController {

    @GetMapping("/greeting")
    public String greeting(){
        return "greeting";
    }

}
```

この状態まできました。import文はControllerとGetMappingの2行追加されてますね？OKです

では、さらにサンプルと見比べて足していきます。greetingは引数を取りますね。引数の括弧の中をまるっとコピペしましょう。私の手元では2カ所エラーになりました。

![エラーはちょっとずつ出す](pic/thymeleaf1.png)

これもimportがないために起きています。IDEに修正してもらいます。Modelの方はさすがに一般の用語すぎて第1候補が違うものでした。サンプルと見比べながら正しいのを選んでください。

![第1候補のこれはなんだろう？](pic/thymeleaf2.png)

エラーが消えたら、いよいよ最後です。メソッドの中を書きましょう。1行だけですね。`model.addAttribute("name", name);`をコピペしましょう。

これでサンプルのGreetingClassをコピぺ出来ました。

どうですか？ただのコピペにこんな手順を要求されるとは思わなかったですか？実はこれは手慣れたプログラマがコードを書くときの手順です。プログラマは頭に浮かんだコードを上から順に書いているわけでは**ありません**。エラーにならない状態を維持しながら少しずつ組み立てていきます。途中で出たエラーはその場で解消させます。

コードを一度にたくさん書かないとエラーが出るような場合、例えば、別のメソッドを先に書かなければそれを呼び出す部分がエラーになるというような場合には、「とりあえずのからっぽの呼び出し先メソッドを書いておく」あるいは「とりあえず、別の似たような違うメソッドを呼び出すようにしておく」などの詐欺じみた行為をします。そうしてでもコードがエラーになっている状態を短くするのがコーディングのコツです。コードがエラーになっている状態では、他の部分がエラーになっているのにエラーが検出されなかったり、ちょっと動かして試したいのに出来ずに間違いに気がつかなかったりというろくでもないことがおきます。コードがエラーの状態で「今日は疲れたな」といって家に帰るようなことはしてはいけないのです。明日の自分はもうなんでエラーになっているのか覚えてません。今すぐ直しましょう。

あ、エラーを消すためのごまかしのコードを書いたら、その部分にはそうコメントしておきましょう。こんな風に書くのがオススメです。

```
// TODO: とりあえずエラーを消すための処理。あとでちゃんと直すこと。
```

これは単なるプログラマの間でよく行われる慣習に過ぎないのですが、みんながよく書くので、イマドキのIDEでは`TODO:`と書いてある場所一覧を表示する機能がついています。利用しましょう。

## Thymeleafを使ってみよう(2): greeting.htmlの追加

ガイドを読み進めましょう。次はgreeting.htmlをsrc/main/resources/templatesにおきましょう。templatesというディレクトリが作りましょう。以前作ったstaticと同じ場所に作ることになります。

そうですね、HTMLはコンパイルエラーにならないので、一気に全部コピペしてもいいですよ。ま、ホントは外の枠から順に作っていくのがいいですけど。

## Thymeleafを使ってみよう(3): アクセスしてみる

ガイドはここまででOK。後はいつもの通りgradle bootRunしてみましょう。起動したら http://localhost:8080/greeting にアクセスしてください。/ にアクセスすると前回までと同じHTMLが表示されます。今回は`@GetMapping("/greeting")`と指定したのですから、/greeting にアクセスしないと。注意してください。

「Hello, world!」と表示されましたか？では、/greeting?name=世界にアクセスしてみましょう。「Hello, 世界!」になりましたか？

## Thymeleafの1次資料とチートシート

ガイド通りに動かしてみて、自分の手元でもThymeleafが動いていることは確認できました。では、次に学習に移りましょう。

まず、Thymeleafの1次資料はコレなんです。

* [Tutorial: Using Thymeleaf (ja)](https://www.thymeleaf.org/doc/tutorials/3.0/usingthymeleaf_ja.html)

日本語が用意されていて非常にありがたいんですが、これを最初から読んでいくとかなり混乱します。そもそもあまりわかりやすくない上に、Spring と組み合わせる場合はこちらを読むべきということになっているからです。

* [Tutorial: Thymeleaf + Spring](https://www.thymeleaf.org/doc/tutorials/3.1/thymeleafspring.html)

しかしながら、こちらのドキュメントも最初の方は「どうやってSpringにインテグレートされているか」という仕組みの話がされていて、知りたい話がなかなか出てきません。しかも、こっちは英語しかないですし。

日本語で書かれたチートシートでわかりやすいものがあります。最初はそれを見てもいいかもしれないです。

* [Spring Boot で Thymeleaf 使い方メモ](https://qiita.com/opengl-8080/items/eb3bf3b5301bae398cc2)

ただし、このドキュメントは最新に対応していないでしょうし、対応する気もないでしょう。このようなチートシート(いわゆるカンペ)は自分で作るのがベストです。

学生のころを思い出してください。定期テスト対策として、「これだけ覚えればOK」という項目を自分で選び出して、1枚の紙にまとめたりしませんでしたか？それをテストに持ち込んじゃったらカンニングなんですが、この「カンニングペーパー」ってテストに持ち込まなくても、それを実際に作ったら意外と頭に入るものでした。今や我々はテストを受けているわけではないので、コードを書くときにカンペを見てOKなのですから自分にあったカンペ作りというのは勉強法としてだけでなく、コードを書く上でとても有効な手段です。作ったカンペをみんなに共有するもの素晴らしいことですが(おそらく、上で紹介したものもそのように個人が学習の為にまとめたカンペなのだと思います)、大事だなと思った技術については、ぜひ、自分で作ってみることをオススメします。

### Thymeleaf、事始め

しかしながら、ちょっとしたアプリケーションを作るために知っておかなければならないことは、そんなに多くありません。わからないことがあった場合にはこれらのドキュメントを参照するのがよいですが、最低限これだけわかれば良いという内容を取り出しました。

まずは、[thymeleaf.html](https://github.com/tambara-ibm/tsjwa_3/blob/main/src/main/resources/templates/thymeleaf.html)を見てください。

理解すべきなのは、3つだけです。

1. Javaコードの変数に入っている文字列で、HTMLの中を置き換える方法
2. メッセージファイルに書いた文章で、HTMLの中を置き換える方法
3. HTMLのある部分をいくつも複製する方法

だいたいこれだけを理解すれば、後は些末なことです。実際にアプリを書くと、その些末なことで、「あれ？これはどうすればいいんだ？」となりますが、それはなったときにドキュメントを検索するなり、ChatGPTに聞くなりしてください。まずは、大まかなことを理解しましょう。

#### Javaコードの変数に入っている文字列で、HTMLの中を置き換える方法


#### メッセージファイルに書いた文章で、HTMLの中を置き換える方法

#### HTMLのある部分をいくつも複製する方法



