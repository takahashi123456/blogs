---
title: 'Next.jsでライブラリを使って、mdファイルをアップロードするブログを作ろう！'
excerpt: 'Next.ja(typescript)のBlig-starter-templateを使い一発でブログを作成する方法を紹介します'
coverImage: '/assets/blog/dynamic-routing/next.png'
date: '2022-01-18T17:35:07.322Z'
author:
  name: H Yuki
  picture: '/assets/blog/authors/nigaoe.JPG'
ogImage:
  url: '/assets/blog/dynamic-routing/cover.jpg'
---

初記事です。yukiです。今回はNext.jsのライブラリを使って誰でも超簡単にブログを作る方法をまとめたいと思います。まずはNext.jsとtemplateをインストールします。
```
npx create-next-app --example ブログ名 blog-starter-typescript-app
# or
yarn create next-app --example ブログ名 blog-starter-typescript-app
```

これだけでブログはほぼ完成です。こんな感じのブログができます。(このブログの元ですね)

<img src="/assets/blog/dynamic-routing/temp.png">


あとはデザインや使い方を学べばOKになります。

## 記事の追加とデザイン
まず記事の追加は_postsディレクトリにmdファイルを追加してあげるだけで自動で記事は追加されます。

<img src='/assets/blog/dynamic-routing/md2.png'>
以下のようなサンプルがあると思うのでコピペし、変更したい箇所を変更するだけで大丈夫です。
画像やhtmlのタグなど、また(mdファイルなので当然ですが)マークダウンも使えるので Qiitaのような感覚でもブログを作ることができます。

また、細かなデザインの変更が行いたい場合は、componentsの中から該当部分を見つけ、変更部分にCSSをを追加してあげるだけでOKです。
また、このフレームワークはtailwindを使用しているので、tailwindのタグも使用できます。

参考になれば幸いです。