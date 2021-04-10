---
title: GatsbyとNetlifyで技術ブログの新規設置してみたい
date: "2021-04-10T21:59:00Z"
template: "post"
draft: false
slug: "new-blog-create"
category: "ブログ設置"
tags:
  - "Blog"
  - "Gatsby"
description: "新しくブログを開設しましたので、その手順をまとめてみたいと思います。GatsbyとNetlifyであまり手間をかけずに設置できればと思います。"
---


- <img src="https://img.shields.io/badge/node-v14.15.5-brightgreen" style="float: left;">
<img src="https://img.shields.io/badge/gatsby-3.2.0-brightgreen" style="float: left;">
<br style="clear: both" />

- [Gatsbyのインストール](#gatsbyのインストール)
- [ブログの構築](#ブログの構築)
- [自分用にカスタマイズ](#自分用にカスタマイズ)

システム開発の技術者として10年近く仕事してきたのですが、アウトプットをしてこなかったことに気づき、これから少しずつでもしていければと思いまして、ブログでもつけてみようかと思いました。

よろしくお願いいたします。

もともと面倒くさがりなので、ブログを開設するとしてもあまり手間をかけたくないと思って簡単にできるものを探していました。

GatsbyとNetlifyでお手軽にできるという記事を読みまして、こちらで対応したいと思います。

---

> Gatsbyのスターターと、Netlifyを使用して誰でも5分で爆速ブログを作成する方法を紹介します。  

https://qiita.com/k-penguin-sato/items/7554e5e7e90aa10ae225

---

## Gatsbyのインストール

下記のコマンドを実行して、Gatsbyのインストールします。

```bash
$ npm install -g gatsby-cli
```

## ブログの構築

以下のコマンドでブログを作成します。

```bash
$ gatsby new my-blog https://github.com/alxshelepenok/gatsby-starter-lumen
```

- `gatsby new`で作成
- 次にブログ名を指定
- 次にフォーマットとなるGitHubのリポジトリを指定

---

下記から好きなフォーマットを選択できるみたいでして、

Gatsby Starters: https://www.gatsbyjs.com/starters/?v=2

私はこちらを選択しました。

![キャプチャ](https://user-images.githubusercontent.com/67815204/114272046-6440e300-9a4f-11eb-8135-02fbec19e833.JPG)

https://github.com/alxshelepenok/gatsby-starter-lumen

---

そのあと、下記コマンドを実行します。

```bash
$ cd my-blog
$ gatsby develop
```

が、おそらく下記のようなエラーがでて、正常に起動できないはず・・・

```
 ERROR #98123  WEBPACK

Generating development JavaScript bundle failed

PostCSS plugin postcss-pxtorem requires PostCSS 8.
Migration guide for end-users:
https://github.com/postcss/postcss/wiki/PostCSS-8-for-end-users

File: src/components/Post/Post.module.scss
```

プラグインとして使っている`postcss-pxtorem:6.0.0`がPostCSS 8を必要としているとのエラーメッセージが出ています。

仕方ないので、下記コマンドで、postcss-pxtoremを6.0.0以前に戻す対応をしました。

```bash
$ yarn remove postcss-pxtorem
$ yarn add --dev postcss-pxtorem@^5
```

これでもう一度、下記コマンドを実行します。

```bash
$ gatsby develop
```

こんなメッセージになるはずです。

```log
success Checking for changed pages - 0.002s
success source and transform nodes - 0.484s
success building schema - 0.481s
info Total nodes: 201, SitePage nodes: 28 (use --verbose for breakdown)
success createPages - 0.104s
success Checking for changed pages - 0.002s
success createPagesStatefully - 0.091s
success update schema - 0.047s
success write out redirect data - 0.003s
success Build manifest and related icons - 0.096s
success onPostBootstrap - 0.103s
info bootstrap finished - 11.957s
success onPreExtractQueries - 0.002s
success extract queries from components - 0.669s
success write out requires - 0.047s
success run page queries - 0.028s - 1/1 36.25/s
 DONE  Compiled successfully in 3334ms
⠀
 I  Netlify CMS is running at http://localhost:8000/admin/
⠀
You can now view gatsby-starter-lumen in the browser.
⠀
  http://localhost:8000/
⠀
View GraphiQL, an in-browser IDE, to explore your site's data and schema
⠀
  http://localhost:8000/___graphql
⠀
Note that the development build is not optimized.
To create a production build, use gatsby build
⠀
success Building development bundle - 10.223s
```

`http://localhost:8000/`にアクセスしろと出ているので、アクセスすると、先ほどの画面が表示されているはずです。

## 自分用にカスタマイズ

下記ファイルを書き換えます。photo.jpgは自分の写真で上書きします。

- config.js
- static/photo.jpg

config.js
```js
'use strict';

module.exports = {
  url: 'https://lumen.netlify.com',
  pathPrefix: '/',
  title: 'Blog by Ando Junya',
  subtitle: '安藤順也のブログ',
  copyright: '© All rights reserved.',
  disqusShortname: '',
  postsPerPage: 4,
  googleAnalyticsId: 'UA-73379983-2',
  useKatex: false,
  menu: [
    {
      label: '全ての記事',
      path: '/'
    },
    {
      label: 'プロフィール',
      path: '/pages/about'
    }
  ],
  author: {
    name: '安藤順也',
    photo: '/photo.jpg',
    bio: '安藤順也です。エンジニアです（このブログおよびデザインは gatsby-starter-lumen さんから拝借しております）',
    contacts: {
      email: '',
      facebook: 'profile.php?id=100005555296352',
      telegram: '',
      twitter: 'AJ86277020',
      github: 'JunyaAndooo',
      rss: '',
      vkontakte: '',
      linkedin: '',
      instagram: '',
      line: '',
      gitlab: '',
      weibo: '',
      codepen: '',
      youtube: '',
      soundcloud: '',
      medium: '',
    }
  }
};
```

- `menu`はプロフィールの下のリンク
- `author`は左コンテンツのプロフィールに対応
- `contacts`は各SNSのアイコンが登録されており、空だったら表示しないという作り

再起動すればこんな感じになりました。

![キャプチャ2](https://user-images.githubusercontent.com/67815204/114272812-9d2e8700-9a52-11eb-9b51-5e55370360ca.JPG)