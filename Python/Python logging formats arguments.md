# Python logging formats arguments

```python
logging, use args, similar to string interpolation:
ok: logger.debug('found %i', q.count())
bad: logger.debug(f'found {q.count()}')
bad: logger.debug('found %r' % q.count())
```
because logging is conditionally lazy,
