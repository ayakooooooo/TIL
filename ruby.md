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
        <!-- 現在ログイン中のユーザーを取得し、変数current_userに代入してください -->
        <% current_user = User.find_by(id: session[:user_id]) %>
        
        <!-- if文の条件を書き換えてください -->
        <% if current_user %>
          <li>
            <!-- 以下の「現在しているユーザーのid:」を削除してください -->
            
            <!-- Log In中のユーザーの名前を表示し、詳細ページのリンクとなるように書き換えてください -->
            <%= link_to(current_user.name, "/users/#{current_user.id}") %>
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
          <li>
            <%= link_to("ログアウト", "/logout", {method: "post"}) %>
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
```
class ApplicationController < ActionController::Base
before_action :set_current_user
   def set_current_user
   @current_user = User.find_by(id: session[:user_id])
   end
   def authenticate_user
     if @current_user == nil
       flash[:notice] = "ログインが必要です"
       redirect_to("/login")
      end
    end
    def forbid_login_user
    if @current_user 
      flash[:notice] = "すでにログインしています"
      redirect_to("/posts/index")
    end
  end
end
```
```
class UsersController < ApplicationController
  before_action :authenticate_user, {only: [:index, :show, :edit, :update]}
  before_action :forbid_login_user, {only: [:new, :create, :login_form, :login]}
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
def ensure_correct_user
   if @current_user.id != params[:id].to_i
    flash[:notice] = "権限がありません"
    redirect_to("/posts/index")
  end
end
end
```
```
class PostsController < ApplicationController
  before_action :authenticate_user
  
  def index
    @posts = Post.all.order(created_at: :desc)
  end
  
  def show
    @post = Post.find_by(id: params[:id])
  end
  
  def new
    @post = Post.new
  end
  
  def create
    @post = Post.new(
      content: params[:content],
      # user_idの値をログインしているユーザーのidにしてください
      user_id: @current_user.id
    )
    if @post.save
      flash[:notice] = "投稿を作成しました"
      redirect_to("/posts/index")
    else
      render("posts/new")
    end
  end
  
  def edit
    @post = Post.find_by(id: params[:id])
  end
  
  def update
    @post = Post.find_by(id: params[:id])
    @post.content = params[:content]
    if @post.save
      flash[:notice] = "投稿を編集しました"
      redirect_to("/posts/index")
    else
      render("posts/edit")
    end
  end
  
  def destroy
    @post = Post.find_by(id: params[:id])
    @post.destroy
    flash[:notice] = "投稿を削除しました"
    redirect_to("/posts/index")
  end
  
end
```
```
<div class="main posts-show">
  <div class="container">
    <div class="posts-show-item">
      <!--指定されたコードを貼り付けてください-->
      <div class="post-user-name">
        <!-- ユーザーの画像が表示されるように、以下のsrcの中を埋めてください -->
        <img src="<%= "/user_images/#{@user.image_name}" %>">
        
        <!-- link_toメソッドを用いて、ユーザー詳細ページへのリンクを作成してください -->
        <%=link_to(@user.name,"/users/#{@user.id}")%>
      </div>
      
      <p>
        <%= @post.content %>
      </p>
      <div class="post-time">
        <%= @post.created_at %>
      </div>
      <div class="post-menus">
        <%= link_to("編集", "/posts/#{@post.id}/edit") %>
        <%= link_to("削除", "/posts/#{@post.id}/destroy", {method: "post"}) %>
      </div>
    </div>
  </div>
</div>
```
```
class Post < ApplicationRecord
  validates :content, {presence: true, length: {maximum: 140}}
  validates :user_id, {presence: true}
  
  # インスタンスメソッドuserを定義してください
  def user
  return User.find_by(id:self.user_id)
  end
  
end
```
```
class PostsController < ApplicationController
  before_action :authenticate_user
  
  def index
    @posts = Post.all.order(created_at: :desc)
  end
  
  def show
    @post = Post.find_by(id: params[:id])
    @user = @post.user
  end
  
  def new
    @post = Post.new
  end
  
  def create
    @post = Post.new(
      content: params[:content],
      user_id: @current_user.id
    )
    if @post.save
      flash[:notice] = "投稿を作成しました"
      redirect_to("/posts/index")
    else
      render("posts/new")
    end
  end
  
  def edit
    @post = Post.find_by(id: params[:id])
  end
  
  def update
    @post = Post.find_by(id: params[:id])
    @post.content = params[:content]
    if @post.save
      flash[:notice] = "投稿を編集しました"
      redirect_to("/posts/index")
    else
      render("posts/edit")
    end
  end
  
  def destroy
    @post = Post.find_by(id: params[:id])
    @post.destroy
    flash[:notice] = "投稿を削除しました"
    redirect_to("/posts/index")
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
      <% if @user.id == @current_user.id %>
        <%= link_to("編集", "/users/#{@user.id}/edit") %>
      <% end %>
    </div>
    <!-- 以下の<% @user.posts.each do |post|%>を使ってeach文を追加してください -->
    <% %>
      <!-- 指定されたコードを貼り付けてください -->
       <div class="posts-index-item">
        <div class="post-left">
          <img src="<%= "/user_images/#{post.user.image_name}" %>">
        </div>
        <div class="post-right">
          <div class="post-user-name">
            <%= link_to(post.user.name, "/users/#{post.user.id}") %>
          </div>
          <%= link_to(post.content, "/posts/#{post.id}") %>
        </div>
      </div>
    <!-- 以下の<% %>を使ってeach文のendを追加してください -->
    <% end %>
  </div>
</div>
```
```
<div class="main posts-show">
  <div class="container">
    <div class="posts-show-item">
      <div class="post-user-name">
        <img src="<%= "/user_images/#{@user.image_name}" %>">
        <%= link_to(@user.name, "/users/#{@user.id}") %>
      </div>
      <p>
        <%= @post.content %>
      </p>
      <div class="post-time">
        <%= @post.created_at %>
      </div>
      <!-- 以下の<% %>を使ってif文を追加してください -->
      <% if @post.user_id == @current_user.id %>
        <div class="post-menus">
          <%= link_to("編集", "/posts/#{@post.id}/edit") %>
          <%= link_to("削除", "/posts/#{@post.id}/destroy", {method: "post"}) %>
        </div>
      <!-- 以下の<% %>を使ってif文のendを追加してください -->
      <% end %>
    </div>
  </div>
</div>
```
```
class PostsController < ApplicationController
  before_action :authenticate_user
  # before_actionでensure_correct_userメソッドを指定してください
  
  
  def index
    @posts = Post.all.order(created_at: :desc)
  end
  
  def show
    @post = Post.find_by(id: params[:id])
    @user = @post.user
  end
  
  def new
    @post = Post.new
  end
  
  def create
    @post = Post.new(
      content: params[:content],
      user_id: @current_user.id
    )
    if @post.save
      flash[:notice] = "投稿を作成しました"
      redirect_to("/posts/index")
    else
      render("posts/new")
    end
  end
  
  def edit
    @post = Post.find_by(id: params[:id])
  end
  
  def update
    @post = Post.find_by(id: params[:id])
    @post.content = params[:content]
    if @post.save
      flash[:notice] = "投稿を編集しました"
      redirect_to("/posts/index")
    else
      render("posts/edit")
    end
  end
  
  def destroy
    @post = Post.find_by(id: params[:id])
    @post.destroy
    flash[:notice] = "投稿を削除しました"
    redirect_to("/posts/index")
  end
  
  # ensure_correct_userメソッドを定義してください
  def ensure_correct_user
  @pos = Post.find_by(id: params[:id])
  flash[:notice] = "権限がありません"
      redirect_to("/posts/index")
end
 ```
