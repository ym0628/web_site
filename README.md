## <font color="Teal">本記事の目的</font>
- サイト制作やLP制作の仕事を受注できるようにする
- サイト制作の基本的な流れを把握してこれまでの疑問点を払拭する
- 見本サイトを真似して作り、最終的にはオリジナルサイトを作って自身のポートフォリオとする



## <font color="Teal">よく使うタグやコマンドのメモ</font>
- `cd ~/workspace/web_site`
- `git checkout create_site`
- h2タグの色： `## ***<font color="Teal">テキスト</font>***`
- h3タグの色：`### ***<font color="SteelBlue">テキスト</font>***`
- アンカーリンク（別タブで）`<a href="URL" target="_blank">テキスト</a>`
- 画像サイズ変更 ＋ alt属性付与`<img src="" alt="" width=50%>`


## <font color="Teal">参考サイト</font>

https://youtu.be/Hbxulm8iXSA?si=WZ0tvfXYCRRrRKgH

https://zen-babbage-6a4d64.netlify.app/

https://qiita.com/ym0628/items/c348d5620fecdaf032bd

https://qiita.com/twipg/items/d8043cd4681a2780c160



## <font color="Teal">制作ログ</font>
以下に制作の記録をつけていく。

## <font color="Teal">環境構築</font>

- 任意のディレクトリにフォルダを作成　`$ mkdir web_site`
- 新しく作ったディレクトリなのでGit管理されていない状態。
- なので、Git管理するための作業を行う。
- 参考：https://qiita.com/ym0628/items/8a7b45bcde064825faa4
- GitHubで新規作成したリポジトリをgit cloneする。
- `$ git clone git@github.com:ym0628/web_site.git`
- 生成したディレクトリに移動 `$ cd ~/workspace/web_site`
- まずはhtmlファイルを生成する `$ touch index.html`
- 次にGit管理するコマンドを叩く `$ git init`
- ステータスを確認 `$ git status`
- これでGit管理化することができた。
- ちなみにGit管理下されたかどうかは、`$ tree -a`コマンドを打つとわかる。
- 隠しフォルダである`.git`が生成されているのがわかる。

```terminal
$ tree -a
.
├── .git
│   ├── HEAD
│   ├── config
│   ├── description
│   ├── hooks
│   │   ├── applypatch-msg.sample
│   │   ├── commit-msg.sample
│   │   ├── fsmonitor-watchman.sample
│   │   ├── post-update.sample
│   │   ├── pre-applypatch.sample
│   │   ├── pre-commit.sample
│   │   ├── pre-merge-commit.sample
│   │   ├── pre-push.sample
│   │   ├── pre-rebase.sample
│   │   ├── pre-receive.sample
│   │   ├── prepare-commit-msg.sample
│   │   ├── push-to-checkout.sample
│   │   └── update.sample
│   ├── info
│   │   └── exclude
│   ├── objects
│   │   ├── info
│   │   └── pack
│   └── refs
│       ├── heads
│       └── tags
└── index.html

10 directories, 18 files
```


- 次に***Git管理したくないファイル***を指定する
- まずは`.gitignore`ファイルを生成 `$ touch .gitignore`
- 生成したファイルにGit管理したくないファイルを記述する。

```:.gitignore
# macOS
.DS_Store
```

- ここまでやったら、ひとまずfirst commitする.
- これで環境構築はひとまず完了ってことで良いかな？

```terminal
$ git add .
$ git status
$ git commit -m "initial commit"
$ git log
$ git push
$ 最初のコミットでは、GitHubでプルリクエスト作成はいらないっぽい。
$ また、`git pull origin main`も必要ない。
（※これはmainブランチだから？）
```



## <font color="Teal">実装開始</font>
- ここから実装を開始していく。
- まずはローカルブランチを切って、そこに実装していく。


### ***<font color="SteelBlue">何はともあれブランチ切る</font>***

```
$ git checkout -b create_site
$ git branch
```

- `index.html`に実装していく
- `html:5`と叩くと、自動で、以下まで実装してくれる！
- `VScode 最高！`

```html:index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<body>
  
</body>
</html>
```

- 一旦、ここまで、コミット〜プッシュ〜プルリク〜プルまでやっておこう。

```terminal
$ git add .
$ git status -u
$ git commit -m "【Add】html:5まで"
$ git push
$ git push --set-upstream origin create_site
$ プルリクエスト〜マージ
$ git checkout main
$ git branch
$ git pull origin main
```

