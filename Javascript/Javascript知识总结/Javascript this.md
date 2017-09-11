
this 指针存在于函数中，用以标识函数运行时所处的上下文。函数的类型不同，this指向规则也不一样：对于普通函数，this 始终指向全局对象window；对于构造函数，this则指向新创建的对象；对于方法，this指向调用该方法的对象。另外，Function对象也提供了call、apply 和 bind 等方法来改变函数的 this 指向，其中，call 和 apply 主动执行函数，bind一般在事件回调中使用，而 call 和 apply 的区别只是参数的传递方式不同。

如果往深的去理解，无论什么函数，this是否被改变， 本质上，this 均指向触发函数运行时的那个对象。而在函数运行时，this 的值是不能被改变的。

//待补充



















参考：
[Web前端知识体系精简](http://www.cnblogs.com/onepixel/p/7021506.html)






