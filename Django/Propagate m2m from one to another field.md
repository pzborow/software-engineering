# Propagate m2m from one to another field

```python
def asset_language_changed(sender, instance: Asset, action, reverse, model: Type[Language], pk_set: Set[int], **kwargs):
    asset = instance
    if asset.owner is None:
        return
    languages = model.objects.filter(pk__in=pk_set)

    if action == 'post_add':
        try:
            plvs = ProductLanguageVersion.objects.filter(product=asset.owner, language__in=languages)
            asset.product_language_versions.add(*plvs)
        except asset.DoesNotExist:
            pass
    elif action == 'post_remove':
        try:
            plvs = ProductLanguageVersion.objects.filter(product=asset.owner, language__in=languages)
            asset.product_language_versions.remove(*plvs)
        except asset.DoesNotExist:
            pass

m2m_changed.connect(asset_language_changed, sender=Asset.languages.through)
```