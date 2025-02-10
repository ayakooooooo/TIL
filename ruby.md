```
class PostsController < ApplicationController
  def index
    @posts = Post.all
  end
  
  # showアクションを追加してください
  def show
  end
end
```
「localhost:3000」にアクセスしたときにトップページが表示されるようにしてください。  
ルーティング
```
Rails.application.routes.draw do
  get "/" => "home#top"

  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
end
```
コントローラー
```
class HomeController < ApplicationController
  def top
  end
end
```
サービス紹介ページを追加しよう  
```
ルーティング
Rails.application.routes.draw do
  get "/" => "home#top"
  get "/about" => "home#about"
  # For details on the DSL available within this file, see http://guides.rubyonrails.org/routing.html
end
```
```
コントローラー
class HomeController < ApplicationController
  def top
  end
  def about
  end
end
```
```
ビュー
<div class="about-main">
  <h2>TweetAppとは</h2>
  <p>
    SNSサービスです。
    近況やつぶやきを投稿し、他のユーザーと楽しくコミュニケーションできます。
  </p>
  <img class="about-img" src="/tweets.png">
</div>
```
「localhost:3000」 (後ろに/○○がないURL) に対応するルーティングは、  
「get "/" => "コントローラ名#アクション名"」というように、URLに"/"を指定  
```
```
<header>
      <div class="header-logo">
        <%= link_to("TweetApp", "/") %>
      </div>
      <ul class="header-menus">
        <li>
          <%= link_to("TweetAppとは", "/about") %>
        </li>
      </ul>
    </header>
    
    <h1>Home#top</h1>
<p>Find me in app/views/home/top.html.erb</p>
<div class="main top-main">
  <div class="top-message">
    <h2>つぶやきで、世界はつながる</h2>
    <p>今の気持ちをつぶやいてみよう！</p>
  </div>
</div>
```
```
ビュー
<div class="main posts-show">
  <div class="container">
    <div class="posts-show-item">
      <p>
        <%= @post.content %>
      </p>
      <div class="post-time">
        <%= @post.created_at %>
      </div>
    </div>
  </div>
</div>
```
```
ルーティング
Rails.application.routes.draw do
  get "posts/index" => "posts#index"
  get "posts/:id" => "posts#show"

  get "/" => "home#top"
  get "about" => "home#about"
end
```
一覧にリンク
```
<div class="main posts-index">
  <div class="container">
    <% @posts.each do |post| %>
      <div class="posts-index-item">
         <%= link_to(post.content, "/posts/#{post.id}") %>
      </div>
    <% end %>
  </div>
</div>
```
```
コントローラー
class PostsController < ApplicationController
 def index
    @posts = Post.all.order(created_at: :desc)
  end
  def show            
   @post = Post.find_by(id: params[:id])            
 end
end
```
投稿詳細からの編集削除
```
Loading development environment (Rails 5.0.3)
[1] pry(main)> post = Post.find_by(id:2)
  Post Load (0.1ms)  SELECT  "posts".* FROM "posts" WHERE "posts"."id" = ? LIMIT ?  [["id", 2], ["LIMIT", 1]]
=> #<Post:0x00005585e6a43730
 id: 2,
 content: "今日のランチおいしかった。",
 created_at: Fri, 31 Mar 2017 14:24:32 JST +09:00,
 updated_at: Fri, 31 Mar 2017 14:24:32 JST +09:00>
[2] pry(main)> post.destroy
   (0.1ms)  begin transaction
  SQL (0.9ms)  DELETE FROM "posts" WHERE "posts"."id" = ?  [["id", 2]]
   (5.0ms)  commit transaction
=> #<Post:0x00005585e6a43730
 id: 2,
 content: "今日のランチおいしかった。",
 created_at: Fri, 31 Mar 2017 14:24:32 JST +09:00,
 updated_at: Fri, 31 Mar 2017 14:24:32 
 ```
```
<!DOCTYPE html>
<html>
  <head>
    <title>TweetApp</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <header>
      <div class="header-logo">
        <%= link_to("TweetApp", "/") %>
      </div>
      <ul class="header-menus">
        <li>
          <%= link_to("TweetAppとは", "/about") %>
        </li>
        <li>
          <%= link_to("投稿一覧", "/posts/index") %>
        </li>
        <li>
          <%= link_to("新規投稿", "/posts/new") %>
        </li>
        <li>
          <%= link_to("ユーザー一覧", "/users/index") %>
        </li>
        <!-- 新規登録ページへのリンクを作成してください -->
         <li>
          <%= link_to("新規登録", "/signup") %>
        </li>
        
      </ul>
    </header>

    <% if flash[:notice] %>
      <div class="flash">
        <%= flash[:notice] %>
      </div>
    <% end %>
    
    <%= yield %>
  </body>
