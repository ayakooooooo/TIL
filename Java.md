```
class Main {
  public static void main(String[] args) {
    // 「4 + 2」と「6」を比較し、falseとなるようにしてください
    System.out.println(4 + 2 > 6);
    
    // 「4 + 2」と「6」を比較し、trueとなるようにしてください
    System.out.println(4 + 2 == 6);
    
  }
}
```
***
```
class Main {
  public static void main(String[] args) {
    // trueと出力されるようにしてください
    System.out.println(true);
    
    // falseと出力されるようにしてください
    System.out.println(false);
    
    // 「8 < 5」かつ「3 >= 2」の結果を出力してください
    System.out.println(8 < 5&&3 >= 2);
    
    // 「8 < 5」または「3 >= 2」の結果を出力してください
    System.out.println(8 < 5||3 >= 2);
    
    // 「8 < 5」でない、の結果を出力してください
    System.out.println(!(8 < 5));
    
  }
}
```
```
class Main {
  public static void main(String[] args) {
    int number = 12;
    
    // numberが20より小さいとき、どちらでもないときの条件分岐を追加してください
    if (number < 10) {
      System.out.println("10より小さい");
    }else if(number < 20){
      System.out.println("10以上、20より小さい");
    }else{
      System.out.println("20以上");
    }
    
  }
}
```
```
class Main {
  public static void main(String[] args) {
    int number = 10;
    
    // while文を用いて、numberが0より大きい場合に繰り返す、繰り返し処理を作ってください
    while(number>0){
    System.out.println(number);
    number++;
      
    }
  }
}
```
```
class Main {
  public static void main(String[] args) {
    // 変数namesに、配列を代入してください
    String [] names ={"にんじゃわんこ","ひつじ仙人","ベイビーわんこ"};
    
    // インデックス番号が0の要素を出力してください
    System.out.println(names[0]);
    
    // インデックス番号が2の要素を出力してください
    System.out.println(names[2]);
    
  }
}
```
```
class Main {
  public static void main(String[] args) {
    // printDataメソッドを呼び出してください
    printData();
    
  }
  
  // printDataメソッドを定義してください
  public static void printData(){
  System.out.println("私の名前はKate Jonesです");
}
}
```
```
class Main {
  public static void main(String[] args) {
    // それぞれ年齢に関する引数を追加してください
    printData("Kate Jones",27);
    printData("John Christopher Smith",65);
  }

  // 年齢に関する引数を受け取れるようにしてください
  public static void printData(String name,int age) {
    System.out.println("私の名前は" + name + "です");
    // 「年齢は◯◯歳です」と出力してください
     System.out.println("年齢は" + age + "歳です");
  }
}
```
```
class Main {
  public static void main(String[] args) {
    // fullNameメソッドの結果を変数nameに代入してください
    String name = fullName("Kate", "Jones");
    
    // printDataの引数を書き換えてください
    printData(name, 27);
    
    // こちらは書き換えないでください
    printData("John Christopher Smith", 65);
    
  }

  public static void printData(String name, int age) {
    System.out.println("私の名前は" + name + "です");
    System.out.println("年齢は" + age + "歳です");
  }

  // fullNameメソッドを定義してください
   public static String fullName(String firstName,String lastName){
  return firstName + " " + lastName;
}
}
```
```
class Person {
  // 以下にインスタンスフィールドを定義してください
  public String firstName;
  public String lastName;
  public int age;
  public double height;
  public double weight;

  // 以下にコンストラクタを定義し、インスタンスフィールドに値をセットしてください
  Person (String firstName,String lastName,int age,double height,double weight){
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
    this.height = height;
    this.weight = weight;
  }
  
}
```
オーバーロードとは、引数の型や数が違えば同名のメソッドを定義できる仕組み  
middleNameを引数に受け取らないものと、受け取るもの、2つのコンストラクタを定義  
Javaは渡された引数に合わせて適切なコンストラクタを自動で呼び出し  
```
､､､
class Person {
  public static int count = 0;
  public String firstName;
  // インスタンスフィールドmiddleNameを定義してください
  public String middleName;
  
  public String lastName;
  public int age;
  public double height, weight;

  Person(String firstName,String lastName, int age, double height, double weight) {
    Person.count++;
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
    this.height = height;
    this.weight = weight;
  }
  
  // middleNameを受け取るコンストラクタを定義してください
   Person(String firstName,String middleName,String lastName, int age, double height, double weight) {
    Person.count++;
    this.firstName = firstName;
    this.middleName = middleName;
    this.lastName = lastName;
    this.age = age;
    this.height = height;
    this.weight = weight;
  }

  public String fullName() {
    return this.firstName + " " + this.lastName;
  }

  public void printData() {
    System.out.println("私の名前は" + this.fullName() + "です");
    System.out.println("年齢は" + this.age + "歳です");
    System.out.println("BMIは" + Math.round(this.bmi()) + "です");
  }

  public double bmi() {
    return this.weight / this.height / this.height;
  }

  public static void printCount() {
    System.out.println("合計" + Person.count + "人です");
  }
}
```
***
```
class Person {
  public static int count = 0;
  public String firstName;
  public String middleName;
  public String lastName;
  public int age;
  public double height;
  public double weight;

  Person(String firstName, String lastName, int age, double height, double weight) {
    Person.count++;
    this.firstName = firstName;
    this.lastName = lastName;
    this.age = age;
    this.height = height;
    this.weight = weight;
  }

  Person(String firstName, String middleName, String lastName, int age, double height, double weight) {
    this(firstName, lastName, age, height, weight);
    this.middleName = middleName;
  }

  public String fullName() {
    // 以下を、middleNameがない場合とある場合で条件分岐を行ってください
    if(this.middleName==null){
      return this.firstName + " " + this.lastName;
    }else{
     return this.firstName + " " +this.middleName + " " + this.lastName; 
    }
  }

  public void printData() {
    System.out.println("私の名前は" + this.fullName() + "です");
    System.out.println("年齢は" + this.age + "歳です");
    System.out.println("身長は" + this.height + "mです");
    System.out.println("体重は" + this.weight + "kgです");
    System.out.println("BMIは" + Math.round(this.bmi()) + "です");
  }

  public double bmi() {
    return this.weight / this.height / this.height;
  }

  public static void printCount() {
    System.out.println("合計" + Person.count + "人です");
  }
}

```
```
class Main {
  public static void main(String[] args) {
    Person person1 = new Person("Kate", "Jones", 27, 1.6, 50.0);
    person1.printData();
    Person person2 = new Person("John", "Christopher", "Smith", 65, 1.75, 80.0);
    person2.printData();

    System.out.println("----------------------");
    // person1のmiddleNameフィールドの値を「Claire」にしてください
    person1.setMiddleName("Claire");
    
    System.out.println("ミドルネームを" + person1.getMiddleName() + "に変更しました");
    person1.printData();
  }
}
```
```
class Bicycle{
  private String name;
  private String color;
  
    // インスタンスの生成時にフィールドに値をセットできるよう、コンストラクタを用意            
 Bicycle(String name,String color) {            
 this.name = name; 
 this.color = color;
 }            
                                               
  // Mainクラスからnameフィールドの値を取得するためにゲッターを定義            
public void printData() {            
System.out.println("名前：" + this.name);            
System.out.println("色：" + this.color);            
 }            
 }
```
import java.util.Scanner;
 class Main {
  public static void main(String[] args) {
    Scanner scanner = new Scanner(System.in);
    Bicycle bicycle = new Bicycle("ビアンキ","緑");
    System.out.println("【自転車の情報】");
  bicycle.printData();
  System.out.println("-----------------"); 
  System.out.print("走る距離を入力してください：");
 int bicycleDistance = scanner.nextInt();            
 bicycle.run(bicycleDistance);
 System.out.println("=================");            
   Car car = new Car("フェラーリ", "赤");            
   System.out.println("【車の情報】");            
   car.printData();
   System.out.println("-----------------");            
  System.out.print("走る距離を入力してください：");            
   int carDistance = scanner.nextInt();            
   car.run(carDistance);
  }
}
```
継承されるクラスを「スーパークラス」、継承してできる新しいクラスを「サブクラス」  
「class サブクラス名 extends スーパークラス名」としてクラスを定義  
```
class Main {
  public static void main(String[] args) {
    Car car = new Car();
    // setNameメソッドを用いて、carの名前を「フェラーリ」にしてください
    car.setName("フェラーリ");
    
    // setColorメソッドを用いて、carの色を「赤」にしてください
    car.setColor("赤");
    
    Bicycle bicycle = new Bicycle();
    // setNameメソッドを用いて、bicycleの名前を「ビアンキ」にしてください
    bicycle.setName("ビアンキ");
    
    // setColorメソッドを用いて、bicycleの色を「緑」にしてください
    bicycle.setColor("赤");
    
    System.out.println("【車の情報】");
    car.printData();

    System.out.println("=================");
    System.out.println("【自転車の情報】");
    bicycle.printData();
  }
}

```
