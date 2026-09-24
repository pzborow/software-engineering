# Decorator and preserv singature

```.python
import functools


def args_as_ints(func):
    @functools.wraps(func)
    def wrapper(*args, **kwargs):
        args = [int(x) for x in args]
        kwargs = dict((k, int(v)) for k, v in kwargs.items())
        return func(*args, **kwargs)
    return wrapper


@args_as_ints
def funny_function(x, y, z=3):
    """Computes x*y + 2*z"""
    return x*y + 2*z


print(funny_function("3", 4.0, z="5"))
# 22
help(funny_function)
# Help on function funny_function in module __main__:
#
# funny_function(x, y, z=3)
#     Computes x*y + 2*z
```