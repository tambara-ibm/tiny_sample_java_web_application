# �����[�V���i���E�f�[�^�x�[�X

## RDB�Ƃ�

## SQLite�Ƃ�

SQLite�͂��܂�A�v���Ɏg���Ȃ����ǁAExcel����Ɏg����̂Ŋo���Ă����ė~�����B

### �C���X�g�[��

winget install SQLite.SQLite

### �g����

#### REPL

* `sqlite3`��REPL���[�h
* `.help`�ŃR�}���h�ꗗ

#### SQL

* [SQL As Understood By SQLite](https://www.sqlite.org/lang.html)

#### CLI

* [Command Line Shell For SQLite](https://www.sqlite.org/cli.html)

## ����

�t�@�C�������w�肵�āAsqlite3�R�}���h�����s����

```
PS C:\Users\318535760\Desktop\2024H2WG_Java\tsjwa_4\data> sqlite3 data.sqlite
SQLite version 3.49.1 2025-02-18 13:38:58
Enter ".help" for usage hints.
```

.tables�R�}���h�����s�B1���e�[�u�����Ȃ����Ƃ��m�F���āA`CREATE TABLE`����B

�O��܂łɍ����data.csv�����̂܂ܓ������l�ɂ���B

```
sqlite> .tables
sqlite> CREATE TABLE article(user_id INT, user_name TEXT, user_icon TEXT, book_name TEXT, isbn TEXT, message_id INT, content TEXT, timestamp TEXT);
```

data.csv���C���|�[�g����

```
sqlite> .import data.csv article
data.csv:1: expected 8 columns but found 1 - filling the rest with NULL
data.csv:2: expected 8 columns but found 1 - filling the rest with NULL
data.csv:3: expected 8 columns but found 1 - filling the rest with NULL
```

�����import����t�@�C���̑z�肪csv�ɂȂ��Ă��Ȃ����߂ɏo��G���[

```
sqlite> .mode csv
sqlite> .import data.csv article
```

�����OK�B���g���m�F����

```
sqlite> select * from article;
"1,tambara,tambara-icon.png,�V���[���b�N�E�z�[���Y�̊M��,9784120057342,101,2�͂܂œǂ񂾁B�z�[���Y�������w���Ȃ񂾂��H,2024-02-09T01:48:54.298Z",,,,,,,
"2,Eri KUWAHARA,kuwahara-icon.png,AI���X�N���{�@�U�߂̃f�B�t�F���X�Ŋ�@������r�W�l�X����,9784296204083,102,���X�N�̏͂�3�ڂ܂œǂ񂾁B17�͑����Ȃ��I�H,2024-02-07T05:24:32.911Z",,,,,,,
"3,harimoto,harimoto-icon.png,���� ���_��Linux,9784814400218,103,���^�V�A���i�b�N�X�`���b�g�f�L��,2024-01-30T10:07:32.929Z",,,,,,,
1,tambara,tambara-icon.png,"�V���[���b�N�E�z�[���Y�̊M��",9784120057342,101,"2�͂܂œǂ񂾁B�z�[���Y�������w���Ȃ񂾂��H",2024-02-09T01:48:54.298Z
2,"Eri KUWAHARA",kuwahara-icon.png,"AI���X�N���{�@�U�߂̃f�B�t�F���X�Ŋ�@������r�W�l�X����",9784296204083,102,"���X�N�̏͂�3�ڂ܂œǂ񂾁B17�͑����Ȃ��I�H",2024-02-07T05:24:32.911Z
3,harimoto,harimoto-icon.png,"���� ���_��Linux",9784814400218,103,"���^�V�A���i�b�N�X�`���b�g�f�L��",2024-01-30T10:07:32.929Z
```

CSV�ŏ����o�����̂ŁA�`����ς��Ă݂�

```
sqlite> .mode list
sqlite> select * from article;
1,tambara,tambara-icon.png,�V���[���b�N�E�z�[���Y�̊M��,9784120057342,101,2�͂܂œǂ񂾁B�z�[���Y�������w���Ȃ񂾂��H,2024-02-09T01:48:54.298Z|||||||
2,Eri KUWAHARA,kuwahara-icon.png,AI���X�N���{�@�U�߂̃f�B�t�F���X�Ŋ�@������r�W�l�X����,9784296204083,102,���X�N�̏͂�3�ڂ܂œǂ񂾁B17�͑����Ȃ��I�H,2024-02-07T05:24:32.911Z|||||||
3,harimoto,harimoto-icon.png,���� ���_��Linux,9784814400218,103,���^�V�A���i�b�N�X�`���b�g�f�L��,2024-01-30T10:07:32.929Z|||||||
1|tambara|tambara-icon.png|�V���[���b�N�E�z�[���Y�̊M��|9784120057342|101|2�͂܂œǂ񂾁B�z�[���Y�������w���Ȃ񂾂��H|2024-02-09T01:48:54.298Z
2|Eri KUWAHARA|kuwahara-icon.png|AI���X�N���{�@�U�߂̃f�B�t�F���X�Ŋ�@������r�W�l�X����|9784296204083|102|���X�N�̏͂�3�ڂ܂œǂ񂾁B17�͑����Ȃ��I�H|2024-02-07T05:24:32.911Z
3|harimoto|harimoto-icon.png|���� ���_��Linux|9784814400218|103|���^�V�A���i�b�N�X�`���b�g�f�L��|2024-01-30T10:07:32.929Z
```

## Spring boot JPA����g��

https://www.blackslate.io/articles/integrate-sqlite-with-spring-boot

### JPA�Ƃ�

Java Persistence API�̗��ŁAJava EE�W����OR�}�b�p�[�̎d�l�̂��ƁB

Object-Relational Mapping�Ƃ́AJava�v���O������Ńf�[�^��ێ����Ă���I�u�W�F�N�g���A
RDB�ɑΉ��Â��ĕۑ����悤�Ƃ������́B
����ɂ���āA�v���O�������I�����Ă��I�u�W�F�N�g���̃f�[�^���ێ�����邩��"Persistence"�ȃ��P�B

JPA�͎d�l�Ȃ̂ŁA����������B��\�I�Ȏ�����Hibernate�B�Ƃ������AHibernate���W���Ɏ�荞�܂��JPA�ɂȂ����B



### �ˑ��֌W

build.gradle���C���B�ˑ��֌W�Ɉȉ���ǉ�

```
implementation 'org.springframework.boot:spring-boot-starter-data-jpa'
implementation 'org.xerial:sqlite-jdbc:3.49.1.0'
implementation 'org.hibernate.orm:hibernate-community-dialects:6.6.13.Final'
```

��ԏ��JPA���g������Starter�BStarter�Ƃ����̂́A�v���W�F�N�g�̍\�������āA
�u���̈ˑ����C�u�����A�g�������ł���ˁH�v�ƃX�p�C���ėǂ������ɂ��낢��ȃ��C�u������
�ˑ��Ɏ�荞��ł����d�g�݁B���̂��m��Ȃ��B

�Ȃ̂ŁA�ȉ���Starter������Ă���Ȃ����C�u�����BSQLite��Java��Web�A�v���J���Ɏg���̂͋H�Ȃ̂ŁA
��ő����Ă�����K�v������B

��ő���1�ڂ��ASQLite��JDBC�h���C�o�BJDBC�Ƃ����̂�Java�v���O�������猩���Ƃ���RDB�̐ڑ���
���ׂē����悤�Ɉ�����悤�ɂ��邽�߂̃��C���B�Ȃ̂ŁA�����RDB���Ƃɂ���B

2�ڂ��Ahibernate-community-dialects�Bdialects�͕����Ƃ����Ӗ��ŁAHibernate��RDB��SQL���o���Ƃ���
�eRDB���ƂɎ󂯕t������SQL�̈Ⴂ���z�����邽�߂̃��C���BHibernate��SQLite��W���ŃT�|�[�g���Ȃ��̂ŁA
�R�~���j�e�B�ō쐬���ꂽ���̂�ǉ����Ă����B

### �ڑ��\��

application.properties���C���B�ȉ���ǉ�

```
spring.datasource.url=jdbc:sqlite:data/data.sqlite
spring.datasource.driver-class-name=org.sqlite.JDBC
spring.jpa.show-sql=true
spring.jpa.database-platform=org.hibernate.community.dialect.SQLiteDialect
spring.jpa.hibernate.ddl-auto=none
```

### Entity��ǉ�

SQLite�ɍ쐬����article�e�[�u����ǂݍ��ނ��߂̃N���X���쐬�B

���Ȃ݂ɁAHibernate�̐݌v�v�z���猾���ƁA�t�B�����ō�����N���X��ۑ����邽�߂̕\�������B

https://github.com/tambara-ibm/tsjwa_5/blob/main/src/main/java/one/tmbrms/readingsns/ArticleDB.java

### Entity Repository��ǉ�

RDB�ɑ΂���CRUD����Entity��ǂݍ��񂾂�A�ۑ������肷��@�\�������ō���Ă����B

https://github.com/tambara-ibm/tsjwa_5/blob/main/src/main/java/one/tmbrms/readingsns/ArticleRepository.java

### Entity Repository�𐶐�

MainController�̐擪�Ɉȉ���ǉ�����ƁA�����I��ArticleRepository�̃C���X�^���X������Ă����B
����������������Ă����̂́ASpring�̊Ǘ����ɂ���N���X�����B
Article�ł̓_���Ȃ̂ŁAArticle.getArticle�Ɉ����ŃC���X�^���X��n���悤�ɂ��Ă����B

### Article���C��

getArticle���ȉ��̗l�ɏC������

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




