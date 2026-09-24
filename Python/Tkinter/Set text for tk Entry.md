# Set text for tk Entry

```python
entry = tk.Entry(root)
new_text = "Example text"
entry.delete(0, tk.END)
entry.insert(0, new_text)
```

```python
entry_text = tk.StringVar()
entry = tk.Entry(root, textvariable=entry_text)
new_text = "Example text"
entry_text.set(new_text)
```