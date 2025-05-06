
# 🧠 Django ORM Lookup Cheat Sheet

## 🔗 Relaciones (`ForeignKey`, `OneToOne`, `ManyToMany`)

| **Lookup**                              | **¿Qué hace?**                                      | **Ejemplo**                                       |
|-----------------------------------------|-----------------------------------------------------|---------------------------------------------------|
| `field__relatedfield`                   | Accede a un campo relacionado                       | `permission__content_type__model="user"`          |
| `field__relatedfield__in`               | Verifica si el valor está en una lista              | `content_type__model__in=["user", "zona"]`        |
| `user__groups__name="Admin"`            | Usuarios con grupo llamado "Admin"                  |                                                   |
| `group__permissions__codename="add_user"` | Grupos con el permiso `add_user`                   |                                                   |

## 🔍 Búsqueda y comparación

| **Lookup**      | **¿Qué hace?**                                | **Ejemplo**                     |
|------------------|------------------------------------------------|---------------------------------|
| `exact`          | Igual a (`=`)                                  | `name__exact="Oscar"`           |
| `iexact`         | Igual (sin importar mayúsculas)                | `email__iexact="ADMIN@MAIL.COM"`|
| `contains`       | Contiene (sensible a mayúsculas)               | `name__contains="osc"`          |
| `icontains`      | Contiene (sin importar mayúsculas)             | `name__icontains="osc"`         |
| `in`             | Está en una lista                              | `id__in=[1,2,3]`                |
| `startswith`     | Comienza con                                   | `name__startswith="Adm"`        |
| `istartswith`    | Comienza con (sin importar mayúsculas)         | `name__istartswith="adm"`       |
| `endswith`       | Termina con                                    | `name__endswith="zone"`         |

## 📅 Lookups con fechas

| **Lookup**      | **¿Qué hace?**                   | **Ejemplo**                               |
|------------------|----------------------------------|-------------------------------------------|
| `date__year`     | Año específico                  | `created_at__year=2023`                   |
| `date__gte`      | Fecha mayor o igual             | `created_at__date__gte="2023-01-01"`      |
| `date__lt`       | Fecha menor                     | `created_at__date__lt="2023-12-31"`       |

## ✅ Booleanos y nulos

| **Lookup**     | **¿Qué hace?**                     | **Ejemplo**                     |
|----------------|------------------------------------|---------------------------------|
| `isnull`       | ¿Es nulo?                          | `last_login__isnull=True`      |
| `booleanfield` | ¿Es verdadero o falso?             | `is_active=True`               |

## 🧠 Avanzado: `Q()` y `exclude()`

### 🔁 `Q()` para condiciones `OR`

```python
from django.db.models import Q

User.objects.filter(
    Q(username__icontains="admin") | Q(email__icontains="admin")
)
```

### 🚫 `exclude()` para hacer `NOT`

```python
Permission.objects.exclude(content_type__model__in=["tenant", "session"])
```

## 📚 Documentación útil

- [Lookups que cruzan relaciones](https://docs.djangoproject.com/en/stable/topics/db/queries/#lookups-that-span-relationships)
- [Field Lookups completos](https://docs.djangoproject.com/en/stable/ref/models/querysets/#field-lookups)
- [Q Objects para búsquedas complejas](https://docs.djangoproject.com/en/stable/topics/db/queries/#complex-lookups-with-q-objects)
