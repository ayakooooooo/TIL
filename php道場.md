- 表示させる
```
<?php
echo "Hello, PHP";
echo'<br>';
echo "10 + 7";
?>
```
```
<?php
$name = 'Tom';
echo '変数$nameの値: '.$name;
echo '<br>';
echo '-----';
echo '<br>';

// この下にコードを書いてください
echo "My name is {$name}";

?>
```
- 変数$priceと$taxRateから税込価格を求めて、税込価格は○○円ですと出力してください。
```
<?php
$price = 1000;
$taxRate = 0.08;
echo '変数$priceの値: '.$price;
echo '<br>';
echo '変数$taxRateの値: '.$taxRate;
echo '<br>';
echo '-----';
echo '<br>';

// この下にコードを書いてください
$kakaku= $price + $price * $taxRate;
echo '税込価格は'.$kakaku.'円です';

?>
```
- 変数$moneyには所持金が代入されています。
- 次に所持金と求めた税込価格の比較結果に応じて、文字列を出力してみましょう。

-以下のように出力してください。
・所持金が税込価格より大きい場合、
商品を買うことができます

・両方の値が等しい場合、
商品を買うことができますが、所持金がなくなります

・所持金が税込価格より小さい場合、
商品を買うことができません

```
<?php
$money = 2000;
$price = 1000;
$taxRate = 0.08;
echo '変数$moneyの値: '.$money;
echo '<br>';
echo '変数$priceの値: '.$price;
echo '<br>';
echo '変数$taxRateの値: '.$taxRate;
echo '<br>';
echo '-----';
echo '<br>';

// この下にコードを書いてください
$kakaku = $price + $price * $taxRate;

if ($money>$kakaku){
  echo "商品を買うことができます";
}else if($money===$kakaku){
 echo "商品を買うことができますが、所持金がなくなります";
}else{
  echo "商品を買うことができません";
}
?>
```
- 「$i が 3 の倍数かつ 5 の倍数」の条件を最初にチェックしないと、正しく動作しません。
- このコードじゃダメ。
```
<?php
for($i=1;$i<=100;$i++){
  
  if($i % 3 == 0){
    echo 'Fizz';
    echo '<br>'; 
  }elseif($i % 5 == 0){
    echo 'Buzz';
    echo '<br>'; 
  }elseif($i % 3 == 0 && $i % 5 == 0){
    echo 'FizzBuzz';
    echo '<br>'; 
  }else{
   echo $i;
   echo '<br>'; 
  }
}
?>
```
- これが正解！！
```
<?php
for($i=1;$i<=100;$i++){
  
  if($i % 3 == 0 && $i % 5 == 0){
    echo 'FizzBuzz';
 
  }elseif($i % 5 == 0){
    echo 'Buzz';
  
  }elseif($i % 3 == 0){
    echo 'Fizz';
  
  }else{
   echo $i;
 
  }            
 echo '<br>';            
 }
?>
```
foreachで配列の中身全部足して表示させる{}の外にechoしないとダメ
- $totalPrice は最初に 0 で初期化される。
- ループが始まり、最初の $price（1000）が $totalPrice に加算される → $totalPrice = 1000。
- 次の $price（2000）が加算される → $totalPrice = 3000。
- 最後の $price（1500）が加算される → $totalPrice = 4500。
- echo によって「合計金額は4500円です」と表示される。
```
<?php
$prices = array(1000, 650, 750, 800);
echo '$pricesの値: ';
foreach ($prices as $price) {
  echo $price.' ';
}
echo '<br>';
echo '-----';
echo '<br>';

// この下にコードを書いてください
$totalPrice = 0;
foreach ($prices as $price) {
$totalPrice = $totalPrice + $price;
}
echo '合計金額は'.$totalPrice.'円です';

?>
```
```
- 配列$pricesで与えられた価格の最高価格を求めて、
- 最高価格は○○円ですと出力してください。
<?php
$prices = array(1000, 650, 750, 800);
echo '$pricesの値: ';
foreach ($prices as $price) {
  echo $price.' ';
}
echo '<br>';
echo '-----';
echo '<br>';

// この下にコードを書いてください
$maxPrice = 0;
$totalPrice =0;
foreach ($prices as $price) {
  $totalPrice = $totalPrice+$price;
  if ($price > $maxPrice){
    $maxPrice=$price;
  }
}
echo '合計金額は'.$totalPrice.'円です';            
echo '<br>';
echo '最高価格は'.$maxPrice.'円です';

?>
```
```
<?php
$menu = array('name' => 'CURRY', 'price' => 900);
echo '$menuの値: ';
// var_exportは変数の中身を見るための関数です
var_export($menu);
echo '<br>';
echo '-----';
echo '<br>';

// この下にコードを書いてください
echo $menu['name']."は".$menu['price']."円です";

?>
```
-　これ間違い、$menusじゃなく$menuで。
- コードの間違いは、foreach ループ内で $menu を使っているのに、$menus['name'] や $menus['price'] を参照している点です。
- ループ内では、$menu に各メニューの情報が入っているので、$menu['name'] や $menu['price'] を使用する必要があります。

