# How To: Filter Columns

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test filter_columns.

## Prerequisites

**Required Modules:**
- `gzip`
- `os`
- `re`
- `shutil`
- `tarfile`
- `urllib`
- `pathlib`
- `unittest.mock`
- `zipfile`
- `numpy`
- `pytest`
- `requests`
- `nilearn.datasets`
- `nilearn.datasets.tests.conftest`


## Step-by-Step Guide

### Step 1: 'Test filter_columns.'

```python
'Test filter_columns.'
```

**Verification:**
```python
assert np.sum(f) == 24
```

### Step 2: Assign value1 = np.arange(...)

```python
value1 = np.arange(500)
```

**Verification:**
```python
assert np.sum(f) == 15
```

### Step 3: Assign strings = np.asarray(...)

```python
strings = np.asarray(['a', 'b', 'c'])
```

**Verification:**
```python
assert np.sum(f) == 500
```

### Step 4: Assign value2 = value

```python
value2 = strings[value1 % 3]
```

**Verification:**
```python
assert np.sum(f) == 167
```

### Step 5: Assign values = np.asarray(...)

```python
values = np.asarray(list(zip(value1, value2, strict=False)), dtype=[('INT', int), ('STR', 'S1')])
```

**Verification:**
```python
assert np.sum(f) == 167
```

### Step 6: Assign f = _utils.filter_columns(...)

```python
f = _utils.filter_columns(values, {'INT': (23, 46)})
```

**Verification:**
```python
assert np.sum(f) == 84
```

### Step 7: Assign f = _utils.filter_columns(...)

```python
f = _utils.filter_columns(values, {'INT': [0, 9, (12, 24)]})
```

**Verification:**
```python
assert np.sum(f) == 333
```

### Step 8: Assign value1 = value

```python
value1 = value1 % 2
```

### Step 9: Assign values = np.asarray(...)

```python
values = np.asarray(list(zip(value1, value2, strict=False)), dtype=[('INT', int), ('STR', b'S1')])
```

### Step 10: Assign f = _utils.filter_columns(...)

```python
f = _utils.filter_columns(values, [])
```

**Verification:**
```python
assert np.sum(f) == 500
```

### Step 11: Assign f = _utils.filter_columns(...)

```python
f = _utils.filter_columns(values, {'STR': b'b'})
```

**Verification:**
```python
assert np.sum(f) == 167
```

### Step 12: Assign f = _utils.filter_columns(...)

```python
f = _utils.filter_columns(values, {'STR': 'b'})
```

**Verification:**
```python
assert np.sum(f) == 167
```

### Step 13: Assign f = _utils.filter_columns(...)

```python
f = _utils.filter_columns(values, {'INT': 1, 'STR': b'b'})
```

**Verification:**
```python
assert np.sum(f) == 84
```

### Step 14: Assign f = _utils.filter_columns(...)

```python
f = _utils.filter_columns(values, {'INT': 1, 'STR': b'b'}, combination='or')
```

**Verification:**
```python
assert np.sum(f) == 333
```


## Complete Example

```python
# Workflow
'Test filter_columns.'
value1 = np.arange(500)
strings = np.asarray(['a', 'b', 'c'])
value2 = strings[value1 % 3]
values = np.asarray(list(zip(value1, value2, strict=False)), dtype=[('INT', int), ('STR', 'S1')])
f = _utils.filter_columns(values, {'INT': (23, 46)})
assert np.sum(f) == 24
f = _utils.filter_columns(values, {'INT': [0, 9, (12, 24)]})
assert np.sum(f) == 15
value1 = value1 % 2
values = np.asarray(list(zip(value1, value2, strict=False)), dtype=[('INT', int), ('STR', b'S1')])
f = _utils.filter_columns(values, [])
assert np.sum(f) == 500
f = _utils.filter_columns(values, {'STR': b'b'})
assert np.sum(f) == 167
f = _utils.filter_columns(values, {'STR': 'b'})
assert np.sum(f) == 167
f = _utils.filter_columns(values, {'INT': 1, 'STR': b'b'})
assert np.sum(f) == 84
f = _utils.filter_columns(values, {'INT': 1, 'STR': b'b'}, combination='or')
assert np.sum(f) == 333
```

## Next Steps


---

*Source: test_utils.py:332 | Complexity: Advanced | Last updated: 2026-05-18*