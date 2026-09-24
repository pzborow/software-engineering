# Django REST drf, deal with JSON and file

1. **Encode the binary** data (e.g. Base64) and pass it as a value of a key in the JSON document. There are a couple of drawbacks with this approach: it increases the size of the uploaded files, reduces API output readability, prevents servers from streaming files to disk, and the encoding/decoding adds processing overhead.
2. multipart/form-data can be used to handle **multiple documents in a single request.** While easy to design and implement, this solution introduces different content-types for very similar endpoints (i.e. application/json for /profiles but multipart/form-data for /posts if the latter accepts a cover photo) and handling the JSON-encoded part of the body requires some documentation (i.e. specifying that the JSON-encoded data should be sent in a form field named x).
3. **Split the functionality** into two or more separate requests to handle resources that are made up of a mix of binary and JSON content. This approach may force you to rethink your structure a little bit, creation isn’t “atomic”, and it will require a little bit of work (e.g. prune unused metadata or uploaded files, multiple serializers, additional endpoints).

Generally prefer option three despite the drawbacks. The approach can be applied in a couple of different ways.

[Django REST drf, deal with JSON and file, split version](:/b585c9c2f28e426b920bd0b2fbe07f68)

[more](https://www.trell.se/blog/file-uploads-json-apis-django-rest-framework/)