# How To: Valid Sidecar Field

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check sidecar fields actually exist in the metadata listed in the schema.

Test failures are usually due to typos.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `__future__`
- `collections.abc`
- `functools`
- `pytest`
- `pyparsing.exceptions`
- `expressions`
- `types`

**Setup Required:**
```python
# Fixtures: schema_obj
```

## Step-by-Step Guide

### Step 1: 'Check sidecar fields actually exist in the metadata listed in the schema.\n\n    Test failures are usually due to typos.\n    '

```python
'Check sidecar fields actually exist in the metadata listed in the schema.\n\n    Test failures are usually due to typos.\n    '
```

**Verification:**
```python
assert name.split('.', 2)[1] in field_names, f'Bad field in {expr_type}: {name} ({key})'
```

### Step 2: Assign field_names = value

```python
field_names = {field.name for field in schema_obj.objects.metadata.values()}
```

**Verification:**
```python
assert name.split('.', 2)[1] in field_or_column_names, f'Bad field in {expr_type}: {name} ({key})'
```

### Step 3: Assign column_names = value

```python
column_names = {column.name for column in schema_obj.objects.columns.values()}
```

### Step 4: Assign field_or_column_names = value

```python
field_or_column_names = field_names | column_names
```

### Step 5: Assign ast = value

```python
ast = expression.parse_string(expr)[0]
```

**Verification:**
```python
assert name.split('.', 2)[1] in field_names, f'Bad field in {expr_type}: {name} ({key})'
```


## Complete Example

```python
# Setup
# Fixtures: schema_obj

# Workflow
'Check sidecar fields actually exist in the metadata listed in the schema.\n\n    Test failures are usually due to typos.\n    '
field_names = {field.name for field in schema_obj.objects.metadata.values()}
column_names = {column.name for column in schema_obj.objects.columns.values()}
field_or_column_names = field_names | column_names
for key, rule in walk_schema(schema_obj.rules, lambda k, v: isinstance(v, Mapping) and v.get('selectors')):
    for expr_type in ('selector', 'check'):
        for expr in rule.get(f'{expr_type}s', []):
            ast = expression.parse_string(expr)[0]
            for name in find_names(ast):
                if name.startswith('json.'):
                    assert name.split('.', 2)[1] in field_names, f'Bad field in {expr_type}: {name} ({key})'
                elif name.startswith('sidecar.'):
                    assert name.split('.', 2)[1] in field_or_column_names, f'Bad field in {expr_type}: {name} ({key})'
```

## Next Steps


---

*Source: test_expressions.py:108 | Complexity: Intermediate | Last updated: 2026-05-18*