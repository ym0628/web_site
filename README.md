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

https://www.webcreatorbox.com/tech/css-flexbox-cheat-sheet


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



***2023/10/14***

### ***<font color="SteelBlue">Featureセクションの４つ小見出しに画像を挿入し、横並びにする</font>***


- まずはアイコン画像がFree素材なので、ネットから探してくる
- 検索`free icon images`
- こちらのサイトから持ってくる
- https://www.flaticon.com/
- サイト内で適当に`feature`とかで検索
- 好きな画像を選択して`add`赤いアイコン
- 右上`コレクション`で選択した画像をダウンロード
- 拡張子を選択。今回は256サイズを選択してダウンロード
- Finderのダウンロードフォルダに落とされるので、
- それをローカルブランチ`create_site`の
- `~/assets/images`フォルダにぶち込む
- アイコン画像の名前は任意で変えてもいいだろう。
- 本来なら相応しい名前に変えるのが良さそうだね。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/58f2d65a-ae4a-490c-8042-aa6500a3d313.jpeg" alt="画像をブッ込む" width=50%>

- 次に、使いまわせるコンポーネントを作っていく。
- `grid`というクラス名から始まるものを定義し、
- それをCSSでも定義して、デザインを適用していこう。
- コンポーネントという呼び方をすることがあるので、そんな感じだと覚えておく。
- 取り込んだ画像のパスを、imgタグのsrc属性に指定する。これで画像を読み込んでくれる。
- `./`とすることで、ホームディレクトリを省略できる。


```diff_html
  <section class="section section-secondary">
    <h1 class="section-headline">Feature</h1>

+   <ul class="grid grid-col-4">
+     <li class="grid-item">
        <dl>
          <dt>1.Great Service</dt>
          <dd>
+           <img src="./assets/images/1_great_service.png" alt="Great Service">
          </dd>
          <dd>Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
+     <li class="grid-item">
        <dl>
          <dt>2.High Performance</dt>
          <dd>
+           <img src="./assets/images/2_high_performance.png" alt="High Performance">
          </dd>
          <dd>Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
+     <li class="grid-item">
        <dl>
          <dt>3.Strong Responsibility</dt>
          <dd>
+           <img src="./assets/images/3_strong_responsibility.png" alt="Strong Responsibility">
          </dd>
          <dd>Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
+     <li class="grid-item">
        <dl>
          <dt>4.Excellent Technology</dt>
          <dd>
+           <img src="./assets/images/4_excellent_technology.png" alt="Excellent Technology">
          </dd>
          <dd>Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
    </ul>

  </section>
```

- `class="grid grid-col-4"`の数字の意味は？
- おそらく、幅のこと、
- つまり、横並びにするために、`１行に4つのコンポーネント`があるよ、ということを宣言しているんだ！
- Bootstrapライクなクラスの指定の仕方だけど、こんな感じで手作りみたいにもできる。
- 行全体を１２等分した時に、４くらいの幅を持たせようとしているのではないかなぁ_？
- ちなみに、`<ul>タグは一つでOK`。間違って４つ定義してしまっていたので削除。
- `grid-item`クラスは4つ分、コピペして定義しておく。
- 次にCSSに上記で定義したクラス名をもとにコンポーネント化していく。
- ***子要素として`>`というコードを付けている。これは初めて知ったかも！***
- 

```diff_css
/*
feature
*/
.grid {}
.grid-item {}
.grid-col-4 {}
.grid-col-4 > .grid-item {}
```

- 大元となる`.grid {}`クラス
- ４つある各コンテンツのクラス`.grid-item {}`
- そして、4つ並びに対する？クラス`.grid-col-4 {}`
- さらに、親子関係を定義するコード`.grid-col-4 > .grid-item {}`
- このように分解してコンポーネント化している。
- これで使い回ししやすい、コードになるってことかな。
- リファクタリングしやすい。可読性の高い、チーム開発に必要な考え方であると思われる。
- 続けて、定義したCSSにデザインを適用していく。
- `.grid { display: flex; }`は、要素を横並びにするコード。
- 大元にとなる`.gird`に適用させる。
- これだけで要素が横並びになったよ！
- 大元の`.grid`というクラスに`display: flex;`を定義したことによって、
- 他のセクションの３カラムの横並びとか、5つ並びの横並びとか、
- いろんなgridパターンに、この`display: flex;`を使い回すことができるのだ❗️
- これは非常に重要！

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/ed92ba61-1d39-0d5f-7122-6d230b59870f.jpeg" alt="横並びになったコンテンツ" width=50%>


- 一旦、ここでコミットしておく。
- コミット・プッシュ後は、コンフリクトを回避するため、
- ここまで使用してきたブランチを、ローカル・リモート共に削除しておく。
- 改めてローカルブランチを切り直して、実装を続けていくことにする。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/4a7fda8f-f687-3b18-595d-92fa0642ebf8.jpeg" alt="不要なリモートブランチを削除する場所" width=75%>


***2023/10/15***


