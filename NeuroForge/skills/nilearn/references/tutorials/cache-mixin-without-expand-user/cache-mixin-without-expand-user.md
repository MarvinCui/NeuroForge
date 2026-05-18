# How To: Cache Mixin Without Expand User

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: test cache mixin without expand user

## Prerequisites

**Required Modules:**
- `shutil`
- `pathlib`
- `pytest`
- `joblib`
- `nilearn`
- `nilearn._utils.cache_mixin`
- `nilearn._utils.helpers`
- `nilearn.datasets.tests.conftest`


## Step-by-Step Guide

### Step 1: Assign cache_dir = '~/nilearn_data/test_cache'

```python
cache_dir = '~/nilearn_data/test_cache'
```

**Verification:**
```python
assert not expand_cache_dir.exists()
```

### Step 2: Assign expand_cache_dir = Path.expanduser(...)

```python
expand_cache_dir = Path(cache_dir).expanduser()
```

**Verification:**
```python
assert not expand_cache_dir.exists()
```

### Step 3: Assign mixin_mock = CacheMixinTest(...)

```python
mixin_mock = CacheMixinTest(cache_dir)
```

**Verification:**
```python
assert not expand_cache_dir.exists()
```

### Step 4: Assign nilearn.EXPAND_PATH_WILDCARDS = False

```python
nilearn.EXPAND_PATH_WILDCARDS = False
```

**Verification:**
```python
assert not expand_cache_dir.exists()
```

### Step 5: Assign nilearn.EXPAND_PATH_WILDCARDS = True

```python
nilearn.EXPAND_PATH_WILDCARDS = True
```

### Step 6: Call mixin_mock.run()

```python
mixin_mock.run()
```

### Step 7: Call shutil.rmtree()

```python
shutil.rmtree(expand_cache_dir)
```


## Complete Example

```python
# Workflow
cache_dir = '~/nilearn_data/test_cache'
expand_cache_dir = Path(cache_dir).expanduser()
mixin_mock = CacheMixinTest(cache_dir)
try:
    assert not expand_cache_dir.exists()
    nilearn.EXPAND_PATH_WILDCARDS = False
    with pytest.raises(ValueError, match="Given cache path parent directory doesn't"):
        mixin_mock.run()
    assert not expand_cache_dir.exists()
    nilearn.EXPAND_PATH_WILDCARDS = True
finally:
    if expand_cache_dir.exists():
        shutil.rmtree(expand_cache_dir)
```

## Next Steps


---

*Source: test_cache_mixin.py:74 | Complexity: Advanced | Last updated: 2026-05-18*