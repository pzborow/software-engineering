# Thread safe local model variable with context manager

```python
import threading


class SomeObject(ABC):
    def __init__(self) -> None:
        super().__init__()
        self._thread_data = threading.local()
        self._thread_data.a_list = []

    @contextmanager
    def set_current_something(self, something):
        self._thread_data.a_list.append(something)
        yield self
        self._thread_data.current_system.pop()

    @property
    def current_something(self):
        if len(self._thread_data.something) > 0:
            return self._thread_data.something[-1]
        return None

"""