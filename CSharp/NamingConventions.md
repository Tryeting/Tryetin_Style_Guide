# C#命名規則
## `グローバル変数`
グローバル変数は「_(アンダーバー)」から始める。  
理由：グローバルで定義した変数を把握しておらず、同じ名前の変数名を付け、変数に代入されなかった等の場合に意図しない結果が出ることを防ぐため。  
コード例：
- Case1：グローバル、ローカル双方で同じ変数を定義してローカルで使用
```C#
private static int temp = 10;   //グローバル変数「temp」が定義されていても
private static void test()
{
    var temp = 20;              //ローカル変数tempが定義されているから
    Console.WriteLine(temp);    //「20」と出力される。
}
```
- Case2：グローバルでのみ定義した変数を、ローカルで出力
```C#
private static int temp = 10;   //グローバル変数「temp」を定義しており、
private static void test()
{         
    Console.WriteLine(temp);    //ローカル変数tempが定義されていないから「10」と出力される。
}
```
- Case3：グローバルでは「_」をつけて定義して、それぞれ出力
```C#
private static int _temp = 10;  //グローバル変数と
private static void test()
{
    var temp = 20;              //ローカル変数それぞれ別の命名がされているため、もちろん
    Console.WriteLine(_temp);   //「10」と出力される。
    Console.WriteLine(temp);    //「20」と出力される。
}
```
- Case4：グローバル、ローカル双方で同じ変数を定義したが、ローカルでは条件分岐内で代入されている`（まずいやつ）`
```C#
private static int temp = 10;
private static void test()
{
    if(trueなら処理に入るよ)                //今回はfalseで、処理に入らないことを想定
    {
        var temp = 5000000000000;
    }
    if(tempの中身があれば処理に入るよ)      //おそらくこのようなコードの流れは書かないが
    {
        Console.WriteLine(temp);          //1つめのidでtempに値が代入されればtempを出力したいが、代入されていない場合にグローバルのtemp=「10」が出力されてしまう。
    }
```