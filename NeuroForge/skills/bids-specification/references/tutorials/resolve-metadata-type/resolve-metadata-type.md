# How To: Resolve Metadata Type

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: A unit test for utils.resolve_metadata_type.

## Prerequisites

**Required Modules:**
- `bidsschematools.render`


## Step-by-Step Guide

### Step 1: 'A unit test for utils.resolve_metadata_type.'

```python
'A unit test for utils.resolve_metadata_type.'
```

**Verification:**
```python
assert target_description == type_description
```

### Step 2: Assign base_definition = value

```python
base_definition = {'name': 'Term', 'description': 'A description'}
```

**Verification:**
```python
assert target_description == type_description
```

### Step 3: Assign term_definition1 = base_definition.copy(...)

```python
term_definition1 = base_definition.copy()
```

### Step 4: Assign unknown = 'string'

```python
term_definition1['type'] = 'string'
```

### Step 5: Assign target_description = '[string](https://www.w3schools.com/js/js_json_datatypes.asp)'

```python
target_description = '[string](https://www.w3schools.com/js/js_json_datatypes.asp)'
```

### Step 6: Assign type_description = utils.resolve_metadata_type(...)

```python
type_description = utils.resolve_metadata_type(term_definition1)
```

**Verification:**
```python
assert target_description == type_description
```

### Step 7: Assign unknown = value

```python
term_definition1['enum'] = ['n/a']
```

### Step 8: Assign target_description = '`"n/a"`'

```python
target_description = '`"n/a"`'
```

### Step 9: Assign type_description = utils.resolve_metadata_type(...)

```python
type_description = utils.resolve_metadata_type(term_definition1)
```

**Verification:**
```python
assert target_description == type_description
```


## Complete Example

```python
# Workflow
'A unit test for utils.resolve_metadata_type.'
base_definition = {'name': 'Term', 'description': 'A description'}
term_definition1 = base_definition.copy()
term_definition1['type'] = 'string'
target_description = '[string](https://www.w3schools.com/js/js_json_datatypes.asp)'
type_description = utils.resolve_metadata_type(term_definition1)
assert target_description == type_description
term_definition1['enum'] = ['n/a']
target_description = '`"n/a"`'
type_description = utils.resolve_metadata_type(term_definition1)
assert target_description == type_description
```

## Next Steps


---

*Source: test_render_utils.py:12 | Complexity: Advanced | Last updated: 2026-05-18*