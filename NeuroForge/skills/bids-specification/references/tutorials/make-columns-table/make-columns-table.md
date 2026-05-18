# How To: Make Columns Table

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test whether expected columns are present and the requirement level is
applied correctly.
This should be robust with respect to schema format.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `bidsschematools.render`
- `bidsschematools.render.utils`

**Setup Required:**
```python
# Fixtures: schema_obj
```

## Step-by-Step Guide

### Step 1: '\n    Test whether expected columns are present and the requirement level is\n    applied correctly.\n    This should be robust with respect to schema format.\n    '

```python
'\n    Test whether expected columns are present and the requirement level is\n    applied correctly.\n    This should be robust with respect to schema format.\n    '
```

**Verification:**
```python
assert rendered_table[0].startswith('| **Column name**')
```

### Step 2: Assign rendered_table = tables.make_columns_table.split(...)

```python
rendered_table = tables.make_columns_table(schema_obj, 'modality_agnostic.Participants').split('\n')
```

**Verification:**
```python
assert rendered_table[1].startswith('|----------------')
```

### Step 3: Assign fields = value

```python
fields = schema_obj.rules.tabular_data.modality_agnostic.Participants.columns
```

**Verification:**
```python
assert len(rendered_table) == len(fields) + 3
```

### Step 4: Assign spec = value

```python
spec = fields[field]
```

**Verification:**
```python
assert render_row.startswith(f'| [{field}](')
```

### Step 5: Assign level = spec

```python
level = spec
```

**Verification:**
```python
assert level.upper() in render_row
```

### Step 6: Assign level_addendum = ''

```python
level_addendum = ''
```

**Verification:**
```python
assert level_addendum.split('\n')[0] in render_row
```

### Step 7: Assign description_addendum = ''

```python
description_addendum = ''
```

**Verification:**
```python
assert description_addendum.split('\n')[0] in render_row
```

### Step 8: Assign level = value

```python
level = spec['level']
```

### Step 9: Assign level_addendum = spec.get.replace(...)

```python
level_addendum = spec.get('level_addendum', '').replace('required', 'REQUIRED')
```

### Step 10: Assign description_addendum = spec.get(...)

```python
description_addendum = spec.get('description_addendum', '')
```


## Complete Example

```python
# Setup
# Fixtures: schema_obj

# Workflow
'\n    Test whether expected columns are present and the requirement level is\n    applied correctly.\n    This should be robust with respect to schema format.\n    '
rendered_table = tables.make_columns_table(schema_obj, 'modality_agnostic.Participants').split('\n')
assert rendered_table[0].startswith('| **Column name**')
assert rendered_table[1].startswith('|----------------')
fields = schema_obj.rules.tabular_data.modality_agnostic.Participants.columns
assert len(rendered_table) == len(fields) + 3
for field, render_row in zip(fields, rendered_table[2:-1]):
    assert render_row.startswith(f'| [{field}](')
    spec = fields[field]
    if isinstance(spec, str):
        level = spec
        level_addendum = ''
        description_addendum = ''
    else:
        level = spec['level']
        level_addendum = spec.get('level_addendum', '').replace('required', 'REQUIRED')
        description_addendum = spec.get('description_addendum', '')
    assert level.upper() in render_row
    assert level_addendum.split('\n')[0] in render_row
    assert description_addendum.split('\n')[0] in render_row
```

## Next Steps


---

*Source: test_render_tables.py:115 | Complexity: Advanced | Last updated: 2026-05-18*