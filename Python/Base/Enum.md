# Enum

To zbiór symbolicznych nazw (elementów) powiązanych z unikalnymi wartościami

```.python
from enum import Enum

class Tags(Enum):
    items = "items"
    users = "users"
	
print(Tags.items.value)
```

https://docs.python.org/3/library/enum.html