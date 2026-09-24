# Context Manager

"Context Managers" are any of those Python objects that you can use in a with statement.

In Python, you can create Context Managers by creating a class with two methods: __enter__() and __exit__().

Another way to create a context manager is with:

@contextlib.contextmanager or
@contextlib.asynccontextmanager
using them to decorate a function with a single yield.