<br>
<br>

***2023/10/01***

### ***<font color="SteelBlue">自動生成した`html`コードに足りないのをつけたす</font>***

- `html:5`と打つだけで、上記のコードを自動生成してくれる。
- だが、若干足りないコードもあるので付け足していく。

```diff_html:index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
+ <title>my_site</title>
+ <meta name="description" content="ここにはメタディスクリプションが入ります。Google検索結果に表示される重要な部分のテキストを入れます。">
</head>
<body>
  
</body>
</html>

```
- タイトル`my_site`は適当です。
- `<meta name="description" content="テキスト"`
- これが足りないので付け足しました。メタディスクリプションを入れるところです。


### ***<font color="SteelBlue">後で必要になるディレクトリやファイルを先に作る</font>***

- 後で必要になるディレクトリ（フォルダ）を先に作っておきます。
- ターミナルでコマンド叩いて作ってもいいし。
- VScodeで作ってもいい。
- 作るフォルダは以下の通り。

```diff
 - web_site
+    - assets
+        - css
+        - images
+        - js
+        - videos
```

- treeコマンドでも一応、ちゃんと出来たか確認しておきます。

```terminal
$ tree
.
├── assets
│   ├── css
│   ├── images
│   ├── js
│   └── videos
└── index.html
```
- よくあるWebサイトの構成として、`assets`ディレクトリ内に、、、、
- `css`とか`js`とか、画像などのメディアのディレクトリを用意する事が多いよ。
- ついでに、`css`のファイルも作っておきましょうか。

```terminal:コマンド
`$ cd assets/css`
`$ touch style.css`
`$ cd ..`
`$ cd ..`
`$ tree`
.
├── assets
│   ├── css
│   │   └── style.css
│   ├── images
│   ├── js
│   └── videos
└── index.html
```
- `style.css`できましたね。
- 一旦、ここまでをコミットしておきます。


### ***<font color="SteelBlue">【注意】空のディレクトリはコミット・プッシュできない</font>***

- 空のディレクトリはコミット・プッシュできない
- なので、隠しファイルで`.gitignore`もしくは`.gitkeep`みたいなファイルを作っておく。
- 今回は簡単に`.gitkeep`ファイルを各種フォルダに作っておいた。
- `git status -u`で確認してみると、、、、

```terminal
$ git status -u
On branch create_site
Your branch is up to date with 'origin/create_site'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
	assets/css/.gitkeep
	assets/images/.gitkeep
	assets/js/.gitkeep
	assets/videos/.gitkeep
```
- これで、空のフォルダでもGit管理、コミット・プッシュができるようになる。
- これをなしにしてしまうと、、`git pull origin main`した時に、空のフォルダが反映されずに、
- ローカルにマージされてしまうところだった💦
- 上記対応を行ったので、再度コミットしておく。

```terminal
$ git add .
$ git status
$ git commit -m "【Add】空のフォルダにgitkeepを追加"
$ git push
$ git log
$ プルリクエスト〜マージ
$ git checkout main
$ git branch
$ git pull origin main
```

<br>

***2023/10/02***


### ***<font color="SteelBlue">ついでに、CSSやJSの中身も先に定義しておこう</font>***

- 何はともあれ、下記コードを記述するのが必要。


```css:style.css
@charset "utf-8";
```

- 続いて、`assets/js/app.js`を新規作成しておく。

```js:app.js
//まだ何も記述しない。

```

- 次に、`style.css`と`app.js`読み込む設定を`index.html`に記述する。
- `script`タグは、bodyタグの閉じタグ直前がベスト。
- なぜなら、htmlの読み込みの順番があるから。
- ただ、Googleアナリティクスは別かも。。。


### ***<font color="SteelBlue">sanitize.cssも導入しておこう。</font>***

- これはブラウザの差異をなくすためのもの。
- これもあらかじめDLしておく。以下のURLから`download`を選択
- https://csstools.github.io/sanitize.css/
- ダウンロードしたファイルを`web_site/assets/css`ディレクトリに配置させる。
- さらに、`style.css`同様、読み込ませるコードを`index.html`に記述する。
- 読み込ませる順番には注意。
- cssは後に記述した方が先に読み込まれる。
- なので、`style.css`を先に読み込ませたいので、`sanitize.css`を上、`style.css`を下に記述する。
- ここのタイミングで一旦、動作確認したいので、`body`タグに`Hello world`とか適当に書いて、出力されるかチェックする。


