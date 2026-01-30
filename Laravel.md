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