- アイコン画像が大きいので、調整していく。
- 具体的には`<img>`タグのwidth heightを調整する。
- 横幅を均等に並べるために`width`をCSSに適用させる。
- `.grid-col4`が不要なので削除。
- Featureセクションでは４等分にするのでcol4だが、
- 他のセクションでは２等分だったり３等分だったりするので、
- col2やcol3といったものもあとで必要になってくる。
- なので、それも作っておく。
- 以下のようになる。
- その他、自動的に適用されるCSSで不要なものを当てないように指示する。
- 参考サイト：https://www.webcreatorbox.com/tech/css-flexbox-cheat-sheet
- 


```diff_css:style.css（追加実装分）
/*
grid
*/
.grid {
  margin: 0;
  padding: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}
.grid-item {
  list-style: none;
}
.grid-col-2 > .grid-item {
  width: 50%;
}
.grid-col-3 > .grid-item {
  width: 33.3%;
}
.grid-col-4 > .grid-item {
  width: 25%;
}

/*
feature
*/
.feature {
  text-align: center;
  padding: 0 15px;
}
.feature-headline {
  font-weight: bold;
  margin-bottom: 20px;
}
.feature-image {
  margin-bottom: 20px;
}
.feature-discription {
  margin: 0;
  text-align: left;
}
```

  `margin: 0;`cssで余分に付いている空白を０にする。
  `padding: 0;`cssで余分に付いている空白を０にする。
  `display: flex;`要素を自動的に横並びにする。
  `align-items: center;`は、display flexが付いている要素を中央揃えする
  `justify-content: center;`は、親要素に空きスペースがあった場合、子要素を水平方向のどの位置に配置するかを指定するCSSコード。
  `list-style: none;`は、CSS自動適用時にgridアイテムに箇条書きで使う「・」が勝手についてしまうので、それを無効化する。


```diff_html:index.html
    <ul class="grid grid-col-4">
      <li class="grid-item">
+       <dl class="feature">
+         <dt class="feature-headline">1.Great Service</dt>
+         <dd class="feature-image">
+           <img src="./assets/images/1_great_service.png" width="100" height="100" alt="Great Service">
          </dd>
+         <dd class="feature-discription">Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
      <li class="grid-item">
+       <dl class="feature">
+         <dt class="feature-headline">2.High Performance</dt>
+         <dd class="feature-image">
+           <img src="./assets/images/2_high_performance.png" width="100" height="100" alt="High Performance">
          </dd>
+         <dd class="feature-discription">Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
      <li class="grid-item">
+       <dl class="feature">
+         <dt class="feature-headline">3.Strong Responsibility</dt>
+         <dd class="feature-image">
+           <img src="./assets/images/3_strong_responsibility.png" width="100" height="100" alt="Strong Responsibility">
          </dd>
+         <dd class="feature-discription">Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
      <li class="grid-item">
+       <dl class="feature">
+         <dt class="feature-headline">4.Excellent Technology</dt>
+         <dd class="feature-image">
+           <img src="./assets/images/4_excellent_technology.png" width="100" height="100" alt="Excellent Technology">
          </dd>
+         <dd class="feature-discription">Text text text text text text text text text text text text text text text text text...</dd>
        </dl>
      </li>
    </ul>
```

- `width="100" height="100"`で、画像の横幅、縦幅を指定する。
- 画像の大きさ指定はCSSスタイルで当てることもできるが、htmlに指定するのが手っ取り早い。
- これをどっちするのかは、企業やクライアントによって要求が異なりそうだ。
- さらにデータリストタグにもCSSスタイルを適用させたいので、
- `<dl>`と`<dt>`と`<dd>`タグにclass名を定義する。
- CSSスタイルの状況は`Googleデベロッパーツール`を活用してCSSの状況を確認する。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/62a2d63a-d947-8061-5c7b-eef18b399bcb.jpeg" alt="Googleデベロッパーツールを活用してCSSの状況を確認する" width=50% height=50%>

- 完成したFeatureセクションの画像

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/ab8cc523-e4ef-6cc4-5cf9-1c5c7180d5b4.jpeg" alt="完成したFeatureセクションの画像" width=66% height=66%>


***ここで一旦コミットしておく。***


***2023/10/16***

### ***<font color="SteelBlue">Blogセクションのコーディング</font>***

こんな感じの完成イメージとなる。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/7c3ca3b3-e005-ecec-d1e3-bed666d82c32.jpeg" alt="Blogセクション完成イメージ" width=50% height=50%>


- まずは大体おんなじ要領で、流用できるヘッドラインあたりのhtmlタグをコピペしてくる。
- 背景は白なので、`section-secondary`はいらない。
- カラムは今回3つなので、`col-4`じゃなくて`col-3`にする。
- このカラムを３つ作ってあげる。
- すると、この時点で、3つの要素が横並びになったリストが出来上がる。
- これは、前回、`.grid-col-3 > .grid-item { width: 33.3%; }`というCSSスタイルを適用させているため。
- つまり、スタイルも流用できるわけだ！便利！


### ***<font color="SteelBlue">【Blogセクション】articleタグ（html）</font>***