### ***<font color="SteelBlue">追記したコード</font>***

```diff_html:index.html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>my_site</title>
  <meta name="description" content="ここにはメタディスクリプションが入ります。Google検索結果に表示される重要な部分のテキストを入れます。">
+ <link rel="stylesheet" href="./assets/css/sanitize.css">
+ <link rel="stylesheet" href="./assets/css/style.css">
</head>
<body>

+ <p>Hello world!</p>

+ <script src="./assets/js/app.js"></script>
</body>
</html>
```

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/e47fa862-a757-887a-4d09-eac364a7d5a9.jpeg" alt="img01" width="50%">

- OK❗️きちんと文字もCSSも当たってるね！
- ここで一度、コミットしておこう。
- コミットは2023/10/03朝イチにやる❗️


<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/1ba2064b-dd38-665a-af2a-d1fc084b510b.jpeg" alt="パスをコピー" width="50%">

- ちなみに、上記のように、、、
- コーディングの途中経過を動作確認したい場合は、、、
- VScodeの場合、htmlファイルのタブを`右クリック`し、
- `パスをコピー`を押すと、ファイルのパスがコピーされるので、
- それを`ブラウザのURL欄にペースト`して開けばOK。
- `ローカル環境で開発中のhtmlサイトの画面を確認`できる。
- 私のような超絶初心者だと、これすらも知らなかったので、同じような初学者の方は参考にしてみてください。


<br>

***2023/10/06***

<br>


### ***<font color="SteelBlue">Webフォント`Google Font`を適用させる</font>***

- （動画8分49秒〜）
- https://fonts.google.com/
- 無料で使える。
- thin400
- bold700
- この2つくらいしか使わないので、これだけで良い。
- selectして、<link>をコピペするだけ。
- index.htmlの<head>タグ内にコピペ
- HTMLにはフォントデータを読み込ませている。
- style.cssの<body>タグ内にコピペ
- CSSにはフォントファミリーを読み込ませている。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/a5d2f0c6-41cd-68f5-63f8-b0b7582bc6ea.jpeg" alt="" width=50%>

```diff_html:index.html
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>my_site</title>
  <meta name="description" content="ここにはメタディスクリプションが入ります。Google検索結果に表示される重要な部分のテキストを入れます。">

+ <link rel="preconnect" href="https://fonts.googleapis.com">
+ <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
+ <link href="https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;700&display=swap" rel="stylesheet">

  <link rel="stylesheet" href="./assets/css/sanitize.css">
  <link rel="stylesheet" href="./assets/css/style.css">
</head>
<body>
```

```diff_css:style.css
@charset "utf-8";

+ body {
+ font-family: 'Noto Sans JP', sans-serif;
+ }
```
- 先ほどの赤文字のスタイルはただのテストなので、一旦コードは消した。
- ページ全体に適用させたいので、bodyタグを指定した。
- html側のbodyタグを指定しているので、即ちページ全体に適用されることになる。
- また、このコードだけでは物足りない。
- ネット環境が悪く、Web fontが読み込まれなかった場合を想定し、代替案となるその他のフォントも、ここにあらかじめ指定しおこう！
- ゴシック体のフォントファミリーのおすすめ設定をパクる。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/df8c5b77-15dc-ff0a-b9c6-b3c892c53fac.jpeg" alt="サイト画面" width=50%>


- 実装したコードは以下のようになる。
- 先のコードの`sans-serif;`の前に付け足す感じ。

```diff_css:style.css
@charset "utf-8";

body {
+ font-family: 'Noto Sans JP', "Helvetica Neue", "Helvetica", "Hiragino Sans", "Hiragino Kaku Gothic ProN", "Arial", "Yu Gothic", "Meiryo", sans-serif;
}
```

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/94a17a7b-399a-0654-ce64-6dcbf625dc51.jpeg" alt="" width=50%>

- さらに、
- フォントサイズ
- 行ボックスの高さ
- 目に優しいフォントカラー薄い黒色`#333`を指定する。
- ※`#111`とかでもいい。
- 真っ黒は`#000`だが、薄い色が目に優しいらしい。

