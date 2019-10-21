# ECCUBE サイト制作 コーディングガイド

## 開発言語

- HTML5 / CSS3
- JavaScript / JQuery
- PHP

## オリジナルブロック制作における記法

## 共通
- 名称（ファイル名、ID名、class名）は省略しない

  例）
  | OK | NG |
  | ----- | --- |
  | title | ttl |
  | image | img |
  | text | txt |
  | | |

- 名称は、全て英語表記。
- 2単語以上使用する名称には、2単語目の頭文字で大文字英字を使用する<br>
    ```
    例）
    originalFooter
    sideNavigation
    ```

### ブロック名

- ブロック名の語頭は、必ず「tmp」とし、ブロック名との接頭辞はアンダースコア「_」とする。<br>
    ```
    例)
    語頭_ブロック名
    tmp_banner
    tmp_originalFooter
    tmp_sideNavigation
    ```

### ファイル名（twig / css）

- ブロック名と完全同一名称とする。<br>
- 語頭に「tmp_」も必ず付与する<br>
    ```
    例)
    tmp_banner.twig
    tmp_banner.css
    ```

### ファイル管理

#### twig

オリジナルブロックの twg ファイルは、ECCUBE 画面「ブロック管理」から作成すると以下ディレクトリに動的に生成されます。

```
app/template/テンプレート名/Block/ここに保存
```

## HTML

### 共通

- 基本は BEM だが、複雑な規則性を排除して簡略化した記法を用いる。
- ID 名は、html ファイル内で一意の名称にする。

### 記法 / オリジナルブロック制作
- twgファイルの開始行と最終行にはコメントアウトでブロック名称を記載する。
- 最初のdomはdivを使用し、コンポーネントを内包する。
- 最初のdomには、必ずブロック名のIDを付与する（※ただし「tmp_」は除く）
- 最初のdomには、必ずclass名「template」を付与する。
    ```
    例）
    <!-- orginalFotter -->
    <div id="orginalFotter" class="template">
        <div class="originalFooter_container">
            <h1 class="title">タイトル</h1>
            <p class="text">
                <a class="text_link" href="#">テキスト。テキスト。</a>
            </p>
        </div>
    </div>
    <!-- /orginalFotter -->
    ```

## CSS

### 共通

- html タグ、dom に直接 style を記述してはいけない。
- css を記述するときは、必ず ID 名 class 名に対して記述する。
- float は使用しない。inline-block もしくは flex-box を使用する。
- important は使用しない。

### 記法 / オリジナルブロック制作
ECCUBEのデフォルト要素との重複を防ぐために、詳細度を上げて記述する。

- 目的要素のstyleを記述する場合には、必ず先頭にIDを入力する。
    ```
    例）
        #originalFooter .title {
            color:#ff0000;
        }
    ```
### CSSファイルの管理
#### 既存のcssファイル
- cssフォルダ直下にある、以下cssは、既存の要素やレイアウトを管理しているファイルなので、基本的には触らない。
```
css/bootstrap.custom.min.css
css/default.css
css/slick.css
css/style.css
css/theme.css
```

#### オリジナルテンプレート用css
- オリジナルテンプレート用のcssファイルは、以下のディレクトリにおいて、それぞれの性質によってフォルダ別に管理する。
- オーナーにて管理するファイルなので、基本的には触らない。
```
/Users/t-nobuishii/Documents/myJob/watanabe/dev_mos/html/template/テンプレート名/css/template
```
#### 各フォルダとcssファイルの説明
- template/common.css<br>
    templateフォルダ配下のcssをimportして読み込みます。

- template/block/block_common.css<br>
    ブロックのcssを管理し、template/common.cssにインポートさせます。
    - block/compornent<br>
        既存のブロック要素に対するstyleを管理します。<br>
        個々のcssファイルは、block_common.cssにインポートさせます。

    - block/tmp_block<br>
        オリジナルで制作したtwigファイルのcssを管理します。<br>
        個々のcssファイルは、block_common.cssにインポートさせます。

- template/frame/frame_common.css<br>
    既存のレイアウトに関するstyleを修正変更するためのファイルです。<br>
    template/common.cssにインポートさせます。

- template/layout<br>
    検討中

- template/page/page_common.css
    個別ページのstyleを管理します。<br>
    template/common.cssにインポートさせます。

#### 個別修正用css
- ECサイト個別で変更したいstyleがある場合に、このディレクトリにて管理をする。
- 各ECサイトにおけるcssの記述は、このディレクトリで行う。
```
/Users/t-nobuishii/Documents/myJob/watanabe/dev_mos/html/template/テンプレート名/css/original
```
- original/elements/elements.css
    要素のstyleを記述します。

- original/layout/layout.css
    ページのレイアウトに関するstyleを記述します。
