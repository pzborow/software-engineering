# Update Related field in Django DRF Rest Serializer 

Suppose following relates models: asset and langage. If you wand to write serializer, which return nested language in asset endpoint, but you want not to change language it self but only change relation beetween them.

One [solution](https://stackoverflow.com/questions/26561640/django-rest-framework-read-nested-data-write-integer_) is to write two fields for asset serializer as below

```python
class AssetSerializer(serializers.ModelSerializer):
    language = LanguageSerializer(read_only=True)
    langague_id = serializers.PrimaryKeyRelatedField(
        write_only=True,
        source='language',
        queryset=Language.objects.all())

    class Meta:
        model = Pin
        fields = ('id', 'language', 'language_id',)
```

and for M2M field

```python
class AssetSerializer(serializers.ModelSerializer):
    languages = LanguageSerializer(many=True, read_only=True)
    language_ids = serializers.PrimaryKeyRelatedField(
        many=True,
        write_only=True,
        source='languages',
        queryset=Language.objects.all())
    
	class Meta:
        model = Item
        fields = ('id', 'langages', 'language_ids',)
```

[Sacond approach](https://stackoverflow.com/questions/29950956/drf-simple-foreign-key-assignment-with-nested-serializers) is to change serializer in the fly. Field name is the same, bu different on update
```python
from rest_framework import serializers


class RelatedFieldAlternative(serializers.PrimaryKeyRelatedField):
    def __init__(self, **kwargs):
        self.serializer = kwargs.pop('serializer', None)
        if self.serializer is not None and not issubclass(self.serializer, serializers.Serializer):
            raise TypeError('"serializer" is not a valid serializer class')

        super().__init__(**kwargs)

    def use_pk_only_optimization(self):
        return False if self.serializer else True

    def to_representation(self, instance):
        if self.serializer:
            return self.serializer(instance, context=self.context).data
        return super().to_representation(instance)
```
	
	usage
	
```python
class AssetSerializer(ModelSerializer):
   language = RelatedFieldAlternative(queryset=Language.objects.all(), serializer=LanguageSerializer)

    class Meta:
        model = Parent
        fields = '__all__'
```