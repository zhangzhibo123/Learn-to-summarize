### 三层装饰器

````python
def outer(*args, **kwargs):
    print(args)
    print(kwargs)
    def decorator(fun):
        def inner(n):
            print(args)
            print(kwargs)
            fun(n)
        return inner
    return decorator
# @装饰器可以传递参数  传递参数的在@装饰器(实参,实参)
@outer(1, 2, 3, 4, a=11, b=12)
def fun(n1):
    print(n1)
fun(10)
````

### 单例模式

````python
class Shop:
    __instance = None

    def __new__(cls, *args, **kwargs):
        if cls.__instance is None:
            cls.__instance = object.__new__(cls) # object super()
        return cls.__instance
````



