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
      <!-- href属性を追加してください -->
      <a href="/" class="header-logo"  >LIST APP</a>
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
        <% const items = [
          {id: 1, name: 'じゃがいも'},
          {id: 2, name: 'にんじん'},
          {id: 3, name: 'たまねぎ'}
        ]; %>
        <ul class="table-body">
          <% items.forEach((item) => { %>
            <li>
              <span class="id-column"><%= item.id %></span>
              <span class="name-column"><%= item.name %></span>
            </li>
          <% }); %>
        </ul>
      </div>
    </div>
  </body>
</html>
```
```
const express = require('express');
// MySQLを使うためのコードを貼り付けてください
const mysql = require('mysql');

const app = express();

app.use(express.static('public'));
// 定数connectionを定義して接続情報の書かれたコードを代入してください
const connection=mysql.createConnection({
  host: 'localhost',
  user: 'progate',
  password: 'password',
  database: 'list_app'
});

app.get('/', (req, res) => {
  res.render('top.ejs');
});

app.get('/index', (req, res) => {
  res.render('index.ejs');
});

app.listen(3000);
```
```
const express = require('express');
const mysql = require('mysql');
const app = express();

app.use(express.static('public'));

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'progate',
  password: 'password',
  database: 'list_app'
});

app.get('/', (req, res) => {
  res.render('top.ejs');
});

app.get('/index', (req, res) => {
  // データベースからデータを取得する処理を書いてください
  connection.query('SELECT * FROM items
', (error,results)=>{console.log(results);
  res.render('index.ejs');
});
  
  // 下記のコードを削除してください

  // 削除ここまで
});

app.listen(3000);
```
```
const express = require('express');
const mysql = require('mysql');
const app = express();

app.use(express.static('public'));

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'progate',
  password: 'password',
  database: 'list_app'
});

app.get('/', (req, res) => {
  res.render('top.ejs');
});

app.get('/index', (req, res) => {
  connection.query(
    'SELECT * FROM items',
    (error, results) => {
      // res.renderの第２引数にオブジェクトを追加してください
      res.render('index.ejs',{items:results});
    }
  );
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
      <a href="/" class="header-logo">LIST APP</a>
    </header>
    <div class="container">
      <div class="container-header">
        <h1>買い物リスト</h1>
        <!-- 作成画面へのリンクを追加してください -->
        <a href="/new" class="new-button">+ 新規作成</a>
        
      </div>
      <div class="index-table-wrapper">
        <div class="table-head">
          <span class="id-column">ID</span>
          <span>買うもの</span>
        </div>
        <ul class="table-body">
          <% items.forEach((item) => { %>
            <li>
              <div class="item-data">
                <span class="id-column"><%= item.id %></span>
                <span class="name-column"><%= item.name %></span>
              </div>
            </li>
          <% }) %>
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
      <a href="/" class="header-logo">LIST APP</a>
    </header>
    <div class="container">
      <div class="container-header">
        <h1>買い物リスト作成</h1>
      </div>
      <div class="item-form-wrapper">
        <p class="form-label">買うもの</p>
        <!-- formタグを追加してください -->
        <form action="/create" method="post">
          <input type="text">
          <input type="submit" value="作成する">
        <!-- formタグの閉じタグを書いてください -->
        </form>
      </div>
      <a href="/index" class="cancel-button">もどる</a>
    </div>
  </body>
</html>
```
```
const express = require('express');
const mysql = require('mysql');
const app = express();

app.use(express.static('public'));
// フォームから送信された値を受け取れるようにしてください
app.use(express.urlencoded({extended: false}));

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'progate',
  password: 'password',
  database: 'list_app'
});

app.get('/', (req, res) => {
  res.render('top.ejs');
});

app.get('/index', (req, res) => {
  connection.query(
    'SELECT * FROM items',
    (error, results) => {
      res.render('index.ejs', {items: results});
    }
  );
});

app.get('/new', (req, res) => {
  res.render('new.ejs');
});

app.post('/create', (req, res) => {
  // フォームから送信された値を出力してください
  console.log(req.body.itemName);
  
  connection.query(
    'SELECT * FROM items',
    (error, results) => {
      res.render('index.ejs', {items: results});
    }
  );
});

