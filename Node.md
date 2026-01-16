Node.jsはJavaScriptを使ってサーバーサイド開発を行えるように設計された実行環境  
list-app $ npm install express  
```
const express = require('express');
const app = express();

app.get('/', (req, res) => {
  res.render('hello.ejs');
});

// トップ画面を表示するルーティングを作成してください
app.get('/top', (req, res) => {
  res.render('top.ejs');
});


app.listen(3000);
```
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>LIST APP</title>
    <!-- CSSファイルを読み込んでください -->
    <link rel="stylesheet" href="/css/style.css">
    
    <script src="/send_url.js"></script>
  </head>
  <body>
    <div class="top-wrapper">
      <div class="top-detail">
        <h2 class="subtitle">買い物リストアプリ</h2>
        <h1 class="title">LIST APP</h1>
        <p class="description">
          LIST APPは、買い物をリストアップするサービスです。
          <br>
          買いたいものをリストに追加してみましょう。
        </p>
        <a class="index-button">一覧を見る</a>
      </div>
      <div class="top-image">
        <!-- 画像ファイルを読み込んでください -->
        <img src="/images/top.png">
        
      </div>
    </div>
  </body>
</html>
```
```
const express = require('express');
const app = express();

app.use(express.static('public'));

app.get('/', (req, res) => {
  res.render('hello.ejs');
});

app.get('/top', (req, res) => {
  res.render('top.ejs');
});

// 一覧画面を表示するルーティングを作成してください
app.get('/index', (req, res) => {
  res.render('index.ejs');
});

app.listen(3000);
```
