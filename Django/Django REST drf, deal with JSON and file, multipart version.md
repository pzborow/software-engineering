# Django REST drf, deal with JSON and file, multipart version

Multipart version of  [Django REST drf, deal with JSON and file](:/9a246d9b436f4defb569155f00561b04).

```python
#models.py
class Posts(models.Model):
    id = models.UUIDField(default=uuid.uuid4, primary_key=True, editable=False)
    caption = models.TextField(max_length=1000)
    media = models.ImageField(blank=True, default="", upload_to="posts/")
    tags = models.ManyToManyField('Tags', related_name='posts')
```

```python
# views.py
class PostsViewset(viewsets.ModelViewSet):
    serializer_class = PostsSerializer
    parser_classes = (MultipartJsonParser, parsers.JSONParser)
    queryset = Posts.objects.all()
    lookup_field = 'id'
```


```python
#utils.py
from django.http import QueryDict
import json
from rest_framework import parsers


class MultipartJsonParser(parsers.MultiPartParser):
    def parse(self, stream, media_type=None, parser_context=None):
        result = super().parse(
            stream,
            media_type=media_type,
            parser_context=parser_context
        )
        data = {}
        # find the data field and parse it
        data = json.loads(result.data["data"])
        qdict = QueryDkkict('', mutable=True)
        qdict.update(data)
        return parsers.DataAndFiles(qdict, result.files)
```

There is [another approach](https://stackoverflow.com/questions/20473572/django-rest-framework-file-upload/50514022#50514022) to parse each key

```python
class MultipartJsonParser(parsers.MultiPartParser):

    def parse(self, stream, media_type=None, parser_context=None):
        result = super().parse(
            stream,
            media_type=media_type,
            parser_context=parser_context
        )
        data = {}

        # for case1 with nested serializers
        # parse each field with json
        for key, value in result.data.items():
            if type(value) != str:
                data[key] = value
                continue
            if '{' in value or "[" in value:
                try:
                    data[key] = json.loads(value)
                except ValueError:
                    data[key] = value
            else:
                data[key] = value

        # for case 2
        # find the data field and parse it
        data = json.loads(result.data["data"])

        qdict = QueryDict('', mutable=True)
        qdict.update(data)
        return parsers.DataAndFiles(qdict, result.files)
```

After struggling with list, final version of parser looks like
```python

class MultipartJsonParser(parsers.MultiPartParser):
    def parse(self, stream, media_type=None, parser_context=None):
        result = super().parse(
            stream,
            media_type=media_type,
            parser_context=parser_context
        )
        qdict = QueryDict('', mutable=True)
        data = {}
        # find the data field and parse it
        data = json.loads(result.data["data"])

        data_not_list = {key: value for key, value in data.items() if not isinstance(value, list)}
        qdict.update(data_not_list)

        data_list = {key: value for key, value in data.items() if isinstance(value, list)}
        for key, value in data_list.items():
            qdict.setlist(key, value)
        return parsers.DataAndFiles(qdict, result.files)
```
Important part is to setting list by `setlist` method, otherwise you end up with nested lists.

![9a118b16823967ff68a2c9b535e54768.png](:/c321d86a878a4febb048103b7824bb46)