```diff_css:style.css
@charset "utf-8";

body {
 font-family: 'Noto Sans JP', "Helvetica Neue", "Helvetica", "Hiragino Sans", "Hiragino Kaku Gothic ProN", "Arial", "Yu Gothic", "Meiryo", sans-serif;
+ font-size: 15px;
+ line-height: 1.5;
+ color: #333;
}
```

- ここまでを一旦、コミットしておく。


***2023/10/07***

### ***<font color="SteelBlue">サイト内「About」のコーディング</font>***
- 今回見本・参考とするサイトはこれ
- https://zen-babbage-6a4d64.netlify.app/

https://zen-babbage-6a4d64.netlify.app/

- とりあえず、一番トップのスライダー画像のコーディングは難しいので後回し。
- 簡単な`About`セクションの箇所をコーディングしていこう。
- `index.html`に追記していく。
- とりあえず、`<p>Hello world!</p>`はもう不要なので一旦、削除。
- bodyタグ内に記述していく。
- まずは、`section`タグを定義して、`About`セクションを作ろう。


```diff_html:index.html
<body>

  <section class="section">
    <h1 class="section-headline">About</h1>
    <figure>
      <img src="" alt="">
      <figcaption>
        <h2>What can we do?</h2>
        <p>
          テキスト テキスト テキスト テキスト テキスト テキスト テキスト<br>
          テキスト テキスト テキスト テキスト テキスト テキスト テキスト<br>
          <br>
          テキスト テキスト テキスト テキスト テキスト テキスト テキスト<br>
          テキスト テキスト テキスト テキスト テキスト テキスト テキスト<br>
        </p>
      </figcaption>
    </figure>
  </section>

  <script src="./assets/js/app.js"></script>
</body>
```

- `HTML5`の場合、`<section>`タグの中だと、`<h1>`タグは実質一個下がってh2の役割になると言われている。なので、`section`タグで区切った箇所が複数あれば、その数だけ、h1を1回ずつ使ってもOK。
- 他にも`<article>`とか`<aside>`とかも同様で、このタグの中なら、h1タグを何度使ってもOK.
- まぁ、普通に、`h2`って指定すればいい話なんだけどね。
- 動画では ***`14分前後`***で解説している。
- `<figure>`は画像とそれを説明するエリアを囲むマークアップのタグである。
- `<figcaption>`は、図や画像の説明のテキストを入れる場所としてマークアップするタグ。
- ここまでやった状況のサイト画面はこんな感じ。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/5c3e3496-54c2-399f-4e3b-20cdf9186121.jpeg" alt="sectionを定義したサイト画面" width=50%>


今日はここまで❗️

***2023/10/08***
***（動画15分40秒〜）***

- ダミー画像をフリー素材のサイトから取ってくるところから❗️
- ダミー画像はここから作れる。
- https://dummyimage.com/
- サイズや色を指定すると、勝手にURLが生成される。
- それをコピーして、index.htmlに貼り付ければOK
- ついでにalt属性にも説明のテキストを入れておく。

```diff_html:index.html
  <section class="section">
    <h1 class="section-headline">About</h1>
    <figure>
+     <img src="https://dummyimage.com/600x400/009999/fff" alt="About image">
      <figcaption>
        <h2>What can we do?</h2>
以下省略
```

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/e21eb56f-1c48-4423-e9cc-bb8cce83505a.jpeg" alt="イメージ画像の動作確認" width=50%>

- こんな感じで、イメージ画像が挿入されました。
- 動作確認取れたのでOK❗️
- その他、<figure>などのタグに、クラス属性の名前をつけておこう。
- おそらく、後々、CSSなどを適用させる際に、クラス名を定義しておかないとダメだから、、だと思う。
- 【英語学習】captionとdescription、どちらも同じような意味に思えるが、、、、ちょい違うっぽい。
- caption：画像などを説明する引用を指すらしい。
- description：これは、物事の一部を説明するという使い方らしい。
- 英語の意味も覚えると、htmlも覚えやすいかもね。
- 以下のように、`<figure>` `<img>` `<figcaption>` `<h2>` `<p>`と、セクションに定義したタグすべてに、クラス名を定義してあげる。

