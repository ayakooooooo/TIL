Visual Studio Code (VS Code) でPHPを実行するための手順  

VS Codeの設定:  
VS Codeの設定ファイル settings.json にPHPのパスを設定します。  
メニューから「ファイル」 > 「ユーザー設定」 > 「設定」をクリックします。  
「拡張機能」を選択し、「PHP 実行可能ファイルを指定」します。  
VS Code拡張機能「PHP Server」のインストール:  
「拡張機能」の「Marketplace」で「phpserver」を検索してインストールします。  
XAMPPのインストール:  
XAMPPのインストーラーからXAMPPをダウンロードしてインストールします。  
path環境変数の設定:  
path環境変数に「C:\xampp\php」を追加します。  
※「システム環境変数」に追加した場合は再起動が必要です。  
以上の設定を行った後、VS CodeでPHPファイルを編集したら、コード上で右クリックし、  
「PHP Server: Serve project」などを選択するだけで、ブラウザが開き、該当のファイルが実行されます。  
***
初めてのプログラミング言語を触る際、環境構築を必ず行う    
XAMPP（シャンプ）はPHPの実行環境を提供 
１、XAMPPインストール  
2、VSCodeエディタをインストール  
３、VSCode拡張機能「PHP IntelliSense」インストール  
4、VSCode側の「基本設定（setting.json）」を編集する  
***
macOSでのXAMPPの削除手順:
Finderを開きます。
アプリケーションフォルダーに移動します。
XAMPPフォルダーを見つけて右クリックし、「ゴミ箱に入れる」を選択します。
ゴミ箱を空にしてXAMPPを完全に削除します。
***
