#  Dart学习笔记

### 一.Class

>
> Dart中一切皆为对象，而每个对象都是一个类的实例，所有的类都继承于Object。
>
> 除了普通的构造方法，Dart中的Class还提供了不同用途的构造方法，比如命名构造方法、重定向构造方法、常量构造方法、工厂构造方法，还有初始化参数列表等。
>
> 抽象类
> 抽象类使用abstract关键字定义，是不能被实例化的，通常用来定义接口以及部分实现。
> 但与其他语言不太一样的地方是，抽象方法也可以定义在非抽象类中。
>
> mixin
> Dart语言集合了现代编程语言的众多优点，Mixin继承机制也是其一。具体的读法应该叫做 mix in，翻译下就是混入。

#### 1. 构造函数（3种写法）

```dart
class Animal{
  int age;
  String name;
//  1.语法糖写法
//  Animal(this.age,this.name);
//  2.构造函数
  Animal(int age,String name){
    age = age;
    name = name;
  }
//  3.Map
  Animal.fromJson(Map data){
    age = data['age'];
    name = data['name'];
  }
}
// main
void main() {
  const obj = {
    'age': 1,
    'name':'dog'
  };
  var dog = new Animal.fromJson(obj);
  print(dog.name);
}
```

#### 2.Getter与Setter

```dart
class React {
  int width;
  int left;
  int height;
  int top;
    
  React(this.width,this.left,this.height,this.top);
    
  int get right => width+left;
      set right(val)=> left = val -width;
}
```

#### 3.抽象类

```dart
abstract class Doer {
  // ...Define instance variables and methods...
  void doSomething(); // Define an abstract method.
}

class EffectiveDoer extends Doer {
  void doSomething() {
    // ...Provide an implementation, so the method is not abstract here...
  }
}
```

> 继承抽象类的类，必须实现抽象类的方法

#### 4. with实现mixins

```dart
mixin TestMixin {
  void test() {
    print('test');
  }
  int testInt = 1;
  void test2();
}

class Test with TestMixin {
  @override
  test2() {
    print('test2');
  }
}

void main() {
  Test().test();            // test
  print(Test().testInt);    // 1
  Test().test2();           // test2
}
```

> mixins的类中，可以调用被mixins类的属性和方法。