app.listen(3000);
```
```
const express = require('express');
const mysql = require('mysql');
const app = express();

app.use(express.static('public'));
app.use(express.urlencoded({extended: false}));

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'progate',
  password: 'password',
  database: 'list_app'
});

app.get('/', (req, res) => {
  res.render('top.ejs');
});

app.get('/index', (req, res) => {
  connection.query(
    'SELECT * FROM items',
    (error, results) => {
      res.render('index.ejs', {items: results});
    }
  );
});

app.get('/new', (req, res) => {
  res.render('new.ejs');
});

app.post('/create', (req, res) => {
  // データベースに追加する処理を書いてください
  connection.query(
  'INSERT INTO items (name) VALUES (?)',
  [req.body.itemName],
  (error,results)=>{
    connection.query(
        'SELECT * FROM items',
        (error, results) => {
          res.render('index.ejs', {items: results});
        }
      );
  });
  // 以下の一覧画面表示の処理を削除してください

  // ここまで削除してください
});

app.listen(3000);
```
```
const express = require('express');
const mysql = require('mysql');
const app = express();

app.use(express.static('public'));
app.use(express.urlencoded({extended: false}));

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'progate',
  password: 'password',
  database: 'list_app'
});

app.get('/', (req, res) => {
  res.render('top.ejs');
});

app.get('/index', (req, res) => {
  connection.query(
    'SELECT * FROM items',
    (error, results) => {
      res.render('index.ejs', {items: results});
    }
  );
});

app.get('/new', (req, res) => {
  res.render('new.ejs');
});

app.post('/create', (req, res) => {
  connection.query(
    'INSERT INTO items (name) VALUES (?)',
    [req.body.itemName],
    (error, results) => {
      res.redirect('/index');
    }
  );
});

// ルーティングにルートパラメータを指定してください
app.post('/delete/:id', (req, res) => {
  // ルートパラメータで受け取った値を出力してください
  console.log(req.params.id);
  
  res.redirect('/index');
});

app.listen(3000);
```
```
const express = require('express');
const mysql = require('mysql');
const app = express();

app.use(express.static('public'));
app.use(express.urlencoded({extended: false}));

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'progate',
  password: 'password',
  database: 'list_app'
});

app.get('/', (req, res) => {
  res.render('top.ejs');
});

app.get('/index', (req, res) => {
  connection.query(
    'SELECT * FROM items',
    (error, results) => {
      res.render('index.ejs', {items: results});
    }
  );
});

app.get('/new', (req, res) => {
  res.render('new.ejs');
});

app.post('/create', (req, res) => {
  connection.query(
    'INSERT INTO items (name) VALUES (?)',
    [req.body.itemName],
    (error, results) => {
      res.redirect('/index');
    }
  );
});

app.post('/delete/:id', (req, res) => {
  // データベースのデータを削除する処理を書いてください
  connection.query(
    'DELETE FROM items WHERE id=?',
    [req.params.id],
    (error, results) => {
      res.redirect('/index');
    }
  // 下記のコードを削除してください
);
});

app.listen(3000);
```
```
const express = require('express');
const mysql = require('mysql');
const app = express();

app.use(express.static('public'));
app.use(express.urlencoded({extended: false}));

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'progate',
  password: 'password',
  database: 'list_app'
});

app.get('/', (req, res) => {
  res.render('top.ejs');
});

app.get('/index', (req, res) => {
  connection.query(
    'SELECT * FROM items',
    (error, results) => {
      res.render('index.ejs', {items: results});
    }
  );
});

app.get('/new', (req, res) => {
  res.render('new.ejs');
});

app.post('/create', (req, res) => {
  connection.query(
    'INSERT INTO items (name) VALUES (?)',
    [req.body.itemName],
    (error, results) => {
      res.redirect('/index');
    }
  );
});

app.post('/delete/:id', (req, res) => {
  connection.query(
    'DELETE FROM items WHERE id = ?',
    [req.params.id],
    (error, results) => {
      res.redirect('/index');
    }
  );
});

