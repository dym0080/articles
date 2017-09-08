## 理解 `prototype`和 `__proto__`
`prototype`是函数的属性，`__proto__`是对象的属性。

首先来看三个例子：
```js
       //例子1
        function Person() {
            
        }
        var person1=new Person();
        var person2=new Person();
        person1.age=12;
        console.log(person1.age);// 12
        console.log(person2.age);// undefined
```
```js
        //例子2
       function Person() {
            
        }
        Person.prototype.age=12;
        var person1=new Person();
        var person2=new Person();
        console.log(person1.age);// 12
        console.log(person2.age);// 12
```
```js
        //例子3
        function Person() {
            
        }
        Person.prototype.age=12;
        var person1=new Person();
        var person2=new Person();
        person1.age=17;
        console.log(person1.age);// 17
        console.log(person2.age);// 12
```
在这三个例子中，`Person` 就是一个构造函数，我们使用 `new` 创建了两个实例对象 `person1`，`person2`。这两个实例对象的原型是`Person.prototype`。

什么是原型呢？你可以这样理解：每一个JavaScript对象(null除外)在创建的时候就会与之关联另一个对象，这个对象就是我们所说的原型，每一个对象都会从原型"继承"属性。

在例子1中，在实例对象`person1`上加了`age`属性，`person2`上没有加属性，所以打印出来是`12`和`undefined`。

在例子2中，直接在构造函数`Person`的原型(`Person.prototype`)上加了`age`属性，打印时`person1`、`person2`都在它们各自的实例中都没有找到age属性，然后去它们的原型中找到了age属性，所以打印出来都是12。

在例子3中，直接在构造函数`Person`的原型(`Person.prototype`)上加了`age`属性，打印时`person1`在实例中找了`age`属性，值为17，所以打印17，`person2`在实例中没有找到`age`属性，然后去它的原型中找到了age属性，值为12，所以打印出来是12。

每个函数都有一个` prototype` 属性，该属性指向了一个对象，这个对象正是调用该构造函数而创建的实例的原型，也就是这个例子中的 `person1 `和 `person2` 的原型。构造函数是通过` prototype` 来指向原型，那么使用构造函数创建的实例是通过什么指向原型的呢？答案是`__proto__`。

每一个JavaScript对象(除了 null )都具有的一个属性，叫`__proto__`，这个属性会指向该对象的原型。

我们用一张图来展示构造函数，实例，原型之间的关系：

![关系图](http://upload-images.jianshu.io/upload_images/1018021-bc1bcd0bb412c275.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

通过这张图，我们可以看到，构造函数`Person`是通过` prototype`指向原型，使用构造函数创建的实例person是通过`__proto__`指向原型，两者是指向同一个原型(`Person.prototype`)，该原型本身也是一个对象。为了证明两者是指向同一个原型，可在浏览器控制台输入以下代码验证：
```js
        function Person() {

        }
        var person = new Person();
        console.log(person.__proto__ === Person.prototype); // true
```
既然实例对象和构造函数都可以指向原型，那么原型是否有属性指向构造函数或者实例呢？
>对于`__proto__`, 绝大部分浏览器都支持这个非标准的方法访问原型，然而它并不存在于` Person.prototype `中，实际上，它是来自于 `Object.prototype` ，与其说是一个属性，不如说是一个 `getter/setter`，当使用` obj.__proto__` 时，可以理解成返回了 `Object.getPrototypeOf(obj)`。

## constructor

指向实例倒是没有，因为一个构造函数可以生成多个实例，但是原型指向构造函数倒是有的，这就是属性constructor，每个原型都有一个 constructor 属性指向关联的构造函数。更新下上面的关系图：

![image.png](http://upload-images.jianshu.io/upload_images/1018021-ff65faa417dc50f7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
为了验证这一点，我们可以尝试：
```js
        function Person() {

        }
        console.log(Person=== Person.prototype.constructor); // true
```
值得注意的地方，看下面的例子：
```js
    function Person() {

    }
    var person = new Person();
    console.log(person.constructor === Person); // true
```
当获取` person.constructor` 时，其实` person` 中并没有 `constructor` 属性,当不能读取到`constructor` 属性时，会从 `person` 的原型也就是 `Person.prototype` 中读取，正好原型中有该属性。

## 实例与原型
当读取实例的属性时，如果找不到，就会查找与对象关联的原型中的属性，如果还查不到，就去找原型的原型，一直找到最顶层为止。
```js
    function Person() {
    
    }
    Person.prototype.age = 18;
    var person = new Person();
    person.age = 24;
    console.log(person.age) // 24
    delete person.age;
    console.log(person.age) // 18
```
在这个例子中，我们给实例对象 `person` 添加了 `age `属性，当我们打印 `person.age` 的时候，结果自然为 24。

但是当我们删除了 `person` 的 `age` 属性时，读取 `person.age`，从 `person` 对象中找不到 age 属性就会从 `person` 的原型也就是 `person.__proto__ `，也就是 `Person.prototype`中查找，幸运的是我们找到了 `age` 属性，结果为 18。

但是万一还没有找到呢？原型的原型又是什么呢？
## 原型的原型
原型对象是通过 `Object `构造函数生成的，结合之前所讲，实例的 `__proto__ `指向构造函数的 `prototype` ，所以我们再更新下关系图：

![image.png](http://upload-images.jianshu.io/upload_images/1018021-6ed14c4a406bba3c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
## 原型链
那 `Object.prototype `的原型呢？答案是 `null`。不信我们可以打印：
```js
  console.log(Object.prototype.__proto__ === null) // true
```
所以查到属性的时候查到 `Object.prototype `就可以停止查找了。最后一张关系图更新：

![image.png](http://upload-images.jianshu.io/upload_images/1018021-0a52595953717c30.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
顺便还要说一下，图中由相互关联的原型组成的链状结构就是原型链，也就是蓝色的这条线。

参考：
- [JavaScript深入之从原型到原型链](https://github.com/mqyqingfeng/Blog/issues/2)
