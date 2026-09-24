# Python pretty printer

```python
stuff = ['spam', 'eggs', 'lumberjack', 'knights', 'ni']
stuff.insert(0, stuff[:])

import pprint

pp = pprint.PrettyPrinter(indent=4)
pp.pprint(stuff)
```