- articleというタグを使っていく。
- ブログ記事なので、articleというhtmlで使える便利なタグがある。
- さらにcardというタグでカードみたいに縦長のエリアを作ってくれるタグを使う。
- `article.card`と入力してEnterを押すと、自動的に、、
- `<article class="card"></article>`というタグを作ってれる。
- これはVScodeの予測変換の標準機能もしくは、拡張機能によるものである。
- ブログ記事のエリアをクリックするだけで、その記事のリンクに飛んでくれる。
- これがcardタグの良いところである。
- その中にアンカーリンクタグを用意してあげる`<a href=""></a>`
- さらにその中に、クラスを定義してあげてる。
- `<a href="#" class="card-link"></a>`としてみる。
- 新しい記事に`span`タグでNewという文字を付け、クラス名は`class="card-label"`とする。
- spanは特に意味を持たないタグ。装飾のためだけに付けている。
- ブログ記事のイメージ画像には前回も使用したダミーを用意する。
- 今回は200*100のイメージ画像を用意する。
- 画像のURLを`src=""`に入れる。
- また、画像にもクラスを定義`img class="card-image"`
- alt属性は`thumbnail`とする。
- 次に、`<div class="card-info"></div>`を定義。
- この中に`time`タグをつけておく。これは日付を表すタグのこと。
- この時VScodeの書き方として`time.card-time`と打つと、予測変換で、クラス名をつけたtimeタグ`<time class="card-time"></time>`を簡単に生成できる。このショートカットはかなり便利！
- このtimeタグには必ず？datetime属性も漏れなくつけてあげよう！
- `datetime="yyyy-mm-dd"`
- 今回は、このコード実装日である2023-10-15を入力してあげる。
- この属性を付与することはブラウザに、この数字が日付であることを認識させることを目的としている重要な属性だ。
- あと、h1タグとpタグを用意する。
- h1を使っているのは前回の通り、articleタグがセクショニングタグであるからだ。
- 自動的に見出しの階段がひとつ落ちるように設計されているため、h1を使っても良いということである。
- 次に、投稿者を表しているアバターアイコンも用意する。
- ここはデータリストタグ３種類を使用する
- `<dl>`アバター
- `<dt>`著者の名前
- `<dd>`アバターイメージ画像（ダミー画像サイトから持ってくる）
- ここでのダミー画像のimgタグにはクラスは設けなかった（時と場合によるかも。）
- ここまでの途中経過をサイトで見ると、、、こんな感じ。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/6db62ff2-e42b-b9d0-3ab7-dfe19c6962fd.jpeg" alt="Blogセクション途中経過イメージ" width=50% height=50%>

- 追加したコードはこんな感じ。

```html:index.html
  <section class="section">
    <h1 class="section-headline">Blog</h1>

    <ul class="grid grid-col-3">
      <li class="grid-item">
        <article class="card">
          <a href="#" class="card-link"></a>
            <span class="card-label">New</span>
            <img class="card-image" src="https://dummyimage.com/200x100/f5c7f5/000000" alt="thumbnail">
            <div class="card-info">
              <time class="card-time" datetime="2023-10-15">2023.10.15</time>
              <h1 class="card-headline">Title text text text text text text text text</h1>
              <p class="card-description">Text text text text text text text text text text text text text text text text...</p>
            </div>
            <dl class="avator">
              <dt class="avator-name">Tanaka</dt>
              <dd class="avator-image">
                <img src="https://dummyimage.com/50x50/000/fff" alt="Author">
              </dd>
            </dl>
        </article>
      </li>
      <li class="grid-item">
        <article class="card">
          <a href="#" class="card-link"></a>
            <span class="card-label"></span>
            <img class="card-image" src="https://dummyimage.com/200x100/f5c7f5/000000" alt="thumbnail">
            <div class="card-info">
              <time class="card-time" datetime="2023-10-15">2023.10.15</time>
              <h1 class="card-headline">Title text text text text text text text text</h1>
              <p class="card-description">Text text text text text text text text text text text text text text text text...</p>
            </div>
            <dl class="avator">
              <dt class="avator-name">Tanaka</dt>
              <dd class="avator-image">
                <img src="https://dummyimage.com/50x50/000/fff" alt="Author">
              </dd>
            </dl>
        </article>
      </li>
      <li class="grid-item">
        <article class="card">
          <a href="#" class="card-link"></a>
            <span class="card-label"></span>
            <img class="card-image" src="https://dummyimage.com/200x100/f5c7f5/000000" alt="thumbnail">
            <div class="card-info">
              <time class="card-time" datetime="2023-10-15">2023.10.15</time>
              <h1 class="card-headline">Title text text text text text text text text</h1>
              <p class="card-description">Text text text text text text text text text text text text text text text text...</p>
            </div>
            <dl class="avator">
              <dt class="avator-name">Tanaka</dt>
              <dd class="avator-image">
                <img src="https://dummyimage.com/50x50/000/fff" alt="Author">
              </dd>
            </dl>
        </article>
      </li>
  </section>
```

- ここまではhtmlのコードを実装してきた。
- この後は、CSSスタイルを適用させて、見栄えの良い感じにしていく。

