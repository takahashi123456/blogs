---
title: '出席の自動化を行いたい！'
excerpt: 'GoogleFormで行われる出席や朝の報告などの自動化を行っている記事です'
coverImage: '/assets/blog/dynamic-routing/kuma.jpeg'
date: '2022-01-25T05:35:07.322Z'
author:
  name: H Yuki 
  picture: '/assets/blog/authors/nigaoe.JPG'
ogImage:
  url: '/assets/blog/dynamic-routing/enjin_people.png'
---

こんにちわ、無職のエンジニア志望の稲沢と申します。
みなさん、テレワークやオンライン授業となって朝の報告や、出席などめんどくさいことをしなくてはいけなくなってはいませんか？
私は無職なので一切そういう煩わしさはないですが、働いている皆さんはそういうことがあると思います。

今回は題名にもあるとおり、朝の定時報告とか出席確認とかを自動化していこうと思います。
＊あくまで私の仮想での感覚のため、本投稿の書かれた事項は、自己学習を目的としたものであり、サボりの勧誘を目的としたものではありません。 最終的な決定は、自分の判断でお願いいたします。自己責任でおねがいします。一切責任は取れません。

# こんなフォームを自動入力
![スクリーンショット 2021-07-16 13.39.49.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/764631/e74ae19c-40a4-db74-2e25-bae77c6b4010.png)
このようなgoogleフォームを自動入力させていきます。(どんなフォームであってもできますが。。。)

https://twitter.com/sskei11/status/1415905868000813057?s=20

こんな感じになります

## まずは事前準備

今回はPython3を使ってプログラムを動かしていくのでまずはPython3をインストールしましょう
詳しくは

https://qiita.com/ms-rock/items/72b8f1abc661c539bb09


で見てもらえば簡単にインストールできると思います。
当然ですがコマンドプロンプトやターミナルでインストールもできますが、その方法でやる人はすでにPythonなどはインストールずみだと思うので詳しく書かなくても大丈夫でしょう()

次に今回使うパッケージです。
今回はseleniumとwebドライバーのchoromedriverを使っていきます。

seleniumのインストールはターミナル（コマンドプロンプト）に

```
pip install selenium
```
で終わりです。
chromedriver　は自分でダウンロードしてきていれることも可能ですが、いちいちパスやらをつなぐのも面倒だし、初心者にはわからないと思うので、ターミナル（コマンドプロンプト）に

```
pip install import chromedriver_binary
```

と書いてやればインストールされます。
（注）もしのちにプログラムを実行した際にエラーが出た場合、クロームのバージョンとドライバーのバージョンが違っている可能性もあるのでその場合はクロームの設定からクロームについてを確認し、バージョンを合わせてください
この記事が参考になります。

https://qiita.com/tat_aka/items/009775dc0896f9e60bd9


##いよいよプログラムを作成していく

詳しくは説明するほどでもないので全部コードを載せちゃいます

```python:sample.py
import chromedriver_binary
import time
from selenium import webdriver
from selenium.webdriver.chrome.options import Options # オプションを使うために必要

option = Options()                    # オプションを用意     
driver = webdriver.Chrome()   # Chromeを準備
driver.get('https://docs.google.com/forms/d/e/1FAIpQLSdyNm_orMGtWjkIItREL9YrVaufiVrkJh9TvymnolPWfDjFzw/viewform') #ここのurlに自分のフォームを入れてあげる
time.sleep(2)

#１問目　ラジオボタンの場合
FirstQ =  driver.find_element_by_id('i5') #１問目はid = i5 or i8
#人によってlabelのIDは違うのでChromeの開発者ツールを使ってlabelのIDを調べてあげる必要があります。
FirstQ.click()#ラジオボタンをONにする（つまりクリックする）
time.sleep(2)

#2問目　ラジオボタンの場合
SecondQ = driver.find_element_by_id('i15') #2問目はid = i15 or i18 or i21 or i24 or i27 
SecondQ.click()#ラジオボタンをONにする（つまりクリックする）
time.sleep(2)

#3問目(文字を挿入バージョン)
ThirdQ = driver.find_element_by_xpath("//input[@jsname='YPqjbf']")
#フォームのidがないのでjsnameを検索し、その内容を取得
ThirdQ.send_keys("111") #変数.send_key("文字列")で文字を入力できる

#送信ボタンを押す
submit = driver.find_element_by_xpath("//div[@jsname='M2UYVd']")
#buttonのIDを入れたかったのですが、今回はなかったので上と同様にjsnameを検索してその内容を変数に入れてます
submit.click()

time.sleep(2)
driver.quit()#開いたChromeを閉じる

```
フォームのIDの確認などはF12を押すかその他のツールからデベロッパーツールを選択するとホームページの中身が見れます。

皆さんのフォームでは少し違うと思うのでIDの変数や、URLなどを変化させる必要がありますが、大まかにはこれでできると思います！


今回はグーグルフォームの自動化の方法でしたが、新しい技術を学んでいくのは面白かったです。

もっとこうしたほうがいいよ！等ありましたらコメントでお願いします

###追記、朝に自動化するコードを忘れていました。

仮に朝九時に実行するとします
まず、pythonのパスを確認し、

```
which python3
```
これで出てきたパスをコピーし、

ターミナルで　crontab -e　と入力し

0 9 * * 1,2,3,4,5 /Users/bin/python3 /desktop/sample.py
と入力します。
User/...が先ほどコピーしたパスで、半角スペース開けて、 /desktop...というのが先ほど作ったパイソンのファイルのパスになります。

これで平日毎朝九時に自動で実行されます。

祝日等で辞めたい時はcrontab -e でコードを開き、
```
 #0 9 * * 1,2,3,4,5 /Users/bin/python3 /desktop/sample.py
```

#を先頭につけてやり、再起動することで実行されなくなります

以上になります。初めて自動でChromeをうごかせるとたのし〜

