
# ドリル
***
12
- HTMLは、Webサイトやアプリケーションなどの画面上に表示する文字、画像、リンクなどの情報を記載する言語。
- CSSは、Webページの文字の大きさや色を装飾するための言語です。他にも背景の色や、レイアウトなども指定できる。  
- 拡張子とは、ファイルの種類を識別するために、ファイル末尾につける文字列のこと。
- HTMLのファイルであれば.html、CSSのファイルであれば.css。
***
13
- HTMLを構成する成分の1つで、< >と</ >で囲まれているものを要素。また、この< >や</ >自体のことをタグ。
- DOCTYPE HTML　この文章がHTML文章であることを宣言する要素、終了タグはない、この要素を記述しないと、レイアウトが崩れ、正しく表示がされない場合がある
- html要素 HTMLを書く際に必要、HTML文章の始まりと終わりを示す要素、HTMLを記述する際に必要な大枠となる要素
- <meta charset="UTF-8"> HTML文章で使用する文字の種類（文字コード）に関する情報を、指定する必要がある
- title要素　ウェブサイトのタイトルを指定する要素
- p要素は、 文章の段落を表す要素。p要素のpはparagraph（=段落）の略。
- 見出し要素は、名前の通り、見出しを作るための要素。 ```<h1>```が一番大きな見出しになる。
- テキストをリンクにすることができる要素```<a href="移動させたいページのURL">```リンクにしたい文字</a>
***
14
- クラス属性は、HTML要素に対して個別に名前を指定するための記述。
- 下記のコードのclass=の部分がクラス属性で、属性値にclass名を指定。
- ```<p class=”text”>おはよう！</p>```
- クラスセレクタは、HTMLで指定したclass名をCSSのセレクタとして使用するための記述。
- クラスセレクタを使用する場合、CSSファイルに「.class名」と記述。
- span要素は、テキストの一部を示すインライン要素,部分的にテキストのフォント調整・文字色・背景色を変更するなどの文字の修飾など行う。
***
15
- HTMLを実装する際は、必ずしもdiv要素を記述する必要はない。
- インライン要素　中身のテキスト量の分だけ横幅が広がる、連続すると横並びで表示される、高さは中身によって変わる
- div要素は特定の意味を持たない要素で、レイアウトを作成する際によく使用されるブロック要素
- header要素とはWebページ最上部のヘッダー専用のブロックレベル要素
- footer要素とはWebページ最下部のフッター専用のブロックレベル要素
- div要素は汎用的に様々な用途で使うことができる要素
- リスト　親要素：ul要素、子要素：li要素
***
16
- 親要素に、display: flex;を指定することで、その直下の子要素が横並びに。
- justify-contentはdisplay: flex;と併せて親要素に記述。子要素の左右（水平）方向の配置を決める際に使用.
- align-itemsはdisplay: flex;と併せて親要素に記述。子要素の上下（垂直）方向の配置を決める際に使用.
***
17
- border: 3px solid red;境界線の太さを3pxに指定する,ボーダは一本線で表示,境界線の色は赤色に指定。
- padding:30px 50px 30px 10px; 上方向と下方向の、内側の余白をそれぞれ30px,左方向の、内側の余白を10px,右方向の、内側の余白を50px。
- margin:50px 30px;上方向と下方向の、外側の余白をそれぞれ50px,左方向と右方向の、外側の余白を30pxとする。
***
18
- position: relative 現在の位置を基準に相対的な位置を決める。
- 親要素にposition: relative;を指定し、子要素にposition: absolute;を指定すると、基準が親要素の左上となる。
***
19
- 画像を用意する手順
- 用意した画像の配置先は自分で指定しなければいけない,
- Finderを用いることで、画像を指定の位置に移動することができる,
- img要素を用いることで、用意した画像を表示させることができる,
- img要素には、画像の場所を指定するsrc属性 、
- 画像が表示されなかった場合に代替テキストなどを表示するためのalt属性も併せて使用。
***
20
- 名前などを入力するための入力欄を作成する際は、input要素
- 1行のテキスト入力欄の作成を行いたいので、type属性はtext
- ```<input type="text" placeholder="NAME" class="name_form">```
***
21
- リセットCSSとは、ブラウザで設定されているデフォルトCSSをリセットするためのCSS。どのブラウザで閲覧しても見た目が変わらないように、デフォルトCSSを削除。
- viewportとはブラウザで表示されている領域のこと。
- vhはviewport heightの略で、viewportの高さに対する割合のこと。
***
24
- ターミナルは、PCに命令をすることができるツール,Macに初めからインストールされているアプリケーション。
- ターミナルの表示は、ユーザー名、コンピューター名、カレントディレクトリの順で表示。
- ディレクトリとはコンピュータ上で複数のファイルを整理するための入れ物（フォルダのようなもの）のこと。
- ホームディレクトリは、 新規にターミナルを立ち上げた場合に作業中となるディレクトリのこと。Macでのデフォルトのホームディレクトリは、/Users/ユーザ名。ターミナルでは~。
- ターミナルで 現在作業中となるディレクトリのことをカレントディレクトリ。ターミナルではここを基準に、PCに命令を出す。
- カレントディレクトリがホームディレクトリに位置する場合は、ターミナルでは〜と表示。
- ターミナルの操作では、指定するディレクトリの場所を全てパスという文字列で表現する。
- パスとは、ディレクトリやファイルの所在を示す文字列のこと。
- パスの指定方法は 絶対パス と 相対パス の2つがある。
- ルートディレクトリから指定するパス
- cd /Users/ユーザ名/Desktop  ...絶対パス
- カレントディレクトリから指定するパス
- cd Desktop/projects  ...相対パス
***
25
- cdコマンドはchange directoryの略
- カレントディレクトリを移動するときに使う。
- cdだけ入力し実行した場合は、ホームディレクトリに移動。
- 使い方はターミナルでcd [移動したいディレクトリのパス]と打ち込んでエンターを押します。
- ホームディレクトリから『Desktopディレクトリ』の『projectsディレクトリ』に移動する際のコマンド cd Desktop/projects
- pwdコマンドはprint working directoryの略
- カレントディレクトリのパスを表示するコマンド。
- lsコマンドはlist segmentsの略
- ディレクトリやファイルの一覧を表示するコマンド。
***
26
- ファイルの種類を表す.htmlや.cssなどを拡張子
- Rubyファイルをプログラムとして実行するには、ターミナルにruby [実行したいRubyファイルのパス]と入力
- プログラムを書いて保存する テキストエディタ
- PCに対して、書いたプログラムを実行するよう命令を出す ターミナル
***
27
- irbは、ターミナルから直接Rubyのプログラムを動かすことができる機能
- 文字列を生成するためには、文字をダブルクォーテーションまたは、シングルクォーテーションで囲みます
- lengthメソッドは、文字列の文字数を数えるメソッド
- 演算子/は割り算
- 演算子%は余剰
***
28
- 文字列と数値は別の種類の値なので、+を使って連結することができない
- エラーを解決するためには、ageに代入した28を文字列に変換すれば良い
- to_sメソッドを使用すると数値を文字列に変換することが可能
- 変数の命名には、Rubyの文法などで使うことがあらかじめ決まっている単語は使用できません
***
29
- 今回はto_iメソッドを使用しているため、文字列は数値へ変換
- getsメソッドで入力された値は、文字列としてプログラムに渡される
- 数値と文字列は違う種類のデータのため、計算ができずにエラー
- 値の種類が異なる文字列と+で連結することが不可能なためエラー
- バックスラッシュ記法はその名前の通り、\（バックスラッシュ） から始まる文字の記法のことです。\nは改行を行う際に使用するバックスラッシュ記法
***
30
- 配列は、複数の値をまとめて管理することができる値
- 配列は順番によって各値に0から始まる番号が割り振られます。この番号のことを添字
- ```pencil_case = ["ペン", "消しゴム", "定規"]```
- ```pencil_case << "えんぴつ"```
- ```puts pencil_case.length```
- 1行目で要素を3つ持つ配列を、pencil_caseという変数に代入
***
31
- ハッシュは、「データ」とそれに対応する「名前」のセットを要素として持つ値
- ハッシュにおいては、データをバリュー、それに対応する名前をキーと呼ぶ
- シンボルオブジェクトとは今回のハッシュのキーのような名前を識別するためのラベル
- シンボルの宣言は、文字列の先頭にコロン:
- ハッシュを生成するためには、キーに””をつけて文字列にするか、:をつけてシンボルオブジェクトにする必要があります。
***
32
- 論理演算子とは、式の真偽の確認や、真偽値に対しての演算を行うことができる演算子
- 論理演算子!=は、A != Bと使用した場合、AとBが等しくない時にtrueを返す
- ==は、A == Bと使用した場合、AとBが等しい時にtrueを返す
***
33
- ブロック変数は、繰り返し処理（今回ならtime do ~ end）の中でしか使用できない
***
35
- クラスは、値の元となるもの。
- 値の共通のルールを定義。
- 共通の情報をまとめ、個別の情報は各データごとに分けることで、開発・管理・保守がしやすくなるという利点がある。
- インスタンスとは、クラスを元にして作られるデータのこと。
- インスタンスは、クラスが使用できるnewメソッドを実行することで生成される。
***
36
- インスタンスメソッドとは、インスタンスが使用できるメソッド
- 「インスタンスメソッドを定義したクラス」から生成される、インスタンスのみが使用できるメソッド
- initializeメソッドが呼び出されるタイミング newメソッドが実行された時
- インスタンス変数の定義方法 @title = 値
- インスタンス変数の特徴 そのクラスのすべてのインスタンスメソッドで使用できる
***
37
- 動的とは、Twitterのように、常に最新のツイートを取得し表示する仕組みや、ユーザーごとで表示されるものが変わるような仕組み。
- 静的とは、誰がいつ見ても、常に同じ内容が表示されるような仕組み。
***
38
- HTTP通信は情報を持っており、その情報の中にはHTMLなどが含まれます。
- 通信後にそれらを画面に表示することで、Webアプリケーションを使うことができる仕組みになっている。
- HTTP通信でやり取りをする場所を、URL。
- URLはインターネットのサービスの場所を表すもの。
- リクエストはデータや情報を要求すること
- レスポンスはリクエストで要求されたデータや情報を返却すること
***
39
- クライアントサイドはクライアントが利用する領域のこと
- Webアプリケーションの見た目やそれを表示するブラウザのこと
- サーバーサイドは実際にWebアプリケーションが存在する領域のこと
***
40
- Sinatraを読み込む require 'sinatra'
- ルーティングとは、リクエストに対してどのような処理を実行するかという道筋を明記する仕組み
- 行いたい処理の種類をサーバーへ伝える部分をHTTPメソッドという
- localhostとは、操作しているPCや端末のこと
***
41
- フレームワークは、最小のコストでWebアプリケーションの作成ができるような仕組みのこと
- Webアプリケーション開発で必要となる作業やリソースを事前に仮定し、用意してくれている
- Ruby on RailsはRubyのフレームワーク
- Ruby on Rails自体で規約を用意
- その規約に乗っ取ったコードを書くことで記述量を少なくすることができ、スピーディーな開発が可能
- この理念をCoC（Convention over Configuration）
***
42
- rails newコマンドは、Railsで新規アプリケーションを作成する際に使用
- このコマンドを実行することで、アプリケーションを作成するための雛形が自動で生成
- もしDBがmysqlのsample_appというアプリケーションを作成したい場合 sample_app -d mysql
- 新しくデータベースを作成するには rails db:create
- データベースの中身をわかりやすく視覚化して表示するアプリケーション Sequel Pro
- MVCについて
- ルーティングは、クライアントからのリクエストの振り分けを行う役割
- コントローラーは、振り分けられたリクエストを処理して、クライアントに返す役割
- モデルは、共通の処理をまとめたり、DBとのやりとり
- ビューは、レスポンスとして返す見た目を用意
***
43
- ルーティングの設定は、configディレクトリの「routes.rb」に記述
- ルーティングの記述方法 [HTTPメソッド] '[URIパターン]', to: '[コントローラー名]#[アクション名]'
- /postsというURLでposts_controller.rbのindexアクションを実行し、ブラウザにページを表示させる
- get '/posts', to: 'posts#index'
- アプリケーションのディレクトリでrails routesコマンドを実行すると、そのアプリケーションで設定されているルーティングを確認できる
***
44
- コントローラーは、ルーティングで振り分けられたリクエストを実際に処理する役割
- コントローラーは、ルーティングからリクエストを受け取って処理を行った後、クライアントにレスポンスを返す
- ルーティングがリクエストを受け取った際、対応するアクションを動かす
- 必要であればモデルとやり取りをする
- レスポンスとして返すビューを決める
- Railsではターミナルのコマンドでコントローラーを作成することができます。
- 例えば、tweetのコントローラーを作成する場合は以下のように
- %  rails g controller tweets
- 一度作成したコントローラーの関連ファイルを全て削除
- rails d controller コントローラー名
