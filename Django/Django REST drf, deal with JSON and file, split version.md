# Django REST drf, deal with JSON and file, split version

Split version of [Django REST drf, deal with JSON and file](:/9a246d9b436f4defb569155f00561b04).

```python
#models.py
from django.db import models


class Profile(models.Model):
    name = models.CharField(max_length=200)
    bio = models.TextField(blank=True)

    pic = models.ImageField(upload_to='pics', blank=True)

    updated_at = models.DateTimeField(auto_now=True)
    created_at = models.DateTimeField(auto_now_add=True)
```

```python
# serializers.py
from rest_framework import serializers

from .models import Profile


class ProfileSerializer(serializers.ModelSerializer):
    class Meta:
        model = Profile
        fields = ['name', 'bio', 'pic']
        read_only_fields = ['pic']


class ProfilePicSerializer(serializers.ModelSerializer):
    class Meta:
        model = Profile
        fields = ['pic']
```

```python
# views.py
from rest_framework import parsers
from rest_framework import response
from rest_framework import status
from rest_framework import viewsets

from .models import Profile
from .serializers import ProfilePicSerializer
from .serializers import ProfileSerializer


class ProfileViewSet(viewsets.ModelViewSet):
    serializer_class = ProfileSerializer
    queryset = Profile.objects.all()

    @decorators.action(
        detail=True,
        methods=['PUT'],
        serializer_class=ProfilePicSerializer,
        parser_classes=[parsers.MultiPartParser],
    )
    def pic(self, request, pk):
        obj = self.get_object()
        serializer = self.serializer_class(obj, data=request.data,
                                           partial=True)
        if serializer.is_valid():
            serializer.save()
            return response.Response(serializer.data)
        return response.Response(serializer.errors,
                                 status.HTTP_400_BAD_REQUEST)
```

```python
# urls.py
from django.urls import path


router = routers.DefaultRouter()

router.register(r'profiles', views.ProfileViewSet)

urlpatterns = [
    path(r'api/v1/', include(router.urls)),
]
```