### ***<font color="SteelBlue">ちょっとした問題を解決</font>***
- なぜか、アンカーリンクを設けたのに、リンク先に飛ばないぞ、、、、
- 問題解決❗️
- <a></a>タグの、閉じタグをすぐに閉じてしまっていた。
- `<a href="#" class="card-link"></a>`❌
- 以下が正解⭕️

```diff_html
+ <a href="#" class="card-link">
    ＜中略＞
    ＜中略＞
+ </a>
```


### ***<font color="SteelBlue">【Blogセクション】作成したarticleタグにCSSを適用する</font>***

### ***2023/10/17***

- `Shit + Tab`で、インデントを一挙に揃えることができる。
- `<article class="card">`つまり、cardクラスを全部引っ張ってきて、CSSに引っ張ってくる。
- `a href`タグは、インライン要素である。
- そのため、blockスタイルで囲ってあげる必要があるらしい。
- `.card-link { display: block; }`となる。
- `text-decoration: none;`は、アンカーリンクにアンダーバーが勝手に適用されるのを無効化する。
- 何もしていないと、`text-decoration: underline;`となり、リンクのテキストにアンダーバーが入るようになる。
- リンクタグのスタイルに`position: relative;`
- ラベルタグのスタイルに`position: absolute;`
- と、入れてあげると、以下のようになる。
- 画像のなかにテキストが入り込んで、ラベルが出来上がる。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/cd5923d8-1c7e-e984-2f43-ef9b4773d6c8.png" alt="positionスタイルを適用した時の画像" width=50% height=50%>

- ラベルの背景や文字色などをつけて、体裁を整えてあげると、こんな感じになる。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/a1289c40-8390-287e-d16b-e6d60391b16b.png" alt="Newラベルの出来上がり画像" width=50% height=50%>

- ラベルの部分の出来上がりコードを抜粋するとこんな感じ。

```css:style.css
.card-link {
  display: block;
  color: #333;
  text-decoration: none;
  position: relative;
}
.card-label {
  position: absolute;
  background-color: #999;
  color: #fff;
  display: block;
  padding: 5px 10px;
  font-size: 12px;
}
```

- 親要素のアンカーリンクタグに`position:relative`をつけた状態で、、、
- 子孫・子要素に`position:absolute`をつけると、、、、
- `position:relative`の中で自由に動かすことが出来る。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/fc60fe88-871d-40ab-e30f-420298517926.jpeg" alt="ラベルのpositionをデベロッパーツールで自由に動かしている様子" width=50% height=50%>

- 次に、hoverした時の色を変えたい。
- `.card-link:hover`というクラスを別に定義してあげる。
- `background-color: #eee;`としてあげることで、hoverした時に、薄いグレーの色がかかる。
- さらに、`transition`を指定する。
- これは、指定したプロパティ（CSSスタイル）に対して、プロパティが変化するまでの秒数を指定することができる優れものである❗️
- `background-color`と、指定となるプロパティ名を付けて、、、、
- `.25s`と指定することで、`0.25秒`ホバー色が変化するタイムラグを意図的に発生させることができる❗️
- 今回は、自分好みの`0.75秒`を指定してみた。
- このtransitionは、アニメーションを作りたい時にも便利なので、おすすめらしい。
- どうやって応用するのかは知らない、、、が。


***2023/10/19***

- card-imageが少し小さいので
- 横幅をcard一杯に広げる⇨100％
- それに合わせて高さは比率を保つようにautoを指定する。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/0950cab9-6481-6f9f-e61e-6f4b72c686b6.jpeg" alt="width変更前" width=50% height=50%>

:::note info
これがこのように横幅いっぱいに画像を広げてくれます。
:::

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/5c31e4b2-e5fb-54e9-eea8-c9080ea8210c.jpeg" alt="width変更後" width=50% height=50%>


- その他、card-infoなどのテキストが全体的にpaddingが狭いので、
- 微妙に開けてあげる。
- `.card-time {}`は一旦、CSS当てずにコメントアウトしておく
- 

:::note warn
htmlタグ`<dt>と<dd>`の特性上、必ずdtが左側に先に来てしまうという特性がある。そんな時は、`flex-direction: row-reverse;`で横並びの順番を逆にできる！
:::

- `justify-content: start;`で横並びにしたdt、ddタグの要素を左側に寄せることができる。
- その他、`avator`に対してCSSプロパティの`padding`を付けて、上下の間隔を少し開ける。
- また、Newというラベルは一つだけにしたいので、<span>タグで定義していた箇所は3の2を削除。


:::note info
画像を丸くしたい場合は、`border-radius 50%`と`overflow :hidden`をセットで使おう！
:::

- 最後に、ボタンをつける。
- `Blog Page`ボタンをつける。
- `a.button`と入力すれば、、、
- `<a href="#" class="button"></a>`を自動生成してくれる。
- VScode最高！
- `display: inline-block;`はインライン要素でもあり、ブロック要素でもある
- みたいな振る舞いをさせることができる魔法である。
- 具体的には、横並びにもできるんだけど、上下左右にpadding/marginを持つことができる、
- 便利なプロパティである。
- `box-shadow`は影をつけるプロパティである。
- `box-shadow: 5px 5px 0 #bbb;`を分解すると、、、
- 最初の5pxはX軸、つまり、横にどれくらいはみ出しますか？という値を指定している。
- 次の5pxはY軸、つまり、縦、下にどれくらいはみ出しますか？という値を指定している。
- 0という箇所は、ボヤーっと感を出す値。0だと、そのままの色。
- 10pxとかにすると、ボヤッと薄い影みたいにすることができる。
- 最後に色を指定すれば影の出来上がり。