// 編集画面を表示するルーティングを作成してください
app.get('/edit/:id', (req, res) => {
res.render('edit.ejs');
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
      <a href="/" class="header-logo">LIST APP</a>
    </header>
    <div class="container">
      <div class="container-header">
        <h1>買い物リスト編集</h1>
      </div>
      <div class="item-form-wrapper">
        <p class="form-label">買うもの</p>
        <!-- フォームの送信先とメソッドを指定してください -->
        <form action ="/update/<%=item.id%>" method="post">
          <!-- name属性を指定してください -->
          <input type="text" name="itemName"  value="<%= item.name %>">
          <input type="submit" value="更新する">
        </form>
      </div>
      <a href="/index" class="cancel-button"></span>もどる</a>
    </div>
  </body>
</html>
```
```
const express = require('express');
const mysql = require('mysql');
const app = express();

app.use(express.static('public'));
app.use(express.urlencoded({extended: false}));

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'progate',
  password: 'password',
  database: 'list_app'
});

app.get('/', (req, res) => {
  res.render('top.ejs');
});

app.get('/index', (req, res) => {
  connection.query(
    'SELECT * FROM items',
    (error, results) => {
      res.render('index.ejs', {items: results});
    }
  );
});

app.get('/new', (req, res) => {
  res.render('new.ejs');
});

app.post('/create', (req, res) => {
  connection.query(
    'INSERT INTO items (name) VALUES (?)',
    [req.body.itemName],
    (error, results) => {
      res.redirect('/index');
    }
  );
});

app.post('/delete/:id', (req, res) => {
  connection.query(
    'DELETE FROM items WHERE id = ?',
    [req.params.id],
    (error, results) => {
      res.redirect('/index');
    }
  );
});

app.get('/edit/:id', (req, res) => {
  connection.query(
    'SELECT * FROM items WHERE id = ?',
    [req.params.id],
    (error, results) => {
      res.render('edit.ejs', {item: results[0]});
    }
  );
});

app.post('/update/:id', (req, res) => {
  // 選択されたメモを更新する処理を書いてください
  connection.query(
    'UPDATE items SET name = ? WHERE id = ?',
  // 以下の一覧画面へリダイレクトする処理を削除してください
  [req.body.itemName,req.params.id],
  (error, results) => {
  res.redirect('/index');
  }
  );
});

app.listen(3000);
```
```
const express = require('express');
const mysql = require('mysql');
const app = express();

app.use(express.static('public'));
app.use(express.urlencoded({extended: false}));

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'progate',
  password: 'password',
  database: 'blog'
});

app.get('/', (req, res) => {
  res.render('top.ejs');
});

app.get('/list', (req, res) => {
  connection.query(
    'SELECT * FROM articles',
    (error, results) => {
      res.render('list.ejs', { articles: results });
    }
  );
});

app.get('/article/:id', (req, res) => {
  const id = req.params.id;
  connection.query(
    'SELECT * FROM articles WHERE id = ?',
    [id],
    (error, results) => {
      res.render('article.ejs', { article: results[0] });
    }
  );
});

app.get('/login', (req, res) => {
  res.render('login.ejs');
});

app.post('/login', (req, res) => {
  // フォームから送信されたメールアドレスを定数emailに代入してください
  const email = req.body.email;
  
  //ユーザー情報を取得するコードを貼り付けてください
  connection.query(
    'SELECT * FROM users WHERE email = ?',
    [email],
    (error, results) => {
      // 配列resultsの要素数で処理の分岐をしてください
      if (results.length > 0) {
        if (req.body.password === results[0].password){
          console.log('認証に成功しました');
          res.redirect('/list');
        } else {
          console.log('認証に失敗しました');
          res.redirect('/login');
        }
    } else {
      res.redirect('/login');
    }
    }
  );
});

app.listen(3000);
```
```
<header>
  <div class="header-nav">
    <a href="/">BLOG</a>
    <p>ようこそ、<%= locals.username %>さん</p>
    <ul>
      <li><a href="/list">記事一覧</a></li>
      <!-- locals.isLoggedInを用いて表示するリンクを切り替えてください-->
      <% if (locals.isLoggedIn){%>
      <li><a href="/logout">ログアウト</a></li>
      <% } else { %>
      <li><a href="/login">ログイン</a></li>
      <% } %>
    </ul>
  </div>
  <p>わんこの学びブログ</p>
