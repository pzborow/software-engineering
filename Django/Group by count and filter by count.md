# Group by count and filter by count

```ipython
In [12]: Project.objects.values('manufacturer__name', 'name').annotate(count=Count(['manufacturer', 'name'])).filter(count__gt=1)
Out[12]: <ProjectQuerySet [{'manufacturer__name': 'Wella', 'name': 'Wella Professionals Old', 'count': 4}]>
In [13]: str(Project.objects.values('manufacturer__name', 'name').annotate(count=Count(['manufacturer', 'name'])).filter(count__gt=1).query)
Out[13]: 'SELECT "manufacturers_manufacturer"."name", "projects_project"."name", COUNT([\'manufacturer\', \'name\']) AS "count" FROM "projects_project" INNER JOIN "manufacturers_manufacturer" ON ("projects_project"."manufacturer_id" = "manufacturers_manufacturer"."id") WHERE "projects_project"."deleted_at" IS NULL GROUP BY "manufacturers_manufacturer"."name", "projects_project"."name" HAVING COUNT([\'manufacturer\', \'name\']) > 1'

```