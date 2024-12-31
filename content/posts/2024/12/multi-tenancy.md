---
title: "Multitenancy in Django with a Custom ORM"
date: 2024-12-30
description: "Implementing multitenancy in Django using a mixin class."
draft: false
---

Managing multitenant applications can be challenging, especially when handling tenant specific data efficiently. I have worked with a solution in Django that made a PostgreSQL database multitenant, leveraging a custom Django ORM implementation. Here’s how it works and why it’s intuitive for developers.

### The Multitenancy Challenge ###

Multitenancy involves isolating data for different clients or tenants within the same application and database. A common method uses a unique tenant identifier on relevant database records. While this works, it often results in repetitive boilerplate code.

### The Solution: Custom ORM with a Mixin Class ###

To simplify multitenancy, I created a custom mixin class in Python. This mixin adds a tenant_id field automatically to models and integrates seamlessly with Django’s ORM. Additionally, it ensures every instance has a tenant_id assigned. Here’s how it looks:

```python
from django.db import models

class TenantMixin(models.Model):
    tenant_id = models.UUIDField()

    def save(self, *args, **kwargs):
        if not self.tenant_id:
            raise ValueError("tenant_id must be set before saving the object.")
        super().save(*args, **kwargs)

    class Meta:
        abstract = True
```

### Overriding the Query Function ### 

To make tenant filtering automatic and eliminate the need for explicit calls in Django you can customize the query process by creating a custom queryset manager. And have it filter by tenant_id.:

```python
from django.db.models import QuerySet

class TenantQuerySet(QuerySet):
    def _filter_by_tenant(self):
        return self.filter(tenant_id=self.model.current_tenant_id)

    def all(self):
        return super().all()._filter_by_tenant()

class TenantManager(models.Manager):
    def get_queryset(self):
        return TenantQuerySet(self.model, using=self._db)

class Order(TenantMixin):
    objects = TenantManager()
    product_name = models.CharField(max_length=255)

# Example query
orders = Order.objects.all()
```

This implementation requires a `tenant_id` stored directly on each Order (Or tenant specified) object. The private `_filter_by_tenant` method ensures queries automatically include the correct `tenant_id`.

### Benefits ###

1. Automatic Filtering: No need for explicit tenant filtering in queries.
2. Cleaner Code: Reduces boilerplate and ensures tenant isolation by default.
3. Intuitive API: Developers can focus on business logic without extra steps.
4. Scalability: Works seamlessly with PostgreSQL’s indexing and performance features.

### Drawbacks ###

While this approach is powerful, there are some considerations:

1. Validation Overhead: The `tenant_id` requirement might complicate data handling during migrations or with default records.
2. Hidden Behavior: Automatic filtering may obscure logic, making debugging more challenging.
3. Testing Complexity: Ensuring proper tenant data setup for tests can require additional effort.
4. Performance Impact: Depending on query complexity, adding tenant filtering to every query could slightly impact performance.

### Final Thoughts ###

This approach not only simplifies multitenancy but also ensures the implementation is clean, maintainable, and developer friendly. It’s a great example of how Django’s extensibility can solve complex problems elegantly.