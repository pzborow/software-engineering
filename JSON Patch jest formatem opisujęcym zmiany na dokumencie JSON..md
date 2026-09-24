# JSON Patch jest formatem opisujęcym zmiany na dokumencie JSON.

JSON Patch jest formatem opisujęcym zmiany na dokumencie JSON.

Oryginalny dokument
```.json
{
  "baz": "qux",
  "foo": "bar"
}
```

Łatka
```.json
[
  { "op": "replace", "path": "/baz", "value": "boo" },
  { "op": "add", "path": "/hello", "value": ["world"] },
  { "op": "remove", "path": "/foo" }
]
```

I rezultat
```.json
{
  "baz": "boo",
  "hello": ["world"]
}
```
https://jsonpatch.com/