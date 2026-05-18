# How To: Cache Shelving

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test cache shelving

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `shutil`
- `pathlib`
- `pytest`
- `joblib`
- `nilearn`
- `nilearn._utils.cache_mixin`
- `nilearn._utils.helpers`
- `nilearn.datasets.tests.conftest`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: Assign joblib_dir = value

```python
joblib_dir = tmp_path / 'joblib' / 'nilearn' / '_utils' / 'tests' / 'test_cache_mixin' / 'f'
```

**Verification:**
```python
assert res.get() == 2
```

### Step 2: Assign mem = Memory(...)

```python
mem = Memory(location=str(tmp_path), verbose=0)
```

**Verification:**
```python
assert len(_get_subdirs(joblib_dir)) == 1
```

### Step 3: Assign res = cache(...)

```python
res = cache(f, mem, shelve=True)(2)
```

**Verification:**
```python
assert res.get() == 2
```

### Step 4: Assign res = cache(...)

```python
res = cache(f, mem, shelve=True)(2)
```

**Verification:**
```python
assert len(_get_subdirs(joblib_dir)) == 1
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
joblib_dir = tmp_path / 'joblib' / 'nilearn' / '_utils' / 'tests' / 'test_cache_mixin' / 'f'
mem = Memory(location=str(tmp_path), verbose=0)
res = cache(f, mem, shelve=True)(2)
assert res.get() == 2
assert len(_get_subdirs(joblib_dir)) == 1
res = cache(f, mem, shelve=True)(2)
assert res.get() == 2
assert len(_get_subdirs(joblib_dir)) == 1
```

## Next Steps


---

*Source: test_cache_mixin.py:139 | Complexity: Intermediate | Last updated: 2026-05-18*