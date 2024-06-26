# 関数  
いくつかの処理をまとめたもの
「あいさつをする」「名前を言う」という2つの処理を「introduce」という名前でまとめる、など  
***

```
function()  {
まとめたい処理
}
``` 
「関数を定義する」という 

関数を定義した後、  
```定数名();  ```
と書くことで関数の中の処理を実行できる  
「関数を呼び出す」という  
```
const greet = function() {
  console.log("こんにちは！");
  console.log("関数を学習していきましょう！");
};

// 関数を呼び出してください
greet();
```
# 関数の代入  
```
// 定数helloに関数を代入してください
const hello = function(){
console.log("こんにちは！");
console.log("私の名前は○○です");
};
// 定数helloに代入された関数を呼び出してください
hello();
```
# アロー関数  
```
「function()」の部分を「() =>」
===============================  
// 定数greetにアロー関数を代入してください
const greet = ()=> {
console.log("こんにちは！");
};
// 定数greetを呼び出してください
greet();
```
# 引数
関数に与える追加情報のようなもの  
関数を呼び出すときに一緒に値を渡すことで、関数の中でその値を利用することができる

引数を受け取る関数を定義  
```
(引数名) =>
```
括弧の中に引数名を書くことで引数を受け取ることができる
```
// 関数の引数にnameを追加してください
const greet = (name) => {
  // 「こんにちは、〇〇さん」となるように出力してください
  console.log(`こんにちは、${name}さん`);
  
};

// greetの引数に「ひつじ仙人」を渡して呼び出してください
greet("ひつじ仙人");
```
***
// 関数の引数にnumber1とnumber2を追加してください
const add = (number1,number2) => {
  // number1とnumber2を足した値をコンソールに出力してください
 console.log(number1+number2);
};

// 引数に5と7を渡して関数を呼び出してください
add(5,7);
***
# 戻り値
「return 値 」と書くことで、関数はその値を戻り値として返す
```
const half = (number) => {
  // numberを2で割った値を戻り値として返してください
  return number/2　;
};

// 定数resultを定義してください
const result=half(130);

// 「130の半分は〇〇です」となるように出力してください
console.log(`130の半分は${result}です`);
```
if文で使うような条件式をreturnすると、
その条件式の結果として得られる真偽値（trueまたはfalse）を返すことができる
関数の処理を終了させる性質も持っています
returnの後にある関数内の処理は実行されない
```
const check = (number) => {
  // numberが3の倍数かどうかを戻り値として返してください
  return number %3 ===0;
  
};

// if文の条件式で、checkを呼び出してください
if (check(123)) {
  console.log("3の倍数です");
} else {
  console.log("3の倍数ではありません");
}
```

# スコープ
定数や変数の使用できる範囲のこと  
関数の外側で定義した定数や変数は、プログラムのどこからでも使える  
関数の{}内で定義した定数や変数は、その関数の内側でのみ使用  
関数の内側で定義された定数を関数の外側で使用すると参照エラー  
```
// 関数の外側に定数nameを定義してください
const name = "ひつじ仙人";

const introduce = () => {
  // 関数の内側に定数nameを定義してください
  const name = "にんじゃわんこ";

  // 定数nameを出力してください
  console.log(name);
  
};

introduce();

// コードを貼り付けて、定数nameを出力してください。
console.log(name);
```
これで、
にんじゃわんこ  
ひつじ仙人  
出力される  
# 時間を分に換算するtoMinutes関数  
時間（hour）と分（minutes）の数値を引数に受け取り、  
分に換算した結果を戻り値として返す  
```
// toMinutes関数を定義してください
const toMinutes = (hour,minute)=>{
return hour*60+minute;
}
// 定数resultに、toMinutes関数の戻り値を代入してください
const result = toMinutes(3,20);

// 「◯◯分」となるように、分に換算した結果を出力してください
console.log (`${result}分`);
```
