# Python Django Distinct On in different way

```python
def get_unfinished_payments():
    """Return payments older than specified time and without assigned order object."""
    ttl = settings.UNFINISHED_PAYMENT_TTL
    now = timezone.now()
    day_before = now - ttl
    newest = (
        Transaction.objects.filter(payment=OuterRef("pk"))
        .filter(
            kind__in=[TransactionKind.AUTH, TransactionKind.CAPTURE],
            is_success=True,
            action_required=False,
        )
        .order_by("-created")
    )
    payments = (
        Payment.objects.get_queryset()
        .filter(is_active=True, order=None)
        .annotate(newest_trx_date=Subquery(newest.values("created")[:1]))
        .filter(newest_trx_date__lte=day_before)
    )
    return payments
```