class Like < ApplicationRecord
  validates:user_id,{presence:ture}
  validates:post_id,{presence:ture}
end
``` 
  
end
```
```
<div class="main posts-show">
  <div class="container">
    <div class="posts-show-item">
      <div class="post-user-name">
        <img src="<%= "/user_images/#{@user.image_name}" %>">
        <%= link_to(@user.name, "/users/#{@user.id}") %>
      </div>
      <p>
        <%= @post.content %>
      </p>
      <div class="post-time">
        <%= @post.created_at %>
      </div>
      <!-- if文を用いて、表示内容を切り替えてください -->
       <% if Like.find_by (user_id :@current_user.id,post_id :@post_id%>
       いいね！済み
       <% else %>
       いいね！していません
       <% end %>
      
      
      <% if @post.user_id == @current_user.id %>
        <div class="post-menus">
          <%= link_to("編集", "/posts/#{@post.id}/edit") %>
          <%= link_to("削除", "/posts/#{@post.id}/destroy", {method: "post"}) %>
        </div>
      <% end %>
    </div>
  </div>
</div>
```
```
Rails.application.routes.draw do
  # createアクションに対応するルーティングを追加してください
  post "likes/:post_id/create"=> "likes#update"
  
  post "users/:id/update" => "users#update"
  get "users/:id/edit" => "users#edit"
  post "users/create" => "users#create"
  get "signup" => "users#new"
  get "users/index" => "users#index"
  get "users/:id" => "users#show"
  post "login" => "users#login"
  post "logout" => "users#logout"
  get "login" => "users#login_form"

  get "posts/index" => "posts#index"
  get "posts/new" => "posts#new"
  get "posts/:id" => "posts#show"
  post "posts/create" => "posts#create"
  get "posts/:id/edit" => "posts#edit"
  post "posts/:id/update" => "posts#update"
  post "posts/:id/destroy" => "posts#destroy"
  
  get "/" => "home#top"
  get "about" => "home#about"
end
```
```
class LikesController < ApplicationController
  before_action :authenticate_user

  def create
    # 変数@likeを定義してください
    @like=Like.new(
      user_id: @current_user.id,
      post_id: params[:post_id])
    
    # 変数@likeを保存してください
    @like.save
    
    # 投稿詳細ページにリダイレクトしてください
    redirect_to("/posts/#{params[:post_id]}")
  
  end
end
```
```
Rails.application.routes.draw do
  post "likes/:post_id/create" => "likes#create"
  # destroyアクションに対応するルーティングを追加してください
  post "likes/:post_id/destroy" => "likes#destroy" 

  post "users/:id/update" => "users#update"
  get "users/:id/edit" => "users#edit"
  post "users/create" => "users#create"
  get "signup" => "users#new"
  get "users/index" => "users#index"
  get "users/:id" => "users#show"
  post "login" => "users#login"
  post "logout" => "users#logout"
  get "login" => "users#login_form"

  get "posts/index" => "posts#index"
  get "posts/new" => "posts#new"
  get "posts/:id" => "posts#show"
  post "posts/create" => "posts#create"
  get "posts/:id/edit" => "posts#edit"
  post "posts/:id/update" => "posts#update"
  post "posts/:id/destroy" => "posts#destroy"

  get "/" => "home#top"
  get "about" => "home#about"
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
    
    <!-- FontAwesomeを読み込むlinkタグを追加してください -->
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/font-awesome/4.7.0/css/font-awesome.min.css">
    
  </head>

  <body>
    <header>
      <div class="header-logo">
        <% if @current_user %>
          <%= link_to("TweetApp", "/posts/index") %>
        <% else %>
          <%= link_to("TweetApp", "/") %>
        <% end %>
      </div>
      <ul class="header-menus">
        <% if @current_user %>
          <li>
            <%= link_to(@current_user.name, "/users/#{@current_user.id}") %>
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
          <li>
            <%= link_to("ログアウト", "/logout", {method: "post"}) %>
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
```
<div class="main posts-show">
  <div class="container">
    <div class="posts-show-item">
      <div class="post-user-name">
        <img src="<%= "/user_images/#{@user.image_name}" %>">
        <%= link_to(@user.name, "/users/#{@user.id}") %>
      </div>
      <p>
        <%= @post.content %>
      </p>
      <div class="post-time">
        <%= @post.created_at %>
      </div>
      <% if Like.find_by(user_id: @current_user.id, post_id: @post.id) %>
        <!-- アイコンが表示できるように、以下のlink_toメソッドを書き換えてください -->
        <%= link_to("/likes/#{@post.id}/destroy", {method: "post"}) do %>            
