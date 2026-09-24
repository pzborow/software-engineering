# Model
```python
from django.db import models

class Sauce(models.Model):
    name = models.CharField(max_length=100)

    def __str__(self):
        return self.name

class Sandwich(models.Model):
    name = models.CharField(max_length=100)
    sauces = models.ManyToManyField(Sauce, related_name="sandwiches")

    def __str__(self):
        return self.name
```

# Dodawanie i usuwanie
```ipython

>>> chicken_teriyaki_sandwich = Sandwich.objects.create(name="Chicken Teriyaki Sandwich")
>>> bbq_sauce = Sauce.objects.create(name="Barbeque")
>>> mayo_sauce = Sauce.objects.create(name="Mayonnaise")
>>> 
>>> chicken_teriyaki_sandwich.sauces.add(bbq_sauce)
>>> chicken_teriyaki_sandwich.sauces.add(mayo_sauce)
>>> p2.article_set.remove(a5)
>>> a4.publications.clear()
>>> p2.article_set.add(a4, a5)
```

# Filtrowanie

```ipython
>>> Article.objects.filter(publications__id=1)
<QuerySet [<Article: Django lets you build Web apps easily>, <Article: NASA uses Python>]>
>>> Article.objects.filter(publications__pk=1)
<QuerySet [<Article: Django lets you build Web apps easily>, <Article: NASA uses Python>]>
>>> Article.objects.filter(publications=1)
<QuerySet [<Article: Django lets you build Web apps easily>, <Article: NASA uses Python>]>
>>> Article.objects.filter(publications=p1)
<QuerySet [<Article: Django lets you build Web apps easily>, <Article: NASA uses Python>]>

>>> Article.objects.filter(publications__title__startswith="Science")
<QuerySet [<Article: NASA uses Python>, <Article: NASA uses Python>]>

>>> Article.objects.filter(publications__title__startswith="Science").distinct()
<QuerySet [<Article: NASA uses Python>]>

>>> Article.objects.exclude(publications=p2)
<QuerySet [<Article: Django lets you build Web apps easily>]>
```

[More info](http://www.matrix.umcs.lublin.pl/DOC/python-django-doc/html/topics/db/examples/many_to_many.html)