:::note info
さらに、ボタンにもホバーを設定して、transitionも設定するとオシャレ。
:::

- あとは、ボタンのmarginとかを設定して間隔をいい感じに空けるだけとなるが、、、
- ボタンは、この箇所だけでなく、複数用意しているのがこのサイトである。
- なので、ボタンに対しても、divタグでクラス名を定義してあげて、
- 汎用性の高いhtmlコードにしていこう！
- セクションごとにボタンを用意する場面があるため、
- `<section-button>`というクラス名をdivタグで設定してあげる。
- `.section-button { margin-top: 40px; text-align: center;}`
- こうしてあげることで、ボタンのCSSを使い回すことができますよ！


```html:index.html
  <section class="section">
    <h1 class="section-headline">Blog</h1>

    <ul class="grid grid-col-3">
      <li class="grid-item">
        <article class="card">
          <a href="#" class="card-link">
            <span class="card-label">New</span>
            <img class="card-image" src="https://dummyimage.com/200x100/f5c7f5/000000" alt="thumbnail">
            <div class="card-info">
              <time class="card-time" datetime="2023-10-15">2023.10.15</time>
              <h1 class="card-headline">Title text text text text text text text text</h1>
              <p class="card-description">Text text text text text text text text text text text text text text text text...</p>
            </div>
            <dl class="avator">
              <dt class="avator-name">Tanaka</dt>
              <dd class="avator-image">
                <img src="https://dummyimage.com/50x50/000/fff" alt="Author">
              </dd>
            </dl>
          </a>
        </article>
      </li>
      <li class="grid-item">
        <article class="card">
          <a href="#" class="card-link">
            <img class="card-image" src="https://dummyimage.com/200x100/f5c7f5/000000" alt="thumbnail">
            <div class="card-info">
              <time class="card-time" datetime="2023-10-15">2023.10.15</time>
              <h1 class="card-headline">Title text text text text text text text text</h1>
              <p class="card-description">Text text text text text text text text text text text text text text text text...</p>
            </div>
            <dl class="avator">
              <dt class="avator-name">Tanaka</dt>
              <dd class="avator-image">
                <img src="https://dummyimage.com/50x50/000/fff" alt="Author">
              </dd>
            </dl>
          </a>
        </article>
      </li>
      <li class="grid-item">
        <article class="card">
          <a href="#" class="card-link">
            <img class="card-image" src="https://dummyimage.com/200x100/f5c7f5/000000" alt="thumbnail">
            <div class="card-info">
              <time class="card-time" datetime="2023-10-15">2023.10.15</time>
              <h1 class="card-headline">Title text text text text text text text text</h1>
              <p class="card-description">Text text text text text text text text text text text text text text text text...</p>
            </div>
            <dl class="avator">
              <dt class="avator-name">Tanaka</dt>
              <dd class="avator-image">
                <img src="https://dummyimage.com/50x50/000/fff" alt="Author">
              </dd>
            </dl>
          </a>
        </article>
      </li>
    </ul>

    <div class="section-button">
      <a href="#" class="button">
        Blog Page
      </a>
    </div>
  </section>
```



```diff_css:style.css
<中略>

.section-button {
  margin-top: 40px;
  text-align: center;
}

<中略>

/*
card
*/
.card {
  padding: 0 10px;
}
.card-link {
  display: block;
  color: #333;
  text-decoration: none;
  position: relative;
  transition: background-color .75s;
}
.card-link:hover {
  background-color: #eee;
}
.card-label {
  position: absolute;
  background-color: #999;
  color: #fff;
  display: block;
  padding: 5px 10px;
  font-size: 12px;
}
.card-image {
  width: 100%;
  height: auto;
}
.card-info {
  padding: 5px 10px;
}
/* .card-time {} */
.card-headline {
  margin: 0;
}
.card-description {
  margin: 0;
}

/*
avotor
*/
.avator {
 display: flex;
 flex-direction: row-reverse;
 justify-content: start;
 padding: 10px; 
}
.avator-name {
  font-weight: bold;
  padding-left: 15px;
}
.avator-image {
  margin: 0;
  border-radius: 50%;
  overflow: hidden;
}

/*
button
*/
.button {
  display: inline-block;
  color: #fff;
  font-weight: bold;
  background-color: #333;
  text-align: center;
  padding: 15px 60px;
  text-decoration: none;
  border-radius: 5px;
  box-shadow: 5px 5px 0 #bbb;
  transition: box-shadow .50s;
}
.button:hover {
  box-shadow: 0 0 0
}
```

- 以上で、Blogセクションの実装は終了となる。
- 完成セクションのイメージはこちら。


