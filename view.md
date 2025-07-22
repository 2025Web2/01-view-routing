---
sort: 2
---

# ビューについて

ビューは、MVCモデルでいうところの「V(View)」に相当します。<br>
![](./images/mvc_v.png)

ビューは、ユーザーに表示されるWebページのことを指します。
LaravelではBladeテンプレートを使用することで、より動的で再利用可能なコンテンツを作成することができます。

## Bladeテンプレートについて

Bladeテンプレートは、Laravelのテンプレートエンジンで、よりクリーンで保守しやすいHTMLを書くことができます。
ここでいうテンプレートエンジンとは、**HTMLテンプレート内に変数や制御構造を埋め込むための仕組み**({% raw %}`{{  }}`{% endraw %}、ディレクティブ(`@`)など)のことです。

通常のHTMLファイルでは動作しないため、必ずファイル名には「**.blade.php**」という拡張子をつけることを忘れないようにしましょう。

## ビューの作成

まずは、簡単なビューを作成してみましょう。
といっても、中身は前期で学んだHTMLの知識を使ってほぼほぼ作成するだけです。
では、`resources/views`ディレクトリ内に、`index.blade.php`を作成してください。
以下に簡単な入力フォームを作成する例を示します。

**resources/views/index.blade.php**

```php
<!DOCTYPE html>
<html lang="ja">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>サンプル</title>
</head>

<body>
<h3>入力フォーム〜プルダウン〜</h3>
<!-- サンプルのためaction属性は空白にしています-->
<form method="POST" action="">
   @csrf
   ジャンル
   <select name="genre">
      <option value="pc">パソコン</option>
      <option value="book">ブック</option>
      <option value="music">ミュージック</option>
   </select>
   <input type="submit" value="送信">
</form>
</body>
</html>
```

一部前期と違う記載方法がありますので解説します。

**【解説】**

`@csrf`<br>
Bladeテンプレートでは、上記のように`@`から始まる**ディレクティブ**を使って、特定の処理を行うことができます。
`@csrf`ディレクティブは、Laravelが自動的にCSRFトークンを生成し、フォーム送信時のセキュリティを強化します。

ここでいうCSRFトークンとは、クロスサイトリクエストフォージェリ(CSRF)攻撃からアプリケーションを保護するためのセキュリティ対策の一つです。
CSRFトークンを使うことで、フォーム送信時に外部からの不正なリクエストを防ぐことができます。

なお、Laravelのデフォルトの設定では、`<form>`タグを使用する際には、必ず`@csrf`ディレクティブを記述する必要があり、**記載しないとエラーが発生**します。

これでビューの作成が完了しました。
ただし、このビューを表示するためには、**ルーティングを定義する必要があります**。