# README

## <font color="Teal">セイト先生YouTubeを参考にHTML・CSSサイトを作ってみる</font>
- YouTuberセイト先生の動画をもとに、Webサイト制作していく過程を記述していきます。

## <font color="Teal">本記事の目的</font>
- サイト制作やLP制作の仕事を受注できるようにする
- サイト制作の基本的な流れを把握してこれまでの疑問点を払拭する
- 見本サイトを真似して作り、最終的にはオリジナルサイトを作って自身のポートフォリオとする



## <font color="Teal">よく使うタグやコマンドのメモ</font>
- 青系のいい感じの色： `<font color="Teal">テキスト</font>`
- `cd ~/workspace/web_site`
- `git checkout create_site`


## <font color="Teal">参考サイト</font>

https://youtu.be/Hbxulm8iXSA?si=WZ0tvfXYCRRrRKgH

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


### ***自動生成した`html`コードに足りないのをつけたす***

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

### ***後で必要になるディレクトリやファイルを先に作っておく***

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


### ***【注意】空のディレクトリはコミット・プッシュできない***
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



### ***ついでに、CSSやJSの中身も先に定義しておこう***

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


### ***sanitize.cssも導入しておこう。***
- これはブラウザの差異をなくすためのもの。
- これもあらかじめDLしておく。以下のURLから`download`を選択
- https://csstools.github.io/sanitize.css/
- ダウンロードしたファイルを`web_site/assets/css`ディレクトリに配置させる。
- さらに、`style.css`同様、読み込ませるコードを`index.html`に記述する。
- 読み込ませる順番には注意。
- cssは後に記述した方が先に読み込まれる。
- なので、`style.css`を先に読み込ませたいので、`sanitize.css`を上、`style.css`を下に記述する。
- ここのタイミングで一旦、動作確認したいので、`body`タグに`Hello world`とか適当に書いて、出力されるかチェックする。



### ***追記したコード***
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



### ***✅つぎはここから （動画8分49秒〜）***