<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/3c1fb6e6-a164-3238-fa25-c3801f52cc4d.jpeg" alt="" width=50% height=50%>

ここでコミットしておきます。



***2023/10/20***
### ***<font color="SteelBlue">【Contactセクション】のコーディング〜html〜</font>***


- 見本はこう。
- コンタクトフォームの見た目を作る。
- こんな感じのを作っていく。
- あくまでも見た目。
- メーラーの実装などは、バックエンドエンジニアのお仕事である。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/c5dc5359-fbb1-04f3-6f38-4e0a6845c9aa.jpeg" alt="Contactセクションの見本イメージ画像" width=50% height=50%>


- 相変わらず`<section>`タグは使いまわせそう。
- 背景は`Feature`セクションで使った`secondary`クラスを流用できるね。
- 今回使うのは`<form>`タグ。
- ボタンを押してパラメーターを送信するようなインタラクティブな要素を使う時、
- formタグはバックエンドとの連携が取りやすく、重宝する。
- html5では、`form`と打つだけで、`<form action=""></form>`が自動生成してくれる。最高！
- ほんで、このformタグ内にコンタクトフォームの見た目を作っていくわけだが、
- まず使うのは`<table>`タグである。
- あと、それぞれにクラス名も定義しておく。
- ここまでの`index.html`の実装はこんな感じ。

```html
  <section class="section section-secondary">
    <h1 class="section-headline">Contact</h1>

    <form class="form" action="">
      <table class="form-table">
        
      </table>
    </form>
  </section>
```

- 続いてテーブル内のhtmlの実装だ。
- tableタグはセットで覚える（dlやdt、ddタグみたいにセットで覚える）
- trはtable rowつまり、行のこと。枠を作る。
- thはtable headlineつまり、見出しのこと。名前とかメールアドレスとか。
- tdはtable dataつまり、各値となる。入力フォームなどの空欄のボックスを入れたり。


```html
      <table class="form-table">
        <tr>
          <th></th>
          <td></td>
        </tr>
      </table>
```

- 見本ではこの行が5行あるので、
- このセットを5つ分コピペして作っておく。
- では、まずは1行目から作っていく。
- ここはプルダウンの選択肢を作る。
- ひとまずこんな感じに実装する。


<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/b1ead093-3c07-f769-088a-b0e7a6122d77.jpeg" alt="selectタグ実装した際のイメージ画像" width=50% height=50%>


```html
        <tr>
          <th>Menu</th>
          <td>
            <select name="" id="">
              <option value="menu-1">Menu 1</option>
              <option value="menu-2">Menu 2</option>
              <option value="menu-3">Menu 3</option>
            </select>
          </td>
        </tr>
```
- selectタグでプルダウンを作る。
- optionタグはプルダウンの選択肢の項目を作る。
- valueはバックエンド側に送信するパラメーターの名前。
- `Menu 1`がクライアント側に見える見た目の選択項目である。
- `<select name="" id="">`のname属性やid属性は、バックエンド側に送信するもの。
- 今回はフロントエンドのみの実装のため、ここでは深掘りしない。
- 一旦、ここの属性は削除しておく。

***labelタグ***
- labelタグをつけると、ラベルをクリックしたときに、
- そこのフォームに勝手にフォーカスしてカーソルが移動してくれるという優れもののプロパティだ。

```html
        <tr>
          <th>
            <label for="name">
              Name
            </label>
          </th>
          <td>
            <input type="text" id="name">
          </td>
        </tr>
```

:::note info
- labelのfor属性にnameと入れてあげる
- その次のinputタグにid属性を定義し、同じnameという名前で関連づけてあげる。
- こうすることで、フォーカス機能を付与することができる！
:::

- 同じ要領で、emailにもlabelタグをつけたフォームを作ってあげよう。
- 


現在、見た目はこんな感じ。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/1d755fd4-a8a3-427d-eacd-7de0f2dcbbcc.jpeg" alt="フォームの途中経過イメージ画像" width=50% height=50%>


***2023/10/21***
***ラジオボタンの実装***

- 性別にはinputタグの属性でradioをつける。
- それぞれのragio項目にname属性でgenderという名前をつけてあげると、
- radioボタンはどれか一つにしかチェックをつけられないように制限をかけることができる。
- これはname属性を与えることで、3つの選択肢が一つのグループとして認識させることができるから。
- さらにvalue属性を与え、バックセンド側に認識させるパラメターとして設定することも忘れずに。
- さらに、こういうやつこそ、labelタグで囲ってあげると、親切だよ。
- この時のlabelタグには for属性はつけずに、その中のinputタグのテキスト「Male」に対して指定してあげる。
- ちなみに、radioというタイプのほかに、heckboxというタイプもある。
- radioが単一選択であるのに対し、checkboxは複数選択が可能となる特徴がある。
- 


***テキストエリアの実装***

- html5で`textarea`と入れるだけで、、、
- `<textarea name="" id="" cols="30" rows="10"></textarea>`を自動生成してくれる。最高❗️
- colsは1行あたりの半角で入る文字数
- rowsは行数
- この数のテキストエリアを生成してくれる。
- nameとidはバックエンド側へのパラメーターに関わるものなので今回は割愛。