```diff_html:index.html
  <section class="section">
    <h1 class="section-headline">About</h1>
+   <figure class="about">
+     <img class="about-image" src="https://dummyimage.com/600x400/009999/fff" alt="About image">
+     <figcaption class="about-caption">
+       <h2 class="about-headline">What can we do?</h2>
+       <p class="about-description">
          テキスト テキスト テキスト テキスト テキスト テキスト テキスト<br>
          テキスト テキスト テキスト テキスト テキスト テキスト テキスト<br>
          <br>
          テキスト テキスト テキスト テキスト テキスト テキスト テキスト<br>
          テキスト テキスト テキスト テキスト テキスト テキスト テキスト<br>
        </p>
以下省略
```

-　ここまでやったら、一旦コミットしておいた。　



***2023/10/09***
***（動画17分00秒〜）***
***<font color="SteelBlue">サイト内aboutのコーディング「CSS」</font>***

- 先に定義した各種htmlタグのクラス名に対応するCSSを適用していきます。
- セイト先生がCSSを適用させる際にやっている裏技？
- htmlで定義した<section>タグ内のコードを全部コピってCSSに一旦まるごと貼り付ける。
- VScodeの機能を活用する。具体的には、
    - 単語をダブルクリックして何か基準となる単語（今回は`class`）を選択する
    - その状態で、`command + D`を押すと、、、
    - 同じ`class`という単語を次々と同時に選択することができる。
    - これで何か文字を変えると、`class`という文字をいっぺんに変換することができる。
    - また、その文字を基準に後ろすべての行を複数同時選択して削除したりすることもできる。
    - `command + shift を同時押し + 矢印キー`


<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/5b3067d0-f9f2-09b4-4897-b4163c92ed72.jpeg" width=50%>

- 上記のキー操作を駆使して、不要な文字列を削除していく。
- 具体的には、、、、
    - `class="`以前の文字列を削除
    - また、クラス名以降の文字列を削除
    - また、pタグのの余計なテキストを削除
- そうすると、クラス名だけを抽出した状態になる。
- また、CSSではクラス名の最初にドットをつける決まりごとにになっているので、`.` をつける。
- 最後に、クラス名の後に定義する開始タグ終了タグの範囲を決める `{}`をつける。
- 出来上がりはこんな感じになる。

```diff_css:style.css
body {
  font-family: 'Noto Sans JP', "Helvetica Neue", "Helvetica", "Hiragino Sans", "Hiragino Kaku Gothic ProN", "Arial", "Yu Gothic", "Meiryo", sans-serif;
  font-size: 15px;
  line-height: 1.5;
  color: #333;
}

+ .section {}
+ .section-headline {}
+ .about {}
+ .about-image {}
+ .about-caption {}
+ .about-headline {}
+ .about-description {}
```


***2023/10/10***

- ここまでやったら、定義したクラスにCSSのコードを書いていく
- 参考にするのは、セイト先生が提供しているサイト
- https://zen-babbage-6a4d64.netlify.app/
- `margin: 0 0 40px;`は、3つの指定だけで、中途半端だが、これでもOK
- `0 0 40px`とした場合、`top, rightとleft, bottom`という感じで適用される。
- ここまでで、一旦、動作確認

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/b32ca144-8d9c-a129-2516-c0116e924c8c.jpeg" alt="途中経過about_section_css" width=50%>

- sectionで指定したCSSによって、タイトルが中央揃えになっているのでOK。
- 続いて、aboutセクションのCSSコードを書いていく。
- `<figure>`タグのmarginが全体に適用されている。これは自動的になっているのだが、これはいらないのでmarginを0に指定し直す。
- さらに`<figcaption>`のテキストを画像の横に並べたいので、`display: flex;`を当てる。
- これは親要素`About`セクションの子要素に対して、要素を横並びにするCSSコードである。
- こんな感じになる。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/6177a167-e3d7-3c72-f263-c0efbe67264a.jpeg" alt="display: flex;の効果" width=50%>

- これで、画像とテキストが横並びになった。
- しかし、画像とテキストの隙間がなくて見づらいので、ここに空間を空ける。
- `<figcaption class="about-caption">`のクラスのpadding-leftを`15px`空ける。
- するとこんな感じに。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/da1b90c3-7d16-142f-e633-407f7c53742b.jpeg" alt="" width=50%>

- いい感じに、テキストと画像の隙間が空いたのでOK。
- あとは、`<h2 class="about-headline"></h2>`のクラスのテキスト`What can we do?`の大きさやマージンを微調整する。
- `margin: 0 0 20px;`と`font-size: 30px;`を当てた。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/1ca992f3-bcaf-7ceb-688f-e9d4bf19191b.jpeg" alt="Aboutセクション完成" width=50%>

