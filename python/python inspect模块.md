

inspect模块主要提供了四种用处：
* 对是否是模块，框架，函数等进行类型检查。
* 获取源码
* 获取类或函数的参数的信息
* 解析堆栈

## 1. 对是否是模块，框架，函数等进行类型检查 
## 2. 获取源码
## 3. 获取类或函数的参数的信息

先来看一个例子：
```py
# test
import inspect
def a(a, b=0, *c, d, e=1, **f):
    pass
aa = inspect.signature(a)
print("inspect.signature（fn)是:%s" % aa)
print("inspect.signature（fn)的类型：%s" % (type(aa)))
print("\n")

bb = aa.parameters
print("signature.paramerters属性是:%s" % bb)
print("ignature.paramerters属性的类型是%s" % type(bb))
print("\n")

for cc, dd in bb.items():
    print("mappingproxy.items()返回的两个值分别是：%s和%s" % (cc, dd))
    print("mappingproxy.items()返回的两个值的类型分别是：%s和%s" % (type(cc), type(dd)))
    print("\n")
    ee = dd.kind
    print("Parameter.kind属性是:%s" % ee)
    print("Parameter.kind属性的类型是:%s" % type(ee))
    print("\n")
    gg = dd.default
    print("Parameter.default的值是: %s" % gg)
    print("Parameter.default的属性是: %s" % type(gg))
    print("\n")


ff = inspect.Parameter.KEYWORD_ONLY
print("inspect.Parameter.KEYWORD_ONLY的值是:%s" % ff)
print("inspect.Parameter.KEYWORD_ONLY的类型是:%s" % type(ff))
```

运行结果：
inspect.signature（fn)是:(a, b=0, *c, d, e=1, **f)
inspect.signature（fn)的类型：<class 'inspect.Signature'>


signature.paramerters属性是:OrderedDict([('a', <Parameter "a">), ('b', <Parameter "b=0">), ('c', <Parameter "*c">), ('d', <Parameter "d">), ('e', <Parameter "e=1">), ('f', <Parameter "**f">)])
ignature.paramerters属性的类型是<class 'mappingproxy'>


mappingproxy.items()返回的两个值分别是：a和a
mappingproxy.items()返回的两个值的类型分别是：<class 'str'>和<class 'inspect.Parameter'>


Parameter.kind属性是:POSITIONAL_OR_KEYWORD
Parameter.kind属性的类型是:<enum '_ParameterKind'>


Parameter.default的值是: <class 'inspect._empty'>
Parameter.default的属性是: <class 'type'>


mappingproxy.items()返回的两个值分别是：b和b=0
mappingproxy.items()返回的两个值的类型分别是：<class 'str'>和<class 'inspect.Parameter'>


Parameter.kind属性是:POSITIONAL_OR_KEYWORD
Parameter.kind属性的类型是:<enum '_ParameterKind'>


Parameter.default的值是: 0
Parameter.default的属性是: <class 'int'>


mappingproxy.items()返回的两个值分别是：c和*c
mappingproxy.items()返回的两个值的类型分别是：<class 'str'>和<class 'inspect.Parameter'>


Parameter.kind属性是:VAR_POSITIONAL
Parameter.kind属性的类型是:<enum '_ParameterKind'>


Parameter.default的值是: <class 'inspect._empty'>
Parameter.default的属性是: <class 'type'>


mappingproxy.items()返回的两个值分别是：d和d
mappingproxy.items()返回的两个值的类型分别是：<class 'str'>和<class 'inspect.Parameter'>


Parameter.kind属性是:KEYWORD_ONLY
Parameter.kind属性的类型是:<enum '_ParameterKind'>


Parameter.default的值是: <class 'inspect._empty'>
Parameter.default的属性是: <class 'type'>


mappingproxy.items()返回的两个值分别是：e和e=1
mappingproxy.items()返回的两个值的类型分别是：<class 'str'>和<class 'inspect.Parameter'>


Parameter.kind属性是:KEYWORD_ONLY
Parameter.kind属性的类型是:<enum '_ParameterKind'>


Parameter.default的值是: 1
Parameter.default的属性是: <class 'int'>


mappingproxy.items()返回的两个值分别是：f和**f
mappingproxy.items()返回的两个值的类型分别是：<class 'str'>和<class 'inspect.Parameter'>


Parameter.kind属性是:VAR_KEYWORD
Parameter.kind属性的类型是:<enum '_ParameterKind'>


Parameter.default的值是: <class 'inspect._empty'>
Parameter.default的属性是: <class 'type'>


inspect.Parameter.KEYWORD_ONLY的值是:KEYWORD_ONLY
inspect.Parameter.KEYWORD_ONLY的类型是:<enum '_ParameterKind'>

总结：
* `inspect.signature（fn)`将返回一个`inspect.Signature`类型的对象，值为`fn`这个函数的所有参数

* `inspect.Signature`对象的`paramerters`属性是一个`mappingproxy`（映射）类型的对象，值为一个有序字典（Orderdict)。

    * 这个字典里的key是即为参数名，`str`类型
    * 这个字典里的value是一个`inspect.Parameter`类型的对象，根据我的理解，这个对象里包含的一个参数的各种信息

* `inspect.Parameter`对象的kind属性是一个_ParameterKind枚举类型的对象，值为这个参数的类型（可变参数，关键词参数，etc）
    * `POSITIONAL_ONLY `         位置参数
    * `KEYWORD_ONLY`             命名关键词参数
    * `VAR_POSITIONAL `          可选参数 `*args`
    * `VAR_KEYWORD`              关键词参数 `**kw`
    * `POSITIONAL_OR_KEYWORD`    位置或必选参数

* `inspect.Parameter`对象的default属性：如果这个参数有默认值，即返回这个默认值，如果没有，返回一个`inspect._empty`类。

## 4. 解析堆栈

## 参考

* [关于python中inspect模块的一些探究](http://blog.csdn.net/weixin_35955795/article/details/53053762)
