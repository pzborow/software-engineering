# Type checking and import problem

`typing.TYPE_CHECKING`

A special constant that is assumed to be True by 3rd party static type checkers. It is False at runtime. Usage:

```python
if TYPE_CHECKING:
    import expensive_mod

def fun(arg: 'expensive_mod.SomeType') -> None:
    local_var: expensive_mod.AnotherType = other_fun()
```

The first type annotation must be enclosed in quotes, making it a “forward reference”, to hide the expensive_mod reference from the interpreter runtime. Type annotations for local variables are not evaluated, so the second annotation does not need to be enclosed in quotes.