</html>
```
```
class UsersController < ApplicationController
  
  def index
    @users = User.all
  end
  
  def show
    @user = User.find_by(id: params[:id])
  end
  
  def new
    @user = User.new
  end
  
  def create
    @user = User.new(
      name: params[:name],
      email: params[:email],
      image_name: "default_user.jpg"
    )
    if @user.save
      flash[:notice] = "ユーザー登録が完了しました"
      redirect_to("/users/#{@user.id}")
    else
      render("users/new")
    end
  end
  
  def edit
    @user = User.find_by(id: params[:id])
  end
  
  def update
    @user = User.find_by(id: params[:id])
    @user.name = params[:name]
    @user.email = params[:email]
    
    if params[:image]
      @user.image_name = "#{@user.id}.jpg"
      image = params[:image]
      File.binwrite("public/user_images/#{@user.image_name}", image.read)
    end
    
    if @user.save
      flash[:notice] = "ユーザー情報を編集しました"
      redirect_to("/users/#{@user.id}")
    else
      render("users/edit")
    end
  end
  
  def login_form
  end
  
  def login
    # 入力内容と一致するユーザーを取得し、変数@userに代入してください
     @user = User.find_by(email: params[:email],password: params[:password])
    # @userが存在するかどうかを判定するif文を作成してください
   if @user
      flash[:notice] = "ログインしました"
      redirect_to("/posts/index")
    else
      render("users/login_form")
    end
  end
  
end
```
```
<div class="main users-new">
  <div class="container">
    <div class="form-heading">ログイン</div>
    <div class="form users-form">
      <div class="form-body">
        <!-- 指定されたHTMLを貼り付けてください -->
        <% if @error_message %>
          <div class="form-error">
            <%= @error_message %>
          </div>
        <% end %>
        <%= form_tag("/login") do %>
          <p>メールアドレス</p>
          <!-- value属性を追加してください -->
          <input name="email" value="<%=@email%>">
          <p>パスワード</p>
          <!-- value属性を追加してください -->
          <input type="password" name="password" value="<%=@password%>">
          <input type="submit" value="ログイン">
        <% end %>
      </div>
    </div>
  </div>
</div>
```
```
class UsersController < ApplicationController
  # before_actionにauthenticate_userメソッドを指定してください
   before_action:authenticate_user,{only:[:index, :show, :edit, :update]}
  
  def index
    @users = User.all
  end
  
  def show
    @user = User.find_by(id: params[:id])
  end
  
  def new
    @user = User.new
  end
  
  def create
    @user = User.new(
      name: params[:name],
      email: params[:email],
      image_name: "default_user.jpg",
      password: params[:password]
    )
    if @user.save
      session[:user_id] = @user.id
      flash[:notice] = "ユーザー登録が完了しました"
      redirect_to("/users/#{@user.id}")
    else
      render("users/new")
    end
  end
  
  def edit
    @user = User.find_by(id: params[:id])
  end
  
  def update
    @user = User.find_by(id: params[:id])
    @user.name = params[:name]
    @user.email = params[:email]
    
    if params[:image]
      @user.image_name = "#{@user.id}.jpg"
      image = params[:image]
      File.binwrite("public/user_images/#{@user.image_name}", image.read)
    end
    
    if @user.save
      flash[:notice] = "ユーザー情報を編集しました"
      redirect_to("/users/#{@user.id}")
    else
      render("users/edit")
    end
  end
  
  def login_form
  end
  
  def login
    @user = User.find_by(email: params[:email], password: params[:password])
    if @user
      session[:user_id] = @user.id
      flash[:notice] = "ログインしました"
      redirect_to("/posts/index")
    else
      @error_message = "メールアドレスまたはパスワードが間違っています"
      @email = params[:email]
      @password = params[:password]
      render("users/login_form")
    end
  end
  
  def logout
    session[:user_id] = nil
    flash[:notice] = "ログアウトしました"
    redirect_to("/login")
  end
  
end

```
```
<div class="main user-show">
  <div class="container">
    <div class="user">
      <img src="<%= "/user_images/#{@user.image_name}" %>">
      <h2><%= @user.name %></h2>
      <p><%= @user.email %></p>
      <!-- @userのidとLog Inしているユーザーのidが等しい場合のみ、以下のリンクを表示してください -->
      <% if @user.id == @current_user.id %>
      <%= link_to("編集", "/users/#{@user.id}/edit") %>
    </div>
  </div>