</header>
```
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>BLOG</title>
    <link rel="stylesheet" href="/css/style.css">
    <script src="/send_url.js"></script>
  </head>
  <body>
    <%- include('header'); %>
    <main>
      <div class="article">
        <% if (article.category === 'all') { %>
          <h1><%= article.title %></h1>
          <p><%= article.content %></p>
        <% } %>
        <% if (article.category === 'limited') { %>
          <i>会員限定</i>
          <h1><%= article.title %></h1>
          <!-- ここから削除 -->
          <p><%= article.content %></p>
          <!-- ここまで -->
                    
          
          
        <% } %>
      </div>
    </main>
    <footer>
      <a class="btn sub" href="/list">一覧にもどる</a>
    </footer>
  </body>
</html>
```
```
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>BLOG</title>
    <link rel="stylesheet" href="/css/style.css">
    <script src="/send_url.js"></script>
  </head>
  <body>
    <%- include('header'); %>
    <main>
      <div class="article">
        <% if (article.category === 'all') { %>
          <h1><%= article.title %></h1>
          <p><%= article.content %></p>
        <% } %>
        <% if (article.category === 'limited') { %>
          <i>会員限定</i>
          <h1><%= article.title %></h1>
          <!-- ここから削除 -->
          <!-- ここまで -->
          
          <!-- locals.isLoggedInを条件式とする条件分岐を作成してください -->
          <% if (locals.isLoggedIn) { %>
          <p><%= article.content %></p>
          
        <% } else { %>
        <div class="article-login">
              <p>今すぐログインしよう！</p>
              <p>記事の続きは<br>ログインすると読むことができます</p>
              <img src="/images/login.svg">
              <a class="btn" href="/login">ログイン</a>
            </div>
        <% }   %>
         <% }   %>
      </div>
    </main>
    <footer>
      <a class="btn sub" href="/list">一覧にもどる</a>
    </footer>
  </body>
</html>
```
```
const express = require('express');
const mysql = require('mysql');
const session = require('express-session');
const app = express();

app.use(express.static('public'));
app.use(express.urlencoded({extended: false}));

const connection = mysql.createConnection({
  host: 'localhost',
  user: 'progate',
  password: 'password',	
  database: 'blog'
});

app.use(
  session({
    secret: 'my_secret_key',
    resave: false,
    saveUninitialized: false,
  })
);

app.use((req, res, next) => {
  if (req.session.userId === undefined) {
    res.locals.username = 'ゲスト';
    res.locals.isLoggedIn = false;
  } else {
    res.locals.username = req.session.username;
    res.locals.isLoggedIn = true;
  }
  next();
});

app.get('/', (req, res) => {
  res.render('top.ejs');
});

app.get('/list', (req, res) => {
  connection.query(
    'SELECT * FROM articles',
    (error, results) => {
      res.render('list.ejs', { articles: results });
    }
  );
});

app.get('/article/:id', (req, res) => {
  const id = req.params.id;
  connection.query(
    'SELECT * FROM articles WHERE id = ?',
    [id],
    (error, results) => {
      res.render('article.ejs', { article: results[0] });
    }
  );
});

// 作成画面を表示するルーティングを作成してください
app.get('/signup', (req, res) => {
  res.render('signup.ejs');
});

app.get('/login', (req, res) => {
  res.render('login.ejs');
});

app.post('/login', (req, res) => {
  const email = req.body.email;
  connection.query(
    'SELECT * FROM users WHERE email = ?',
    [email],
    (error, results) => {
      if (results.length > 0) {
        if (req.body.password === results[0].password){
          req.session.userId = results[0].id;
          req.session.username = results[0].username;
          res.redirect('/list');
        } else {
          res.redirect('/login');
        }    
      } else {
        res.redirect('/login');
      }
    }
  );
});

app.get('/logout', (req, res) => {
  req.session.destroy((error) => {
    res.redirect('/list');
  });
});

app.listen(3000);
```