<span class="fa fa-heart liked-btn"></span>            
 <% end %>            
 <% else %>            
   <!-- アイコンが表示できるように、以下のlink_toメソッドを書き換えてください -->            
<%= link_to("/likes/#{@post.id}/create", {method: "post"}) do %>            
 <span class="fa fa-heart unliked-btn"></span>            
 <% end %>
        
        
      <% end %>
      <% if @post.user_id == @current_user.id %>
        <div class="post-menus">
          <%= link_to("編集", "/posts/#{@post.id}/edit") %>
          <%= link_to("削除", "/posts/#{@post.id}/destroy", {method: "post"}) %>
        </div>
      <% end %>
    </div>
  </div>
</div>
```
```
class PostsController < ApplicationController
  before_action :authenticate_user
  before_action :ensure_correct_user, {only: [:edit, :update, :destroy]}
  
  def index
    @posts = Post.all.order(created_at: :desc)
  end
  
  def show
    @post = Post.find_by(id: params[:id])
    @user = @post.user
    # 変数@likes_countを定義してください
    @likes_count = Like.where(post_id: @post.id).count
  end
  
  def new
    @post = Post.new
  end
  
  def create
    @post = Post.new(
      content: params[:content],
      user_id: @current_user.id
    )
    if @post.save
      flash[:notice] = "投稿を作成しました"
      redirect_to("/posts/index")
    else
      render("posts/new")
    end
  end
  
  def edit
    @post = Post.find_by(id: params[:id])
  end
  
  def update
    @post = Post.find_by(id: params[:id])
    @post.content = params[:content]
    if @post.save
      flash[:notice] = "投稿を編集しました"
      redirect_to("/posts/index")
    else
      render("posts/edit")
    end
  end
  
  def destroy
    @post = Post.find_by(id: params[:id])
    @post.destroy
    flash[:notice] = "投稿を削除しました"
    redirect_to("/posts/index")
  end
  
  def ensure_correct_user
    @post = Post.find_by(id: params[:id])
    if @post.user_id != @current_user.id
      flash[:notice] = "権限がありません"
      redirect_to("/posts/index")
    end
  end
  
