---
title: 'AtCoderに初心者が初挑戦する'
excerpt: 'ATcoderに挑戦した頃の記事です'
coverImage: '/assets/blog/dynamic-routing/cover.jpg'
date: '2020-03-16T05:35:07.322Z'
author:
  name: H Yuki 
  picture: '/assets/blog/authors/nigaoe.JPG'
ogImage:
  url: '/assets/blog/dynamic-routing/jasper.png'
---

おすすめされたこのぺージの問題を挑戦していきたいと思います。

https://qiita.com/drken/items/fd4e5e3630d0f5859067#5-%E9%81%8E%E5%8E%BB%E5%95%8F%E7%B2%BE%E9%81%B8-10-%E5%95%8F

ほとんど初心者なので、試行錯誤したこーどすべてをのせていきたいとおもいます。
競技プログラミング1日目！
1か月じっくりやってビギナーコンテストをクリアできるようになるのが目標です！
今回は三問やっていきます。
今日（21/04/17）のビギナーコンテストは腕試しとして挑戦したいと思っています。
来月にはどのくらい延ばせるのかがんばります

## 1問目

![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/764631/8b58038a-5814-0172-74fe-9661a1f70329.png)
これは基本の問題だろうと感じました。

python
```python
a,b =map(int ,input().split())
#print(a,b)
#掛け算
c =a * b 
if c % 2 == 0:
  print("Even")
else:
  print("Odd")
```


## 2問目
![image.png](https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/764631/dd1ebaa2-0476-19e7-46c9-ab348bac7afd.png)
素直に一つずつ確かめていきました。

```python
s =input()
counter = 0
if s[0] == str(1):
  counter =+ 1
if s[1] == str(1):
  counter +=1
if s[2] == str(1):
  counter +=1
 
print(counter)
```

##3問目
問題文
黒板に N 個の正の整数 
A,...,N が書かれています．

すぬけ君は，黒板に書かれている整数がすべて偶数であるとき，次の操作を行うことができます．

黒板に書かれている整数すべてを，
2で割ったものに置き換える．
すぬけ君は最大で何回操作を行うことができるかを求めてください
というものでした。

自分の中では　繰り返し（リストの中身をすべて2で割る→もし余りがなければもう一回、余りが出れば終わり）という流れを描いていました。
いざやってみるとなんかうまくいかずに試行錯誤しました
割り算とあまりの関数を作ってあげてそこに当てはめていく感じで解きました

```python 
import math
n = input()
a = list(map(int, input().split()))
count=0
#print(n,a)
def double(n):
  return n / 2
def amari(n):
  return n % 2
data1=[]
data2 =[]
data2 = list(map(amari,a))
#print(data2)
data3=[]
data3=list(map(double,a))
#print(data3)
#print(all(elem % 2 == 0 for elem in a))
#for i in a:
#for i in a　だと試行数がa以上のものができなかった（？）
i=0
while i < 8:
#i < 10 にするとREで謎のエラーが出た。
    if all(elem % 2 == 0 for elem in a):
      a=list(map(double,a))
#      print(a)
      count =count + 1
#      print(count)
    else:
      count=count
      break

#print(a)
print(count)
```

いろいろ試行錯誤しているのが読み取れると思います。
１，２問目と違って一気に難しくなったと感じました。
コードを書くのに一時間くらいかかってます。


