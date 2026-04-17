12まだ不安定　　
11安定
```
① Laravel 12 プロジェクト作成
composer create-project laravel/laravel laravel-form
cd laravel-form

② DB設定（.env）



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
```
ステップ36：部屋管理用のメソッドをAdminControllerに追加
ステップ37：部屋管理用のルートを追加
```
```
ステップ38：部屋一覧画面を作成		
ステップ39：部屋編集画面を作成		
ステップ40：部屋追加画面を作成		
		
ステップ41：ステップ35の時点で：全予約一覧のビューを作り忘れていた				
管理画面に「全予約一覧」と「部屋管理」のボタンが表示されるように
```
```
ステップ42：ルーテイングに availability を追加			
ステップ43：コントローラーに availability メソッドを追加			
ステップ44：空室確認画面のビューを作成			
ステップ45：管理画面のナビゲーションに「空室確認」ボタンを追加
ステップ46：roomsテーブルにcapacityカラムを追加
ステップ47：マイグレーションファイルを編集
ステップ48：マイグレーション実行
ステップ49：部屋編集画面に定員を変更できる入力欄を追加
ステップ50：コントローラーのupdateRoomメソッドにcapacityを追加
ステップ50：コントローラーのupdateRoomメソッドにcapacityを追加（途中）	
ステップ51：部屋追加画面（create.blade.php）にもcapacityの入力欄を追加	
ステップ52：コントローラーのstoreRoomメソッドにもcapacityを追加	
ステップ53：部屋一覧画面に定員を表示	
ステップ54：動作確認❌　Room モデルの $fillable に capacity 追加
```
```
バージョンアップ
マイナーはそのまま？？
管理画面にもチェックアウト
```
```
連泊対応の全ステップ			
ステップ1：マイグレーションファイルを作成			
ステップ2：マイグレーションファイルを編集			
ステップ3：マイグレーション実行			
ステップ4：Bookingモデルにcheck_out_dateを追加			
ステップ5：予約フォームにチェックアウト日の入力欄を追加			
ステップ6：コントローラーの予約保存処理を修正			
ステップ7：重複チェックのロジックを期間対応に修正			
ステップ8：予約一覧にチェックアウト日を表示			
ステップ9：動作確認
```
```
横スクロール
overflow
```
```
ステップ１ ローカルでhotel-bookingを複製　　OK
ステップ２ フォルダ名をreservation-systemなどに変更　　OK
ステップ3：データベースの作成
ステップ4：.envファイルを編集
ステップ5：マイグレーションファイルの修正
```
```
汎用性のあるカラム名に  
＊マイグレーションファイルの修正  
　　・create_rooms_table → resourcesテーブルに変更  
　　・create_bookings_table → 時間帯予約に変更  

＊不要なマイグレーションファイルを削除  
　　・add_capacity_to_rooms_table  
　　・add_check_out_date_to_bookings_table
```
```
ステップ６：php artisan migrate でテーブル作成
ステップ７：モデルの修正
ステップ８：コントローラーの修正
ステップ９：管理者用のコントローラーを修正
ステップ１０：routes/web.php の修正
```
```
ステップ1：resourcesテーブルに
time_slot_minutesカラムを追加
（マイグレーション）

ステップ2：Resourceモデルに
time_slot_minutesを追加

ステップ3：管理画面のリソース追加・編集画面に
時間刻みの入力欄を追加

ステップ4：AdminControllerの
storeResource・updateResourceに
time_slot_minutesを追加

ステップ5：ユーザーの予約フォームに
時間刻みを反映した
時間選択プルダウンを追加

ステップ6：BookingControllerに
時間刻みの検証を追加

ステップ7：動作確認
```
```
ステップ１： 営業時間のマイグレーション ← 今日はここから
ステップ２ ：Resourceモデルに追加
ステップ３：管理画面に営業時間の入力欄を追加
ステップ４：AdminControllerの修正
ステップ５：ユーザーの予約フォームに時間刻みを反映した時間選択プルダウンを追加、カラム名修正
ステップ６：BookingControllerに検証を追加
ステップ７：動作確認
```
```
過去時間の予約が可能　これ修正
リソース管理に開始時間と終了時間も表示
```
```
⑧ 空き状況ページの改修

修正
空き状況確認ページがおかしい
"4/23　舟下り３　12：00〜15:00まで予約したのに
4/23　舟下り３　12：00のみ×　　 13：00〜　14：00〜もバツなはずなのになぜ？"
"予約の start_time が 12:00 なので、現在のロジックでは12:00〜13:00の1時間だけが予約ありと判定されています。
13:00〜14:00・14:00〜15:00は予約の start_time がないので○になってしまっています。"
これ修正

修正
予約ページがおかしい
"舟下り1 ー2026-04-20        10:00:00        10:30:00で予約した後、
舟下り1ー2026-04-20 　　10:30から予約しようとすると、「その時間帯はすでに予約されています。」とでてできないようでした。"
重複チェック部分を修正

修正
⚪︎×△判定がおかしい
"鈴木健二        舟下り4        2026-05-02        15:00        16:30       15:00△16:00△ 本当は  15:00❌16:00△　のはず
鈴木健二        舟下り1        2026-04-20        10:00:00        10:30:00　10:00❌　本当は10:00△のはず"
"$bookedCount = ...->count();　　👉 「予約件数」を見てるだけ
でも本当は「何枠埋まっているか」 を見ないといけない"
```
