# Python debug ipdb pytest

run pytest with -s option (turn off capture output). For example:

```bash
py.test -s my_test.py
```

and then in my_test.py:

```python
import ipdb;
ipdb.set_trace()
```