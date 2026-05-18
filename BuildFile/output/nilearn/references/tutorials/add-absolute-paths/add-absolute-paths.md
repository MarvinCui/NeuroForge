# How To: Add Absolute Paths

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test _add_absolute_paths.

## Prerequisites

**Required Modules:**
- `hashlib`
- `json`
- `os`
- `re`
- `stat`
- `pathlib`
- `urllib`
- `numpy`
- `pandas`
- `pytest`
- `requests`
- `nilearn._utils.data_gen`
- `nilearn.conftest`
- `nilearn.datasets`
- `nilearn.image`


## Step-by-Step Guide

### Step 1: 'Test _add_absolute_paths.'

```python
'Test _add_absolute_paths.'
```

**Verification:**
```python
assert meta['col_absolute_path'] == Path('dir_0', 'neurovault', 'collection_1')
```

### Step 2: Assign meta = value

```python
meta = {'col_relative_path': 'collection_1', 'col_absolute_path': Path('dir_0', 'neurovault', 'collection_1')}
```

**Verification:**
```python
assert meta['col_absolute_path'] == Path('dir_1', 'neurovault', 'collection_1')
```

### Step 3: Assign meta = neurovault._add_absolute_paths(...)

```python
meta = neurovault._add_absolute_paths(Path('dir_1', 'neurovault'), meta, force=False)
```

**Verification:**
```python
assert meta == meta_transformed
```

### Step 4: Assign meta = neurovault._add_absolute_paths(...)

```python
meta = neurovault._add_absolute_paths(Path('dir_1', 'neurovault'), meta, force=True)
```

**Verification:**
```python
assert meta['col_absolute_path'] == Path('dir_1', 'neurovault', 'collection_1')
```

### Step 5: Assign meta = value

```python
meta = {'id': 0}
```

### Step 6: Assign meta_transformed = neurovault._add_absolute_paths(...)

```python
meta_transformed = neurovault._add_absolute_paths(Path('dir_1', 'neurovault'), meta, force=True)
```

**Verification:**
```python
assert meta == meta_transformed
```


## Complete Example

```python
# Workflow
'Test _add_absolute_paths.'
meta = {'col_relative_path': 'collection_1', 'col_absolute_path': Path('dir_0', 'neurovault', 'collection_1')}
meta = neurovault._add_absolute_paths(Path('dir_1', 'neurovault'), meta, force=False)
assert meta['col_absolute_path'] == Path('dir_0', 'neurovault', 'collection_1')
meta = neurovault._add_absolute_paths(Path('dir_1', 'neurovault'), meta, force=True)
assert meta['col_absolute_path'] == Path('dir_1', 'neurovault', 'collection_1')
meta = {'id': 0}
meta_transformed = neurovault._add_absolute_paths(Path('dir_1', 'neurovault'), meta, force=True)
assert meta == meta_transformed
```

## Next Steps


---

*Source: test_neurovault.py:623 | Complexity: Intermediate | Last updated: 2026-05-18*