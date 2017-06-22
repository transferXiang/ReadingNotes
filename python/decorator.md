# 装饰器
装饰器的作用在于它能够在不修改原有业务逻辑的情况下对代码进行扩展。  
哪些地方适合用装饰器呢？但凡是在多个地方出现雷同的代码块，且这些代码与核心业务没有直接关联的都可以用装饰器来代替，装饰器不仅能减少代码量，还使得代码逻辑更清晰、可读性更强，你只需专注于业务逻辑处理就行了。这一点与设计模式中的装饰器思路是完全一致的。
## 无参数装饰器
为了说明这个装饰器的作用，下面举个例子来对它进行分析：假设有一个函数`foo()`，该函数的作用是用来输出一个日志。
``` python
def foo():
    print('hi~')
```
假设某天需求发生了改变，需要在日志前后加上其他的日志如:
``` python
def new_foo_1():
    print('han mei mei say:')
    print('hi~')
    print('to lily')
```
从这里看到，我们只能新写一个函数才能够满足新的需求。在python中一切皆对象，因此函数也是一个对象（相信大家应该都听说过函数式编程吧）。那么可以通过以下方式进行改造：
``` python
def foo():
    print('hi~')

def new_foo_2(func):
    print('han mei mei say:')
    func()
    print('to lily')

new_foo_2(foo)
```
这时我们发现当我们执行`new_foo_2`时，立即就执行了`foo`函数，且客户端代码调用时调用的是`new_foo_2`而非之前的`foo`函数名，这一点是非常不友好的。因此可以进一步的进行优化。
``` python
def foo():
    print('hi~')

def new_foo_3(func):
    def inner_fun():
        print('han mei mei say:')
        func()
        print('to lily')
    return inner_fun

foo = new_foo_3(foo)

foo()
```
到了这一步可以发现客户端的代码没有发生任何变化，且满足了新的需求。注意`foo = new_foo_3(foo)`修改了`foo`的指向，目前指向的其实是`inner_fun`。但每次这样写是不是非常的丑陋，且不实用，因此 Python 提供了很好的语法。最终引入了我们的装饰器：
``` python
def new_foo_4(func):
    def inner_fun():
        print('han mei mei say:')
        func()
        print('to lily')
    return inner_fun

@new_foo_4
def foo():
    print('hi~')

foo()
```
注意这里的`@new_foo_4`就是装饰器的用法。

## 带参数装饰器
上面我们看到的每次都是`han mei mei`对`lily` say hi。那么我们想改一改，或者自定义该怎么办呢，那就该我们带参数的装饰器出场了。
``` python
def new_foo_5(person_a, person_b):
    def decorator(func):
        def inner_fun():
            print('{person} say:'.format(person=person_a))
            func()
            print('to {person}'.format(person=person_b))
        return inner_fun
    return decorator

@new_foo_5('han mei mei', 'lily')
def foo():
    print('hi~')

foo()
```

## 几类装饰器模式
### 装饰器无参数，被装饰函数无参数
``` python
def decorator(func):
    def wrapper():
        ...
        func()
        ...
    return wrapper

@decorator
def foo():
    pass
```
### 装饰器无参数，被装饰函数带参数
``` python
def decorator(func):
    def wrapper(arg):
        ...
        func(arg)
        ...
    return wrapper

@decorator
def foo(arg):
    pass
```
### 装饰器带参数，被装饰函数无参数
``` python
def decorator(arg):
    def wrapper_out(func):
        def wrapper():
            ...
            func()
            ...
        return wrapper
    return wrapper_out

@decorator(arg)
def foo():
    pass
```
### 装饰器带参数，被装饰函数带参数
``` python
def decorator(arg):
    def wrapper_out(func):
        def wrapper(func_arg):
            ...
            func(func_arg)
            ...
        return wrapper
    return wrapper_out

@decorator(arg)
def foo(func_arg):
    pass
```
---
**参考资料：**
* [装饰器为什么难以理解？](http://mp.weixin.qq.com/s/0LIzJr59Xx0af3kN0CDZcA)
* [Python装饰器为什么难理解：写个带参数的装饰器](http://mp.weixin.qq.com/s/TDFDPZk7PJ9TsRc2l17-nw)
* [Python 装饰器](http://python.jobbole.com/82344/)
