# Create model with FileField from console

```python
from django.core.files.base import ContentFile, File

# Using File
with open('/path/to/file') as f:
    product.image.save(new_name, File(f))

# Using ContentFile
product.image.save(new_name, ContentFile('A string with the file content'))
```