# How To: Make Sidecar Table

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test whether expected metadata fields are present and the requirement level is
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

### Step 1: '\n    Test whether expected metadata fields are present and the requirement level is\n    applied correctly.\n    This should be robust with respect to schema format.\n    '

```python
'\n    Test whether expected metadata fields are present and the requirement level is\n    applied correctly.\n    This should be robust with respect to schema format.\n    '
```

**Verification:**
```python
assert rendered_table[0].startswith('| **Key name**')
```

### Step 2: Assign rendered_table = tables.make_sidecar_table.split(...)

```python
rendered_table = tables.make_sidecar_table(schema_obj, 'mri.MRISpatialEncoding').split('\n')
```

**Verification:**
```python
assert rendered_table[1].startswith('|-------------')
```

### Step 3: Assign fields = value

```python
fields = schema_obj.rules.sidecars.mri.MRISpatialEncoding.fields
```

**Verification:**
```python
assert len(rendered_table) == len(fields) + 2
```

### Step 4: Assign spec = value

```python
spec = fields[field]
```

**Verification:**
```python
assert render_row.startswith(f'| [{field}](')
```

### Step 5: Assign level = normalize_requirements(...)

```python
level = normalize_requirements(spec)
```

**Verification:**
```python
assert f'| {level}' in render_row
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

### Step 8: Assign level = normalize_requirements(...)

```python
level = normalize_requirements(spec['level'])
```

### Step 9: Assign level_addendum = normalize_requirements(...)

```python
level_addendum = normalize_requirements(spec.get('level_addendum', ''))
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
'\n    Test whether expected metadata fields are present and the requirement level is\n    applied correctly.\n    This should be robust with respect to schema format.\n    '
rendered_table = tables.make_sidecar_table(schema_obj, 'mri.MRISpatialEncoding').split('\n')
assert rendered_table[0].startswith('| **Key name**')
assert rendered_table[1].startswith('|-------------')
fields = schema_obj.rules.sidecars.mri.MRISpatialEncoding.fields
assert len(rendered_table) == len(fields) + 2
for field, render_row in zip(fields, rendered_table[2:]):
    assert render_row.startswith(f'| [{field}](')
    spec = fields[field]
    if isinstance(spec, str):
        level = normalize_requirements(spec)
        level_addendum = ''
        description_addendum = ''
    else:
        level = normalize_requirements(spec['level'])
        level_addendum = normalize_requirements(spec.get('level_addendum', ''))
        description_addendum = spec.get('description_addendum', '')
    assert f'| {level}' in render_row
    assert level_addendum.split('\n')[0] in render_row
    assert description_addendum.split('\n')[0] in render_row
```

## Next Steps


---

*Source: test_render_tables.py:56 | Complexity: Advanced | Last updated: 2026-05-18*