- コードはこんな感じになった。

```diff_css:style.css
/*
section
*/
.section {
  padding: 30px 15px;
}
.section-headline {
  text-align: center;
  font-size: 40px;
  font-weight: bold;
  margin: 0 0 40px;

}

/*
about
*/
.about {
  margin: 0;
  display: flex;
}
/* .about-image {} */
.about-caption {
  padding-left: 15px;
}
.about-headline {
  margin: 0 0 20px;
  font-size: 30px;
}
/* .about-description {} */
```


ここで一旦、コミットしておく。

- AboutセクションのCSSは以下のようなことをやった。
- テキストを横並び
- セクションのタイトルを中央揃え
- キャプションのタイトルのフォントサイズなどを調整
- ダミーのテキストを追記（index.html）
- 使用しないCSSクラスをコメント化
- CSSの各クラスにコメントを追記してコンポーネントとして視覚化



***2023/10/11***

### ***<font color="SteelBlue">Featureセクションのコーディング</font>***

- こんな感じのセクションを作っていく。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/9a35c263-5962-8cd0-34b8-ee4a1b34a033.jpeg" alt="Featureセクションの見本" width=50%>

- ある程度、前のセクションのhtmlコードを流用できそうだ。
- 同じくbodyタグ内に新しいsectionタグを作っていく。
- ヘッドラインの部分をそのまま流用する。


```html:index.html
  <section class="section">
    <h1 class="section-headline">Feature</h1>

  </section>
```
- CSSで背景をグレーにする。

```css:style.css
.section.section-secondary {
  background: #efefef;
}
```

- この時、同じclassを拡張させる
- `<section class="section section-secondary">`
- このようにしてあげると良い。
- `section-headline`のCSSを再度定義する必要がなく、コードがスッキリする。
- htmlを修正する。

```diff_html:index.html
+ <section class="section section-secondary">
    <h1 class="section-headline">Feature</h1>

  </section>
```
- するとこのようになる。
- 背景がグレーになった。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/09f5ae8b-24d5-82bc-91ed-8141fe43efa7.jpeg" alt="section-secondaryを指定し、CSSを適用させた画像" width=50%>


### ***<font color="SteelBlue">Featureセクション4つ横並びアイコン・テキスト</font>***

- ulタグとliタグ、そしてdlタグとdtタグとddタグを使っていく。
- dtは小見出し、ddは子コンテンツみたいな。
- dt/ddは大きな見出しにするほどでもない感じの軽い感じの見出しみたいな感じ。
- ddにはテキストだけでなく、imgをタグを組み合わせて、画像を差し込むことができる。
- とりあえずの枠組みはこんな感じになる。
- この枠組みができたところで、4つ分、コピペして枠だけ作っておく。

```html:index.html
    <ul>
      <li>
        <dl>
          <dt>1.Great Service</dt>
          <dd>
            <img src="" alt="Great Service">
          </dd>
          <dd>Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
    </ul>
    <ul>
      <li>
        <dl>
          <dt>2.High Performance</dt>
          <dd>
            <img src="" alt="High Performance">
          </dd>
          <dd>Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
    </ul>
    <ul>
      <li>
        <dl>
          <dt>3.Strong Responsibility</dt>
          <dd>
            <img src="" alt="Strong Responsibility">
          </dd>
          <dd>Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
    </ul>
    <ul>
      <li>
        <dl>
          <dt>4.Excellent Technology</dt>
          <dd>
            <img src="" alt="Excellent Technology">
          </dd>
          <dd>Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
    </ul>
```

- ここまでやった時点での動作確認はこんな感じ。
- ちゃんとaltタグが適用されているのでいいね。
- まだ、コンテンツが縦に並んでしまっているので、これはこの後実装していく。
- 一旦ここまで！


<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/f3182a5e-0792-9564-e637-8ec69f747a11.jpeg" alt="Featureセクションの途中経過画像" width=50%>


### ***<font color="SteelBlue">Featureセクションの４つ小見出しに画像を挿入し、横並びにする</font>***


### ***✅つぎはここから （動画24分15秒〜）***

















# よく使うhtmlタグ

`<img src="" alt="" width=50%>`
`<img src="" alt="" width=50%>`
`<img src="" alt="" width=50%>`


