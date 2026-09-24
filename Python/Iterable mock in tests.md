# Iterable mock in tests

```python
@patch.object(Path, "rglob")
def test_validation_directory_path(self, rglob):
    ...
    rglob.return_value.__iter__.return_value = iter([
        Path('/first_path'),
        Path('/second_path')
    ])
    ...
    validate_file.assert_any_call(Path('/first_path'))
    validate_file.assert_any_call(Path('/second_path'))
```