***送信ボタンの実装***

- 送信ボタンを作る。
- 先に作った「Blog page」ボタンを同じhtmlタグを流用したいところだが、ここは違う、
- `<button>`タグを使用する。
- アンカーリンクではなく、値をバックエンド側に送信するボタンであるため、
- 単なる`<a href>`ではダメなのだ。
- そして、先に作ったbuttonクラスをここに流用してあげると、
- CSSは同じデザインの送信ボタンが出来上がる。
- `<button class="button" type="submit">Submit</button>`
- 少しだけ色の調整などをつけるが、一旦これでOK

***一旦ここでコミットhtmlの実装はここまで***
***2023/10/22***

- 続いてCSSを当てていきたいのだが、、、、
- まずはselectとinputタグにクラス名を定義していく。
- index.htmlのselectとinputタグにクラス名を定義していく。
- labelタグのinputのほうは、labelタグにクラス名をつけておく。
- そうすれば、labelタグのほうが親要素となるので
- Detailに関しては、textareaのほうにクラスを定義している。
- 以上、5つのContactセクションにおいて、クラスの定義が完了
    - `<select class="select" id="menu">`
    - `<input class="input" type="text" id="name">`
    - `<input class="input" type="email" id="email">`
    - `<label class="radio">`
    - `<textarea class="textarea" id="detail" cols="30" rows="10"></textarea>`
- ここからCSSスタイルを実装していく。


### ***<font color="SteelBlue">【Contactセクション】のコーディング〜CSS〜</font>***

- まずはselectのCSSからポイントは以下の通り。
- `mini-width: 500px;`は横幅を最低でも500px保ってね。というプロパティ


<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/d8769f37-bf3f-f0ac-f609-4327e7f65a57.jpeg" alt="現在select横幅画像" width=50% height=50%>

- これが以下のように幅を変化させることができる。

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/22a7fd9f-3f06-25c0-b0ae-54f208948acf.jpeg" alt="横幅指定後の画像" width=50% height=50%>

- たぶん、テキストの長さに応じたwidthになるのだが、
- こうやって横幅を、長くしたり短くしたりできるのだ。


<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/699193c9-22a1-7c32-a347-1b27933f13eb.jpeg" alt="inputにCSSを適用後の画像" width=50% height=50%>

- inputタグを使用しているNameとEmailにもCSSをあてる
- まったく同じ内容になってしまったが、まぁいいだろう。
- ragioクラスのCSSは、横幅詰まってるくらいなので、margin幅をつけてあげる。
- textareaクラスのCSSもinputと同じでいいだろう。
- ただ、高さの調整を最低でも100pxにしたいので、以下のプロパティを追加してあげる
- `min-height: 100px;`


<br>

***入力フォームにカーソルを向けた時マウスポインターを指マークに変える***


```diff_css
/*
Base style 
*/
body {
  font-family: 'Noto Sans JP', "Helvetica Neue", "Helvetica", "Hiragino Sans", "Hiragino Kaku Gothic ProN", "Arial", "Yu Gothic", "Meiryo", sans-serif;
  font-size: 15px;
  line-height: 1.5;
  color: #333;
}
+ label, select, input, textarea, button {
+    cursor: pointer;
+ }
```

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/3dab1319-cb5c-1023-f53f-557d77a6d9dc.jpeg" alt="指マークにのイメージ画像" width=50% height=50%>

- このように`cursor: pointer;`とすると、
- 入力フォームにカーソルを向けた時マウスポインターを指マークに変えることができる。

:::note warn
なお、指定するのは、`.class名`ではなく、タグである点に注意
そのため、クラス名の左側に`.`ドットが付いていないのだ。
CSSを当てる対象をクラス名にする時は`.`から始める。
対象がhtmlタグだった場合は、`.`はつけない。
:::

<br>

***フォームのテーブル全体にCSSを当てる***
- 現在、Contactフォーム全体が左側に寄っていたりする。
- フォーム全体に対して、CSSを当てるために、
- `.form`と`.form-table`に対してCSSを実装していく。
- `.form`は一旦、不要なのでコメントアウトしておく
- `/* .form {} */`

```css
.form-table {
  margin: 0 auto;
}
```
- ここ重要

:::note info
- `margin: 0 auto;`とは、、、
- ブロックレベル要素のタグに対してこのように指定すると、、、、
- marginの上下は0に指定して
- 左右を`auto`と指定してあげると、、、
- `中央寄せ`とすることができる。これ便利❗️
:::


<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/28b05e84-7ea9-6437-2e2b-62187111a07a.jpeg" alt="ブロック要素全体が左側によってしまっている画像" width=50% height=50%>

これが、こうなる❗️

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/7cadafa9-0f85-2b5e-a0af-f12d7b8f9d91.jpeg" alt="中央寄せにいっぺんに出来た瞬間の画像" width=50% height=50%>