end
```
```
Rails.application.routes.draw do
  post "likes/:post_id/create" => "likes#create"
  post "likes/:post_id/destroy" => "likes#destroy"

  post "users/:id/update" => "users#update"
  get "users/:id/edit" => "users#edit"
  post "users/create" => "users#create"
  get "signup" => "users#new"
  get "users/index" => "users#index"
  get "users/:id" => "users#show"
  post "login" => "users#login"
  post "logout" => "users#logout"
  get "login" => "users#login_form"
  # "users/:id/likes"に対応するルーティングを追加してください
  get "users/:id/likes" => "users#likes"

  get "posts/index" => "posts#index"
  get "posts/new" => "posts#new"
  get "posts/:id" => "posts#show"
  post "posts/create" => "posts#create"
  get "posts/:id/edit" => "posts#edit"
  post "posts/:id/update" => "posts#update"
  post "posts/:id/destroy" => "posts#destroy"

  get "/" => "home#top"
  get "about" => "home#about"
end
```
```
Param.substring(1) で、最初の & を削除が必要な理由  


 エラーを防ぐため → 一部のサーバーやAPIが処理できない可能性がある  
 SEOやキャッシュの最適化のため → URLの一貫性を保つ  
コードの可読性とメンテナンス性の向上 → 開発者が見て理解しやすい  

そのため、最初の & を削除し、正しい形式にするのがベストプラクティス！   
```
```
class User < ApplicationRecord
  # has_secure_passwordメソッドを追加してください
  has_secure_password
  
  validates :name, {presence: true}
  validates :email, {presence: true, uniqueness: true}
  # 以下のバリデーションを削除してください
 
  
  def posts
    return Post.where(user_id: self.id)
  end
  
end
```
```
class ChangeUsersColumns < ActiveRecord::Migration[5.0]
  def change
    add_column :users, :password_digest, :string
    remove_column :users, :password, :string
  end
end
```
```
class UsersController < ApplicationController
  before_action :authenticate_user, {only: [:index, :show, :edit, :update]}
  before_action :forbid_login_user, {only: [:new, :create, :login_form, :login]}
  before_action :ensure_correct_user, {only: [:edit, :update]}
  
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
    # メールアドレスのみを用いて、ユーザーを取得するように書き換えてください
    @user = User.find_by(email: params[:email])
    # if文の条件を&&とauthenticateメソッドを用いて書き換えてください
    if @user && @user.authenticate(params[:password])
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
  
  def likes
    @user = User.find_by(id: params[:id])
    @likes = Like.where(user_id: @user.id)
  end
  
  def ensure_correct_user
    if @current_user.id != params[:id].to_i
      flash[:notice] = "権限がありません"
      redirect_to("/posts/index")
    end
  end
  
end
```
```
class Post < ApplicationRecord
  validates :content, {presence: true, length: {maximum: 140}}
  validates :user_id, {presence: true}            
 def user            
 return User.find_by(id: self.user_id)            
end
   validates :user_id, {presence: true}
end
```
```
<div class="main posts-index">
  <div class="container">
    <% @posts.each do |post| %>
      <div class="posts-index-item">
        <div class="post-left">
          <img src="<%= "/user_images/#{post.user.image_name}" %>">
        </div>
        <div class="post-right">
          <div class="post-user-name">
            <%= link_to( post.user.name, "/users/#{post.user.id}" ) %>
          </div>
          <%= link_to(post.content, "/posts/#{post.id}") %>
        </div>
      </div>
    <% end %>
  </div>
</div>
```
```
<div class="main posts-show">
  <div class="container">
    <div class="posts-show-item">
      <div class="post-user-name">
  <img src="<%= "/user_images/#{@user.image_name}" %>">
  <%= link_to(@user.name, "/users/#{@user.id}") %>
  </div>
      <p>
        <%= @post.content %>
      </p>
      <div class="post-time">
        <%= @post.created_at %>
      </div>
      <% if @post.user_id == @current_user.id %>
      <div class="post-menus">
        <%= link_to("編集", "/posts/#{@post.id}/edit") %>
        <%= link_to("削除", "/posts/#{@post.id}/destroy", {method: "post"}) %>
      </div>
      <% end %>
    </div>
  </div>
</div>
```
ハッシュ化するgem
