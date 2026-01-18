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
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>LIST APP</title>
    <link rel="stylesheet" href="/css/style.css">
    <script src="/send_url.js"></script>
  </head>
  <body>
    <header>
      <a class="header-logo">LIST APP</a>
    </header>
    <div class="container">
      <div class="container-header">
        <h1>買い物リスト</h1>
      </div>
      <div class="index-table-wrapper">
        <div class="table-head">
          <span class="id-column">ID</span>
          <span>買うもの</span>
        </div>
        <!-- EJSを用いてitemを定義してください -->
        <% const item = {id: 4, name: 'とまと'} %>
        
        <ul class="table-body">
          <li>
            <span class="id-column">1</span>
            <span class="name-column">じゃがいも</span>
          </li>
          <li>
            <span class="id-column">2</span>
            <span class="name-column">にんじん</span>
          </li>
          <li>
            <span class="id-column">3</span>
            <span class="name-column">たまねぎ</span>
          </li>
          <li>
            <span class="id-column">
              <!-- itemのidプロパティの値を表示してください -->
              <%=item.id %>
              
            </span>
            <span class="name-column">
              <!-- itemのnameプロパティの値を表示してください -->
              <%=item.name %>
              
            </span>
          </li>
        </ul>
      </div>
    </div>
  </body>
</html>
```
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>LIST APP</title>
    <link rel="stylesheet" href="/css/style.css">
    <script src="/send_url.js"></script>
  </head>
  <body>
    <header>
      <a class="header-logo">LIST APP</a>
    </header>
    <div class="container">
      <div class="container-header">
        <h1>買い物リスト</h1>
      </div>
      <div class="index-table-wrapper">
        <div class="table-head">
          <span class="id-column">ID</span>
          <span>買うもの</span>
        </div>
        <!-- 配列itemsを定義してください -->
        <% const items=[
          {id: 1, name: 'じゃがいも'},
          {id: 2, name: 'にんじん'},
          {id: 3, name: 'たまねぎ'}
        ];%>
        
        <ul class="table-body">
          <!-- 以下の3つの<li>要素を削除してください -->
          
          <!-- 削除ここまで -->
          
          <!-- forEachを用いてitemsの要素を出力してください -->
          <% items.forEach((item) => { %>
<li>
              <span class="id-column">
                <!-- itemのidプロパティの値を表示してください -->
                <%=item.id %>
                
              </span>
              <span class="name-column">
                <!-- itemのnameプロパティの値を表示してください -->
                <%=item.name %>
                
              </span>
            </li>
<% }); %>

          
        </ul>
      </div>
    </div>
  </body>
</html>
```
