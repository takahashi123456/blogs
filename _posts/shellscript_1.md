---
title: 'shellscriptの基本'
excerpt: 'shellscriptのコマンドや基本的な使用方法などについてまとめた記事になります'
coverImage: '/assets/blog/preview/terminal.png'
date: '2022-01-16T05:35:07.322Z'
author:
  name: H Yuki 
  picture: '/assets/blog/authors/nigaoe.JPG'
ogImage:
  url: '/assets/blog/dynamic-routing/enjin_people.png'
---

# linux commandのまとめと利用例
linuxcommandとその利用例をまとめていきます。
### pwd
今いるディレクトリの絶対パスを表示します。

```shell 
~ $ pwd

> /Users/user
```

というような使い方をし、自分が今どのディレクトリにいるのかなどの確認をします。
### ls (ls -la)
ls は今いるディレクトリ(カレントディレクトリ)の下層に何があるかの表示をします。
ls -la というのは -l(Long)を意味し詳細を表示してくれます。以下のものを表示してくれます。
- ファイルタイプ
- パーミション
- ハードリンクの数
- オーナー名
- グループ名
- バイトサイズ
- タイムスタンプ
- ファイル名
また、-aは、隠しファイルを含む全てのファイルを表示してくれることになります。

```shell
~/Users/user $ ls 

# >Desktop
# >Documents
# >Downloads
# >Library
# >Movies
# >Music
# >Pictures
# >Public
```

### mkdir
mkdir はmake directoryという名前からきていると思われるのですが、そのディレクトリの直下に新しくディレクトリを作るコマンドです。
新しくuserディレクトリの下にtestというディレクトリを使いたい場合は以下のようにします。

```shell
/Users/user $mkdir test

```
### cd
cdはchange directoryを意味し、階層移動(カレントディレクトリの移動)を行うコマンドです
先ほどmkdirで作ったtestというディレクトリに移動したい場合以下のように使います

```shell
/Users/user $cd test/

```

### touch
touch はタイムスタンプを更新するコマンドですが、touch <ファイル名>で該当するファイルがない場合、そのファイルを新規で作成してくれるコマンドで、新規作成の用途で使われていることが多い印象です。
testディレクトリの下でtest.pyを作りたい場合は以下のようになります。

```shell
/Users/user/test $touch test.py

```

### mv (ファイルを移動する、ディレクトリを移動する)
mvはmoveを意味し、ファイルの移動、ディレクトリの移動、リネームなどを行えるコマンドです。
先ほど作ったtest.pyをuserディレクトリに移動させたい場合は以下のようになります。

```shell
/Users/user $mv user/test.py ./

```

### rm (ファイルを消す、ディレクトリを消す)
rmはファイルやディレクトリを消すコマンドになります。
ディレクトリを消す場合は rm -rfと指定するとディレクトリを消すことができます。
＊「rm -rf /」 はOSを含む全ファイルを消してしますので危険なコマンドです。

先ほど作ったtest.pyを消す場合は以下のようにします。

```shell
/Users/user/ $rm test.py 

```

基本的なコマンドの説明は以上になります。

### ps(プロセス表示)
psはOS内で実行されているプロセスの一覧を表示するコマンドです。プロセスのID（PID）やCPU使用時間、コマンド名、端末番号、ユーザー名などを確認できます。
よく使われるオプションとしては a,u,xがあります。
- aは他の端末を含め、端末操作のプロセスを表示するオプションです
- xは今実行しているオプションのみを表示するオプションです。
- uはCPUやメモリの使用率なども表示するオプションです。

```shell
$ ps
# >  PID TTY           TIME CMD
# >42790 ttys001    0:07.84 /bin/zsh -l
# >65802 ttys001    0:00.18 /bin/zsh
# >66739 ttys003    0:03.23 /bin/zsh -l
```

### curl(カール)
client for URLの略でcurlと言います。さまざまなプロトコルを使用してデータ転送などを行うことができます。
基本形はcurl {URL} であり、さまざまなオプションをつけて使用することができる。
オプション例 
curl -X {リクエストメソッド} “URL”など
-L リダイレクトがあればその情報をリダイレクトがあればその情報を読み取る

