- [前端基础进阶（三）：变量对象详解](http://www.jianshu.com/p/330b1505e41d)

这篇文章已经讲解的很好的，不用自己再总结了。
特别要掌握的是：
上下文的生命周期可以分为两个阶段
- 创建阶段
在这个阶段中，执行上下文会分别创建变量对象，建立作用域链，以及确定this的指向
- 代码执行阶段
创建完成之后，就会开始执行代码，这个时候，会完成变量赋值，函数引用，以及执行其他代码。

![image.png](http://upload-images.jianshu.io/upload_images/1018021-8350d65b7a1828c0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

变量对象的创建，依次经历了以下几个过程。
1. 建立arguments对象。检查当前上下文中的参数，建立该对象下的属性与属性值。
2. 检查当前上下文的函数声明，也就是使用function关键字声明的函数。在变量对象中以函数名建立一个属性，属性值为指向该函数所在内存地址的引用。** 如果函数名的属性已经存在，那么该属性将会被新的引用所覆盖。**
3. 检查当前上下文中的变量声明，每找到一个变量声明，就在变量对象中以变量名建立一个属性，属性值为undefined。** 如果该变量名的属性已经存在，为了防止同名的函数被修改为undefined，则会直接跳过，原属性值不会被修改。**

![image.png](http://upload-images.jianshu.io/upload_images/1018021-107b8a7bcf2bad9d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
