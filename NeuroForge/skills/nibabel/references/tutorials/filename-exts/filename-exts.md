# How To: Filename Exts

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test filename exts

## Prerequisites

**Required Modules:**
- `io`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `fileholders`
- `openers`
- `spatialimages`
- `testing`
- `tests`
- `tests`
- `tmpdirs`
- `volumeutils`
- `wrapstruct`
- `mghformat`


## Step-by-Step Guide

### Step 1: Assign v = np.ones(...)

```python
v = np.ones((7, 13, 3, 22), np.uint8)
```

**Verification:**
```python
assert_array_equal(img_back.get_fdata(), v)
```

### Step 2: Assign img = MGHImage(...)

```python
img = MGHImage(v, None)
```

### Step 3: Assign fname = value

```python
fname = 'tmpname' + ext
```

### Step 4: Call save()

```python
save(img, fname)
```

### Step 5: Assign img_back = load(...)

```python
img_back = load(fname)
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(img_back.get_fdata(), v)
```


## Complete Example

```python
# Workflow
v = np.ones((7, 13, 3, 22), np.uint8)
img = MGHImage(v, None)
for ext in ('.mgh', '.mgz'):
    with InTemporaryDirectory():
        fname = 'tmpname' + ext
        save(img, fname)
        img_back = load(fname)
        assert_array_equal(img_back.get_fdata(), v)
        del img_back
```

## Next Steps


---

*Source: test_mghformat.py:194 | Complexity: Intermediate | Last updated: 2026-05-18*