```shell
$ curl -X GET "http://httpbin.org/get"
{
  "args": {}, 
  "headers": {
    "Accept": "*/*", 
    "Host": "httpbin.org", 
    "User-Agent": "curl/7.78.0", 
    "X-Amzn-Trace-Id": "Root=1-61fbc3b7-73f469053f28ccbf7c5d2473"
  }, 
  "origin": "118.10.168.238", 
  "url": "http://httpbin.org/get"
}
```

### top(CPU使用率順にソート)
topは現在実行中のプロセスをCPU利用率が高い順に表示するコマンドです。
リアルタイムで更新されていき、「q」を入力すると終了します。
top を実行中にキーを押すことで絞り込みなどを行えます。
- L <文字列> で文字列を検索しヒットしたものを表示します
- u ユーザーごとにリソースの表示をします。
使用例は以下のgrepと合わせて紹介します。


### grep(検索みたいなコマンド)
grepは検索コマンドのようなものです。文字列を含んだ行を表示します。
オプション
- -i 大文字と小文字を区別せず検索するオプションです。
- -v 一致しないものを検索するオプションです。
先程のtopコマンドにgrepし、表示してみます。

```shell
$ top | grep top
80807* top              0.0  00:00.33 2/1   0   23     5641K 0B    0B    80807 66739 running  *0[1]        0.00000 0.00000    0   2488     95      558746     277824    2086      281823    20         0       0      0.0   0      0      root                   N/A    N/A   N/A   N/A   N/A   N/A  
```

### tail
tailはデフォルトでファイルやコマンドの10行分の表示するコマンドです。
オプションとしては-数字 で表示する行を指定することができます。

```shell
$ tail -3  shellscript_1.md 

```

find
findは、実行したディレクトリ内から一致するファイルがあるかどうかを検索します。
ファイルがない場合は以下のようにエラーを出します
オプション例
- -name でファイルやディレクトリの一部を検索することができます。
- -type f でファイルを対象に検索すると指定します。
- -type d でディレクトリを指定します。

```shell
$ find ng.tx 
find: ng.tx: No such file or directory
```

### chmod #(ファイルパーミションを理解・設定できること)
以下の権限を変更するコマンドになります。
「読み取り」(4)・・・ファイルの中身を見る権限
「書き込み」(2)・・・ファイルの中身を変更する権限
「実行」(1)・・・ファイルを実行する（プログラムを実行する）権限
オプション例
- -c 変更があった場合表示されるコマンドです。

```shell
$ chmod 755 chmod.sh  
-rwxr-xr-x  1 user  staff   754  2  2 22:07 chmod.sh
```

となり、権限が全て許可、読み込みと実行を許可というものに変更することができました

### chown
chownは、そのファイルの所有者を変えるコマンドです
使い方は、chown 所有者 ファイル名 となります。他にユーザーがいないため、使用例はありません
オプション例
- -c 変更があった場合表示されるコマンドです。
- -v 実行状況を表示するコマンドです。


### ""&"" #- バックグラウンドで実行 
&はバックグラウンドジョブとして行うコマンドです。
使用例として,sleepというコマンドをバックグラウンドで実行させてそれを確認します

```shell
$ sleep 300 & 
[1] 82074
$ jobs
[1]  + running    sleep 300
```

### ""&&""
""&""は前のコマンドに成功したら後のコマンドを実行するというコマンドです。
実行結果が以下になります

```shell
$ echo "test" && echo "second"
# >test
# >second
# >失敗例
$ cd test  && echo "second"
# >cd: no such file or directory: test
```

### 参考文献
[よく使うLinuxコマンド](https://qiita.com/arene-calix/items/41d8d4ba572f1d652727#-rm)
[lsコマンドの使い方と覚えたい15のオプション【Linuxコマンド集】](https://eng-entrance.com/linux_command_ls)