- その他、`.form-table th`と`.form-table td`とクラスに対して、
- paddingやtext-alignの微調整を加えてあげる
- 次に、`submit`ボタンだけ左寄せのままになっている。
- まだこのbuttonは、宙ぶらりんになってしまっている。
- 以前、`Blog page`セクションで実装したボタンには、`section-button`というクラスが定義されている
- だが、今回のbuttonはちょっとクラス名的に違う。
- なぜなら、前回のボタンはアンカーリンクのボタンであるのに対して、
- 今回のボタンはフォームのsubmitボタンである。
- そのため、ここでは新しくクラス名`form-button`クラス名を定義してあげる。
- `<div>`タグを使い、余計なhtmlの見た目を変えないようにしてあげながら、クラス名を定義する

```diff_html
+     <div class="form-button">
        <button class="button" type="submit">Submit</button>
+     </div>
```
- これでクラス名が定義できたので、
- ここにCSSを当てていく。

```css
.form-button {
  margin: 40px;
  text-align: center;
}
```

:::note info
- VScodeのCSSで`margin: 40px;`とコードを書く際は、、、
- `m40`と打つだけで予測変換してくれるよ！
:::


- これでsubmitボタンも中央寄せできた。
- あと、ボタンに何か余計なスタイルが当たってしまっているので、微調整していく。
- デベロッパーツールでCSSを確認していく。
- うまくChromeのデベロッパーツールを活用しよう！


<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/7529265f-585e-3351-2605-993294431c85.jpeg" alt="デベロッパーツール活用例イメージ" width=50% height=50%>

- 画像のように一時的なスタイルとか当てることができるよ！

```css
button {
  border: 0;
}
```
- 今回は、ボタンのタグに勝手にスタイルが当たっているため、
- ベーススタイルのbuttonタグに対して、別途`border: 0;`を適用する。
- これで、余計なボーダー線が消え、ボタンのスタイルを統一することができた。

***最後にボタンの色を変える***

- ボタンの色、何色だっけ？と思った際は、
- 見本サイトからデベロッパーツールを活用しよう！
- 

<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/aaf51bb0-847f-5742-161e-d46d1d0dd782.jpeg" alt="デベロッパーツールで使用されている色を確認しているイメージ画像" width=50% height=50%>

- そのまま`.form-button`にCSSを当ててもよさそうに思えるが、
- 今回は汎用性を持たせるため。
- 別バージョンのボタンクラスを定義し、色違いのボタンのCSSを定義してあげよう。
- クラス名を変えたので、htmlのクラス名を修正


```diff_css
  .button:hover {
   box-shadow: 0 0 0
   }
+ .button.button-submission {
+   color: #92d3ca;
+  }
```

```diff_html
      <div class="form-button">
+       <button class="button button-submission" type="submit">Submit</button>
      </div>
```

- なお、`submission`は`提出`という意味
- これで、ボタンの色が変わる。

:::note info
ポイントは、他のスタイルを継承しつつ、ボタンの色だけを変えたということ❗️
:::

<br>

### ***<font color="SteelBlue">【Works】のコーディング〜html〜</font>***

- 見出しがないので、`<section>`タグは使えない。
- ではどうするか？
- `<aside>`タグというものを使用する
- このタグは、`<section>`タグと似たような振る舞いをするが、
- `<section>`のようなメインタグの補完をするような役割のタグである。
- たとえば、2カラムのサイトの右側のTwitterとかがあるようなエリアに使われることが多い
- footer近くの、ちょい足しゾーンみたいなところ。
- あくまでサブ的な要素を囲むタグと覚えておく。
- ひとまずこんな感じでOK

```diff_html
      </div>
    </form>
  </section>

+ <aside class="works">
+   <img src="https://dummyimage.com/150x80/787878/fff" alt="logo">
+   <img src="https://dummyimage.com/150x80/787878/fff" alt="logo">
+   <img src="https://dummyimage.com/150x80/787878/fff" alt="logo">
+   <img src="https://dummyimage.com/150x80/787878/fff" alt="logo">
+   <img src="https://dummyimage.com/150x80/787878/fff" alt="logo">
+ </aside>

  <script src="./assets/js/app.js"></script>
</body>
</html>
```

***2023/10/26***

### ***<font color="SteelBlue">【Works】のコーディング〜CSS〜</font>***

```CSS
.works > img {
  margin: 0 15px;
}
```
- 上記のようにすると、`works`タグの子要素であるimgタグを指定する、、、
- みたいな感じに出来るんだと思う。。。
- 子要素である画像の左右に15pxの marginを空ける
- ここは一瞬で出来ましたね。
- 完成イメージはこれ。


<img src="https://qiita-image-store.s3.ap-northeast-1.amazonaws.com/0/3486945/2e992ce3-f4e7-a4a0-06a7-5107fcfb42ea.png" alt="Worksの完成イメージ" width=50% height=50%>

- ここで`Works`の実装は終了。
- コミットしておきます。






<br>

### ***✅つぎはここから （動画 1時間17分25秒〜）***

<br><br>
<br><br>
<br><br>


# よく使うhtmlタグ

`<img src="" alt="" width=50% height=50%>`
`<img src="" alt="" width=50% height=50%>`
`<img src="" alt="" width=50% height=50%>`