```
<?php
$menus = array(
  array('name' => 'CURRY', 'price' => 900),
  array('name' => 'PASTA', 'price' => 1200),
  array('name' => 'COFFEE', 'price' => 600)
);

// この下にコードを書いてください
foreach ($menus as $menu) {
 echo $menus['name'].'は'.$menus['price'].'円です';
 echo '<br>';
}

?>
```
- 正しくはこれ
```
<?php
$menus = array(
  array('name' => 'CURRY', 'price' => 900),
  array('name' => 'PASTA', 'price' => 1200),
  array('name' => 'COFFEE', 'price' => 600)
);

// この下にコードを書いてください
foreach ($menus as $menu) {
 echo $menu['name'].'は'.$menu['price'].'円です';
 echo '<br>';
}

?>
```
- これだと間違い。
- コードにいくつか問題があります。主な問題は、$totalprice の計算において $menu が正しく使われていないことです。
- 具体的には、$menu は配列であり、そのまま加算することはできません。$menu['price'] を使って価格を加算する必要があります。
```
<?php
$menus = array(
  array('name' => 'CURRY', 'price' => 900),
  array('name' => 'PASTA', 'price' => 1200),
  array('name' => 'COFFEE', 'price' => 600)
);

// この下にコードを書いてください
foreach ($menus as $menu) {
 echo $menu['name'].'は'.$menu['price'].'円です';
 echo '<br>';
}
$totalprice = 0;
foreach ($menus as $menu) {
$totalprice = $totalprice + $menu;
}
echo '合計金額は'.$totalprice.'円です';
?>
```
```
<?php
$menus = array(
  array('name' => 'CURRY', 'price' => 900),
  array('name' => 'PASTA', 'price' => 1200),
  array('name' => 'COFFEE', 'price' => 600)
);

// この下にコードを書いてください
foreach ($menus as $menu) {
 echo $menu['name'].'は'.$menu['price'].'円です';
 echo '<br>';
}
$totalprice = 0;
foreach ($menus as $menu) {
$totalprice = $totalprice + $menu['price'];
}
echo '合計金額は'.$totalprice.'円です';
?>
```
```
<?php
$menus = array(
  array('name' => 'CURRY', 'price' => 900),
  array('name' => 'PASTA', 'price' => 1200),
  array('name' => 'COFFEE', 'price' => 600)
);

// この下にコードを書いてください
foreach ($menus as $menu) {
 echo $menu['name'].'は'.$menu['price'].'円です';
 echo '<br>';
}

$totalprice = 0;
$maxPrice = 0;
$maxPricemenuname = 0;

foreach ($menus as $menu) {
$totalprice = $totalprice + $menu['price'];
if($menu['price']>$maxPrice){
  $maxPrice = $menu['price'];
  $maxPricemenuname = $menu['name'];
}
}
echo '合計金額は'.$totalprice.'円です';
 echo '<br>';
echo $maxPricemenuname.'が最高価格で'.$maxPrice.'です';

?>
```
- 最初の $maxPrice は 0 です。
- 最初のメニュー CURRY の価格 900 は $maxPrice より大きいので、$maxPrice が 900 に更新され、 $maxPricemenuname が 'CURRY' になります。
- 次に PASTA の価格 1200 は現在の $maxPrice より大きいので、$maxPrice が 1200 に更新され、 $maxPricemenuname が 'PASTA' になります。
- 最後の COFFEE の価格 600 は $maxPrice よりも小さいので、 $maxPrice と $maxPricemenuname は変わりません。
- このようになまえは随時更新されている。それがりかいできなかった。
```
<?php
$menus = array(
  array('name' => 'CURRY', 'price' => 900),
  array('name' => 'PASTA', 'price' => 1200),
  array('name' => 'COFFEE', 'price' => 600)
);

// この下にコードを書いてください
foreach ($menus as $menu) {
 echo $menu['name'].'は'.$menu['price'].'円です';
 echo '<br>';
}

$totalprice = 0;
$maxPrice = 0;
$maxPricemenuname = '';

foreach ($menus as $menu) {
$totalprice = $totalprice + $menu['price'];
if($menu['price']>$maxPrice){
  $maxPrice = $menu['price'];
  $maxPricemenuname = $menu['name'];
}
}
echo '合計金額は'.$totalprice.'円です';
echo '<br>';
echo $maxPricemenuname.'が最高価格で'.$maxPrice.'円です';
echo '<br>';
?>
```
