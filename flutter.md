1.Flutter SDK をダウンロード  
2. PATH を通す    
3.Android Studio のセットアップ  
4. Xcode のセットアップ  
5. flutter doctor  
6. Android License の設定  
全て Green になれば終了  
普段 Flutter を書くだけなら Ruby は気にしなくていい  
ただし iOS でビルドするときだけ Ruby と CocoaPods が必要  
今のエラーはまさに「iOS ビルドの準備段階で Ruby/CocoaPods がうまく動いていない」という状態  
Logger は Ruby 標準ライブラリのクラスです。通常は require 'logger' で利用可能  
なのに ActiveSupport が見つけられないということは、Ruby の環境が壊れているか gem の競合が起きている可能性が高い  
