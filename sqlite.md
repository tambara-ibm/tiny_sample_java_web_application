# リレーショナル・データベース

## RDBとは

## SQLiteとは

SQLiteはあまりアプリに使われないけど、Excel代わりに使えるので覚えておいて欲しい。

### インストール

winget install SQLite.SQLite

### 使い方

#### REPL

* `sqlite3`でREPLモード
* `.help`でコマンド一覧

#### SQL

* [SQL As Understood By SQLite](https://www.sqlite.org/lang.html)

#### CLI

* [Command Line Shell For SQLite](https://www.sqlite.org/cli.html)

## 準備

ファイル名を指定して、sqlite3コマンドを実行する

```
PS C:\Users\318535760\Desktop\2024H2WG_Java\tsjwa_4\data> sqlite3 data.sqlite
SQLite version 3.49.1 2025-02-18 13:38:58
Enter ".help" for usage hints.
```

.tablesコマンドを実行。1つもテーブルがないことを確認して、`CREATE TABLE`する。

前回までに作ったdata.csvをそのまま入れられる様にする。

```
sqlite> .tables
sqlite> CREATE TABLE article(user_id INT, user_name TEXT, user_icon TEXT, book_name TEXT, isbn TEXT, message_id INT, content TEXT, timestamp TEXT);
```

data.csvをインポートする

```
sqlite> .import data.csv article
data.csv:1: expected 8 columns but found 1 - filling the rest with NULL
data.csv:2: expected 8 columns but found 1 - filling the rest with NULL
data.csv:3: expected 8 columns but found 1 - filling the rest with NULL
```

これはimportするファイルの想定がcsvになっていないために出るエラー

```
sqlite> .mode csv
sqlite> .import data.csv article
```

これでOK。中身を確認する

```
sqlite> select * from article;
"1,tambara,tambara-icon.png,シャーロック・ホームズの凱旋,9784120057342,101,2章まで読んだ。ホームズが腐れ大学生なんだが？,2024-02-09T01:48:54.298Z",,,,,,,
"2,Eri KUWAHARA,kuwahara-icon.png,AIリスク教本　攻めのディフェンスで危機回避＆ビジネス加速,9784296204083,102,リスクの章の3つ目まで読んだ。17個は多くない！？,2024-02-07T05:24:32.911Z",,,,,,,
"3,harimoto,harimoto-icon.png,入門 モダンLinux,9784814400218,103,ワタシ、リナックスチョットデキル,2024-01-30T10:07:32.929Z",,,,,,,
1,tambara,tambara-icon.png,"シャーロック・ホームズの凱旋",9784120057342,101,"2章まで読んだ。ホームズが腐れ大学生なんだが？",2024-02-09T01:48:54.298Z
2,"Eri KUWAHARA",kuwahara-icon.png,"AIリスク教本　攻めのディフェンスで危機回避＆ビジネス加速",9784296204083,102,"リスクの章の3つ目まで読んだ。17個は多くない！？",2024-02-07T05:24:32.911Z
3,harimoto,harimoto-icon.png,"入門 モダンLinux",9784814400218,103,"ワタシ、リナックスチョットデキル",2024-01-30T10:07:32.929Z
```

CSVで書き出されるので、形式を変えてみる

```
sqlite> .mode list
sqlite> select * from article;
1,tambara,tambara-icon.png,シャーロック・ホームズの凱旋,9784120057342,101,2章まで読んだ。ホームズが腐れ大学生なんだが？,2024-02-09T01:48:54.298Z|||||||
2,Eri KUWAHARA,kuwahara-icon.png,AIリスク教本　攻めのディフェンスで危機回避＆ビジネス加速,9784296204083,102,リスクの章の3つ目まで読んだ。17個は多くない！？,2024-02-07T05:24:32.911Z|||||||
3,harimoto,harimoto-icon.png,入門 モダンLinux,9784814400218,103,ワタシ、リナックスチョットデキル,2024-01-30T10:07:32.929Z|||||||
1|tambara|tambara-icon.png|シャーロック・ホームズの凱旋|9784120057342|101|2章まで読んだ。ホームズが腐れ大学生なんだが？|2024-02-09T01:48:54.298Z
2|Eri KUWAHARA|kuwahara-icon.png|AIリスク教本　攻めのディフェンスで危機回避＆ビジネス加速|9784296204083|102|リスクの章の3つ目まで読んだ。17個は多くない！？|2024-02-07T05:24:32.911Z
3|harimoto|harimoto-icon.png|入門 モダンLinux|9784814400218|103|ワタシ、リナックスチョットデキル|2024-01-30T10:07:32.929Z
```

## Spring boot JPAから使う

https://www.blackslate.io/articles/integrate-sqlite-with-spring-boot

### JPAとは

Java Persistence APIの略で、Java EE標準のORマッパーの仕様のこと。

Object-Relational Mappingとは、Javaプログラム上でデータを保持しているオブジェクトを、
RDBに対応づけて保存しようというもの。
これによって、プログラムが終了してもオブジェクト内のデータが保持されるから"Persistence"なワケ。

JPAは仕様なので、実装がある。代表的な実装はHibernate。というか、Hibernateが標準に取り込まれてJPAになった。



### 依存関係

build.gradleを修正。依存関係に以下を追加

```
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
implementation 'org.xerial:sqlite-jdbc:3.49.1.0'
implementation 'org.hibernate.orm:hibernate-community-dialects:6.6.13.Final'
```

一番上はJPAを使う時のStarter。Starterというのは、プロジェクトの構成を見て、
「この依存ライブラリ、使いたいですよね？」とスパイして良い感じにいろいろなライブラリを
依存に取り込んでくれる仕組み。得体が知れない。

なので、以下はStarterが入れてくれないライブラリ。SQLiteをJavaのWebアプリ開発に使うのは稀なので、
手で足してあげる必要がある。

手で足す1つ目が、SQLiteのJDBCドライバ。JDBCというのはJavaプログラムから見たときにRDBの接続が
すべて同じように扱えるようにするためのレイヤ。なので、これはRDBごとにある。

2つ目が、hibernate-community-dialects。dialectsは方言という意味で、HibernateがRDBにSQLを出すときに
各RDBごとに受け付けられるSQLの違いを吸収するためのレイヤ。HibernateはSQLiteを標準でサポートしないので、
コミュニティで作成されたものを追加しておく。

### 接続構成

application.propertiesを修正。以下を追加

```
spring.datasource.url=jdbc:sqlite:data/data.sqlite
spring.datasource.driver-class-name=org.sqlite.JDBC
spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.community.dialect.SQLiteDialect
spring.jpa.hibernate.ddl-auto=none
```

### Entityを追加

SQLiteに作成したarticleテーブルを読み込むためのクラスを作成。

ちなみに、Hibernateの設計思想から言うと、逆。ここで作ったクラスを保存するための表が作られる。

https://github.com/tambara-ibm/tsjwa_5/blob/main/src/main/java/one/tmbrms/readingsns/ArticleDB.java

### Entity Repositoryを追加

RDBに対してCRUDしてEntityを読み込んだり、保存したりする機能を自動で作ってくれる。

https://github.com/tambara-ibm/tsjwa_5/blob/main/src/main/java/one/tmbrms/readingsns/ArticleRepository.java

### Entity Repositoryを生成

MainControllerの先頭に以下を追加すると、自動的にArticleRepositoryのインスタンスを作ってくれる。
これを書いたら作ってくれるのは、Springの管理下にあるクラスだけ。
Articleではダメなので、Article.getArticleに引数でインスタンスを渡すようにしておく。

### Articleを修正

getArticleを以下の様に修正する

```
public static List<Article> getArticles(ArticleRepository articleRepository) {
        List<ArticleDB> articles = articleRepository.findAll();

        return articles.stream().map(db -> {
            Article article = new Article();
            article.setUser(db.getUserId(), db.getUserName(), db.getUserIcon());
            article.setBook(db.getBookName(), db.getIsbn());
            article.setMessage(db.getMessageId(), db.getContent(), db.getTimestamp());
            return article;
        }).collect(Collectors.toList());
        

    }
```




