# How To: Entity Order

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check the order of the entities of the suffix group of each datatype
and lists those that are out of order.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `collections.abc`
- `pytest`

**Setup Required:**
```python
# Fixtures: schema_obj
```

## Step-by-Step Guide

### Step 1: 'Check the order of the entities of the suffix group of each datatype\n    and lists those that are out of order.\n    '

```python
'Check the order of the entities of the suffix group of each datatype\n    and lists those that are out of order.\n    '
```

### Step 2: Assign status_ok = True

```python
status_ok = True
```

### Step 3: Assign entities_order = value

```python
entities_order = schema_obj.rules.entities
```

### Step 4: Call print()

```python
print(f'Checking {key}')
```

### Step 5: Assign entities = list(...)

```python
entities = list(group.get('entities', ()))
```

### Step 6: Assign correct_order = sorted(...)

```python
correct_order = sorted(entities, key=lambda x: entities_order.index(x))
```

### Step 7: Assign status_ok = False

```python
status_ok = False
```

### Step 8: Call warnings.warn()

```python
warnings.warn(f'\n\nfilename rule {key} has entities out-of-order:\n                - got: {entities}\n                - should be: {correct_order}\n                ')
```


## Complete Example

```python
# Setup
# Fixtures: schema_obj

# Workflow
'Check the order of the entities of the suffix group of each datatype\n    and lists those that are out of order.\n    '
status_ok = True
entities_order = schema_obj.rules.entities
for key, group in schema_obj.rules.files.items(level=2):
    print(f'Checking {key}')
    entities = list(group.get('entities', ()))
    correct_order = sorted(entities, key=lambda x: entities_order.index(x))
    if entities != correct_order:
        status_ok = False
        warnings.warn(f'\n\nfilename rule {key} has entities out-of-order:\n                - got: {entities}\n                - should be: {correct_order}\n                ')
if not status_ok:
    raise RuntimeError('Some suffix groups have their entities out of order. See warnings above.')
```

## Next Steps


---

*Source: test_rules.py:116 | Complexity: Advanced | Last updated: 2026-05-18*