</div>
```
```
class UsersController < ApplicationController
  before_action :authenticate_user, {only: [:index, :show, :edit, :update]}
  before_action :forbid_login_user, {only: [:new, :create, :login_form, :login]}
  # before_actionにensure_correct_userメソッドを指定してください
  before_action:ensure_correct_user, {only: [:edit, :update]}
  
  def index
    @users = User.all
  end
  
  def show
    @user = User.find_by(id: params[:id])
  end
  
  def new
    @user = User.new
  end
  
  def create
    @user = User.new(
      name: params[:name],
      email: params[:email],
      image_name: "default_user.jpg",
      password: params[:password]
    )
    if @user.save
      session[:user_id] = @user.id
      flash[:notice] = "ユーザー登録が完了しました"
      redirect_to("/users/#{@user.id}")
    else
      render("users/new")
    end
  end
  
  def edit
    @user = User.find_by(id: params[:id])
  end
  
  def update
    @user = User.find_by(id: params[:id])
    @user.name = params[:name]
    @user.email = params[:email]
    
    if params[:image]
      @user.image_name = "#{@user.id}.jpg"
      image = params[:image]
      File.binwrite("public/user_images/#{@user.image_name}", image.read)
    end
    
    if @user.save
      flash[:notice] = "ユーザー情報を編集しました"
      redirect_to("/users/#{@user.id}")
    else
      render("users/edit")
    end
  end
  
  def login_form
  end
  
  def login
    @user = User.find_by(email: params[:email], password: params[:password])
    if @user
      session[:user_id] = @user.id
      flash[:notice] = "ログインしました"
      redirect_to("/posts/index")
    else
      @error_message = "メールアドレスまたはパスワードが間違っています"
      @email = params[:email]
      @password = params[:password]
      render("users/login_form")
    end
  end
  
  def logout
    session[:user_id] = nil
    flash[:notice] = "ログアウトしました"
    redirect_to("/login")
  end
  
  # ensure_correct_userを定義してください
  def ensure_correct_user
   if @current_user.id != params[:id].to_i
    flash[:notice] = "権限がありません"
    redirect_to("/posts/index")
  end
end
  
end
```
```
<div class="main users-new">
  <div class="container">
    <div class="form-heading">ログイン</div>
    <div class="form users-form">
      <div class="form-body">
        <%= form_tag("/login") do %>            
                  <p>メールアドレス</p>            
                   <input name="email">            
                   <p>パスワード</p>            
                  <input type="password" name="password">            
                  <input type="submit" value="ログイン">            
                  <% end %>
      </div>
    </div>
  </div>
</div>
```
```
<div class="main users-new">
  <div class="container">
    <div class="form-heading">ログイン</div>
    <div class="form users-form">
      <div class="form-body">
        <% if @error_message %>            
            <div class="form-error">            
            <%= @error_message %>            
            </div>            
         <% end %>
        <%= form_tag("/login") do %>            
<p>メールアドレス</p>  
<input name="email" value="<%= @email %>">
<p>パスワード</p>
<input type="password" name="password" value="<%= @password %>">  
<input type="submit" value="ログイン">
<% end %>
      </div>
    </div>
  </div>
</div>
```
```
class UsersController < ApplicationController
  def index
    @users = User.all
  end
  
  def show
    @user = User.find_by(id: params[:id])
  end
  
  def new
    @user = User.new
  end
  
  def create
    @user = User.new(
      name: params[:name],
      email: params[:email],
      image_name: "default_user.jpg",
      password: params[:password]
      )
    if @user.save
      session[:user_id] = @user.id
      flash[:notice] = "ユーザー登録が完了しました"
      redirect_to("/users/#{@user.id}")
    else
      render("users/new")
    end
  end
  
  def edit
    @user = User.find_by(id: params[:id])
  end
  
  def update
    @user = User.find_by(id: params[:id])
    @user.name = params[:name]
    @user.email = params[:email]
    if params[:image]
             @user.image_name = "#{@user.id}.jpg"
             image = params[:image]
              File.binwrite("public/user_images/#{@user.image_name}", image.read)      
             end
    if @user.save
      flash[:notice] = "ユーザー情報を編集しました"
      redirect_to("/users/#{@user.id}")
    else
      render("users/edit")
    end
  end
 def login_form
 end
 
 def login         
 @user = User.find_by(email: params[:email], password: params[:password])
   if @user
  session[:user_id] = @user.id
   flash[:notice] = "ログインしました"
    redirect_to("/posts/index")
       else
         @error_message = "メールアドレスまたはパスワードが間違っています"
         @email = params[:email]
         @password = params[:password]
      render("users/login_form")
      end         
      end
end
```
```
<!DOCTYPE html>
<html>
  <head>
    <title>TweetApp</title>
    <%= csrf_meta_tags %>

    <%= stylesheet_link_tag    'application', media: 'all', 'data-turbolinks-track': 'reload' %>
    <%= javascript_include_tag 'application', 'data-turbolinks-track': 'reload' %>
  </head>

  <body>
    <header>
      <div class="header-logo">
        <%= link_to("TweetApp", "/") %>
      </div>
      <ul class="header-menus">
        <% if session[:user_id] %>       
            <li>       
            現在ログインしているユーザーのid:  
            <%= session[:user_id] %>     
            </li>       
      <%= link_to("投稿一覧", "/posts/index") %>        
       </li>    
       <li>  
        <%= link_to("新規投稿", "/posts/new") %>    
       </li>
       <li>
        <%= link_to("ユーザー一覧", "/users/index") %>       
       </li>     
        <li>       
        </li>         
   <% else %>            
  <li>
  <%= link_to("TweetAppとは", "/about") %>
 </li>
 <li>
  <%= link_to("新規登録", "/signup") %>     
  </li>
  <li>
  <%= link_to("ログイン", "/login") %>   
    </li>
    <% end %>
      </ul>
    </header>

    <% if flash[:notice] %>
      <div class="flash">
        <%= flash[:notice] %>
      </div>
    <% end %>
    
    <%= yield %>
  </body>
</html>
```
