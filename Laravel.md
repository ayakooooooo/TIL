12まだ不安定　　
11安定
```
① Laravel 12 プロジェクト作成
composer create-project laravel/laravel laravel-form
cd laravel-form

② DB設定（.env）
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=laravel_form
DB_USERNAME=root
DB_PASSWORD=


DBを先に作っておきます（phpMyAdminなどでOK）

③ 認証機能を一瞬で作る（超重要）

LaravelはBreezeが学習向きです。

composer require laravel/breeze --dev
php artisan breeze:install


どれにするか聞かれたら👇
👉 Blade + PHP を選択

php artisan migrate
npm install
npm run dev
php artisan serve


🎉
これだけで

ユーザー登録

ログイン

ログアウト

パスワードリセット
全部完成！

④ まず動作確認

ブラウザで

http://127.0.0.1:8000


/register → 登録

/login → ログイン

DBの users テーブルに保存されていれば成功✨

⑤ 学習用：簡単な「投稿フォーム」を作る

例：メモ投稿フォーム

モデル＆マイグレーション
php artisan make:model Post -m

// database/migrations/xxxx_create_posts_table.php
Schema::create('posts', function (Blueprint $table) {
    $table->id();
    $table->foreignId('user_id')->constrained()->cascadeOnDelete();
    $table->string('title');
    $table->text('body');
    $table->timestamps();
});

php artisan migrate

⑥ ルーティング（ログイン必須）
// routes/web.php
Route::middleware('auth')->group(function () {
    Route::get('/posts/create', [PostController::class, 'create']);
    Route::post('/posts', [PostController::class, 'store']);
});

⑦ コントローラ
php artisan make:controller PostController

use App\Models\Post;
use Illuminate\Http\Request;

class PostController extends Controller
{
    public function create()
    {
        return view('posts.create');
    }

    public function store(Request $request)
    {
        $request->validate([
            'title' => 'required',
            'body' => 'required',
        ]);

        Post::create([
            'user_id' => auth()->id(),
            'title' => $request->title,
            'body' => $request->body,
        ]);

        return redirect()->back()->with('success', '保存しました');
    }
}


※ Post モデルに👇を忘れずに

protected $fillable = ['user_id', 'title', 'body'];

⑧ フォーム（Blade）
<!-- resources/views/posts/create.blade.php -->
<form method="POST" action="/posts">
    @csrf

    <input type="text" name="title" placeholder="タイトル">
    <textarea name="body"></textarea>

    <button>保存</button>
</form>

⑨ ログアウト

Breezeならすでに用意済み👇

<form method="POST" action="{{ route('logout') }}">
    @csrf
    <button>ログアウト</button>
</form>

学習の順番（超おすすめ）

1️⃣ Breezeで認証の全体像を見る
2️⃣ Controller → Route → View → Model の流れ
3️⃣ auth()->id() の意味
4️⃣ middleware（auth）
```
```
Breezeてなんですかrubyでいうgem??
Laravel Breeze は  
👉 「ログイン・登録・ログアウト」を一式まとめて用意してくれる公式パッケージ
Breeze がやってくれること
インストールすると自動で👇が入ります
ユーザー登録
ログイン / ログアウト
パスワードリセット
認証用ルーティング
コントローラ
Blade（画面）
バリデーション
セッション管理
👉 「認証の土台」全部
```
```
cd ~/Sites/localhost
composer create-project laravel/laravel laravel-form
```
```
✅ Laravel 12.49.0（最新版）がインストールされた
✅ 依存パッケージ111個が正常にインストール
✅ アプリケーションキーが生成された
✅ マイグレーションが自動実行された（SQLiteで）
✅ エラーなし、セキュリティ問題なし
```
```
SQLiteからMySQLに切り替えたことで、より実践的な環境に
```
```
Breezeインストール  
セットアップ  
Nodeなくてエラー  
```
```
Nodeインストール
マイグレーション
```
```
ステップ1：新しいLaravelプロジェクトを作成  
ステップ2：データベース設定  
ステップ3：タイムゾーンと日本語設定  
ステップ4：マイグレーション実行  
ステップ5：Breezeインストール  
ステップ6：Breezeセットアップ  
ステップ7：マイグレーション実行  
ステップ8：動作確認  
ステップ9：Roomモデルとマイグレーション作成（部屋テーブルの箱を作る）  
ステップ10：roomsテーブルのマイグレーションファイルを編集（部屋テーブルの中身を設計）  
ステップ11：Bookingモデルとマイグレーション作成（予約テーブルの箱を作る）  
ステップ12：bookingsテーブルのマイグレーションファイルを編集（予約テーブルの中身を設計）  
ステップ13：マイグレーション実行（設計図を見ながら、実際にデータベースにテーブルを作った）  
ステップ14：Roomモデルを編集（部屋データを登録できるようにする）  
ステップ15：Bookingモデルを編集（予約データを登録できるようにする）  
ステップ16：10部屋の初期データを登録（初期データを入れる箱を用意）  
ステップ17：RoomSeederを編集（10部屋のデータを書く）  
ステップ18：シーダーを実行（実際にデータベースに10部屋を登録）  
ステップ19：BookingControllerを作成  
ステップ20：BookingControllerを編集  
ステップ21：ルーティングを設定  
```
```
ステップ22：ビュー（予約画面）を作成
ステップ23：動作確認
```
```
ステップ24：usersテーブルにis_adminカラムを追加			
ステップ25：マイグレーションファイルを編集			
ステップ26：マイグレーション実行			
ステップ27：自分を管理者にする			
ステップ28 ： 管理者専用の門番（チェック機能）			
ステップ29：IsAdminミドルウェアを編集（チェック機能追加）			
ステップ30：ミドルウェアを登録（作った門番（IsAdmin）をシステムに登録して、使えるようにする）			
ステップ31：AdminControllerを作成（管理画面用のコントローラー）			
ステップ32：AdminControllerに仕事内容を教える			
ステップ33：管理画面のデザインを作る			
ステップ34：「このURLなら管理画面」と設定			
ステップ35：実際に動かしてみる			
```
