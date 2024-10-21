# Live2D ウィジェット

![](https://forthebadge.com/images/badges/built-with-love.svg)
![](https://forthebadge.com/images/badges/uses-html.svg)
![](https://forthebadge.com/images/badges/made-with-javascript.svg)
![](https://forthebadge.com/images/badges/contains-cat-gifs.svg)
![](https://forthebadge.com/images/badges/powered-by-electricity.svg)
![](https://forthebadge.com/images/badges/makes-people-smile.svg)

[English](README.en.md)

## 特徴

ウェブページに Live2D のキャラクターを追加します。PJAX との互換性があり、リフレッシュなしでの読み込みがサポートされています。

<img src="assets/screenshot-2.png" width="280"><img src="assets/screenshot-3.png" width="280"><img src="assets/screenshot-1.png" width="270">

（注：上記のキャラクターモデルは表示用のものであり、本リポジトリにはモデルは含まれていません。）

以下のサンプルウェブサイトもご覧いただけます：

- [米米のブログ](https://zhangshuqiao.org) の左下角で効果を確認できます
- [demo.html](https://stevenjoezhang.github.io/live2d-widget/demo/demo.html)、基本機能を示します
- [login.html](https://stevenjoezhang.github.io/live2d-widget/demo/login.html)、NPM のログイン画面を模したもの

## 使い方

初心者の方や基本的な機能だけが必要な方は、以下の1行のコードを HTML ページの `head` または `body` に追加するだけで、キャラクターを読み込むことができます：
```xml
<script src="https://fastly.jsdelivr.net/gh/stevenjoezhang/live2d-widget@latest/autoload.js"></script>
```
コードを追加する位置は、ウェブサイトの構築方法に応じて異なります。たとえば、[Hexo](https://hexo.io) を使用している場合は、テーマのテンプレートファイルに上記のコードを追加する必要があります。他のテンプレートエンジンを使用している場合も同様の方法で修正できます。  
ウェブサイトで PJAX が有効になっている場合、キャラクターは各ページでリフレッシュする必要がないため、PJAX の更新領域の外にこのスクリプトを配置することに注意してください。

**しかし！私たちは、キャラクターをあなたのウェブサイトにもっと適したものにするために、独自の設定を行うことを強くお勧めします！**  
興味がある方は、以下の詳細な説明をご覧ください。

## 設定

`autoload.js` のソースコードを参照して、利用可能な設定項目を確認できます。`autoload.js` は自動的に3つのファイルを読み込みます：`waifu.css`、`live2d.min.js`、および `waifu-tips.js`。`waifu-tips.js` は `initWidget` 関数を作成します。これがキャラクターを読み込む主関数です。`initWidget` 関数は Object 型の引数を受け取り、キャラクターの設定を指定します。以下は設定オプションです：

| オプション | タイプ | デフォルト値 | 説明 |
| - | - | - | - |
| `waifuPath` | `string` | `https://fastly.jsdelivr.net/gh/stevenjoezhang/live2d-widget@latest/waifu-tips.json` | キャラクターのリソースパス。変更可能 |
| `apiPath` | `string` | `https://live2d.fghrsh.net/api/` | API パス。オプション |
| `cdnPath` | `string` | `https://fastly.jsdelivr.net/gh/fghrsh/live2d_api/` | CDN パス。オプション |
| `tools` | `string[]` | `autoload.js` を参照 | 読み込む小ツールボタン。オプション |

`apiPath` と `cdnPath` のうち、いずれか一方を設定できます。`apiPath` はバックエンド API の URL で、自分で構築してモデルを追加することができます（変更する内容が多く、この場では詳しく説明しません）。参考として [live2d_api](https://github.com/fghrsh/live2d_api) をご覧ください。`cdnPath` は jsDelivr のような CDN サービスを通じてリソースを読み込むことで、より安定性が増します。

## カスタマイズ

上記の「設定」部分の選択肢が不足している場合は、自分で変更できます。本リポジトリのディレクトリ構造は次のとおりです：

- `src/waifu-tips.js` はボタンとダイアログのロジックを含みます；
- `waifu-tips.js` は `src/waifu-tips.js` から自動的にパッケージ化されたもので、直接の変更は推奨されません；
- `waifu-tips.json` はトリガー条件（`selector`、CSS セレクタ）とトリガー時に表示されるテキスト（`text`）を定義します；
- `waifu.css` はキャラクターのスタイルシートです。

`waifu-tips.json` のデフォルトの CSS セレクタルールは Hexo の [NexT テーマ](http://github.com/next-theme/hexo-theme-next) に対して有効です。自分のウェブページに適用するために、独自に修正するか、新しいコンテンツを追加する必要があるかもしれません。  
**警告：`waifu-tips.json` の内容はすべての年齢層に適しているわけではなく、業務中にアクセスするのに適していない可能性があります。使用する際には、適切であることを確認してください。**

このプロジェクトの開発テスト環境をローカルでデプロイするには、Node.js と npm をインストールし、以下のコマンドを実行します：

```bash
git clone https://github.com/stevenjoezhang/live2d-widget.git
npm install
npm run build
```

質問がある場合は、Issue を提起してください。修正提案がある場合は、Pull Request を歓迎します。

## デプロイ

ローカルで変更を加えた後、変更したプロジェクトをサーバーにデプロイするか、CDN からロードしてウェブページで使用できます。

### CDN の使用

コンテンツをカスタマイズするには、このリポジトリをフォークし、変更した内容を git push で自分のリポジトリにアップロードします。この場合、使い方は次のように変わります：
```xml
<script src="https://fastly.jsdelivr.net/gh/username/live2d-widget@latest/autoload.js"></script>
```
ここで、`username` をあなたの GitHub ユーザー名に置き換えてください。CDN の内容が正常に更新されるためには、新しい git タグを作成し、GitHub リポジトリにプッシュする必要があります。そうしないと、ここでの `@latest` は更新前のファイルを指し続けます。また、CDN 自体にはキャッシュが存在するため、変更が反映されるまでには時間がかかる場合があります。関連ドキュメント：
- [Git Basics - Tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging)
- [Managing releases in a repository](https://docs.github.com/en/repositories/releasing-projects-on-github/managing-releases-in-a-repository)

### 自ホスティング

CDN を介さずにファイルをサーバーに直接配置することもできます。

- `ssh` でホストに接続できる場合は、フォークして変更したコードリポジトリをサーバーにクローンします。
- 一般的な仮想ホストのように `ssh` 接続できない場合は、ローカルでコードを修正した後、`ftp` などの方法でファイルをホストのウェブサイトのディレクトリにアップロードします。
- Hexo などのツールを使用して静的ブログをデプロイしている場合は、本プロジェクトのコードをブログのソースファイルディレクトリに配置します（たとえば `source` ディレクトリ）。ブログを再デプロイする際、関連ファイルが自動的にアップロードされます。これ
