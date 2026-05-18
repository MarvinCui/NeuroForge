# How To: Load Mni152

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test load mni152

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pathlib`
- `pandas`
- `pytest`
- `nibabel`
- `sklearn.utils`
- `nilearn._utils.helpers`
- `nilearn.datasets.struct`
- `nilearn.datasets.tests._testing`
- `nilearn.surface`

**Setup Required:**
```python
# Fixtures: func, resolution
```

## Step-by-Step Guide

### Step 1: Assign img = func(...)

```python
img = func(resolution=resolution)
```

**Verification:**
```python
assert isinstance(img, Nifti1Image)
```

### Step 2: Call check_type_fetcher()

```python
check_type_fetcher(img)
```

**Verification:**
```python
assert img.shape == expected_shape
```

### Step 3: Assign expected_shape = value

```python
expected_shape = (197, 233, 189)
```

**Verification:**
```python
assert img.header.get_zooms() == expected_zooms
```

### Step 4: Assign expected_zooms = value

```python
expected_zooms = (1.0, 1.0, 1.0)
```

### Step 5: Assign expected_shape = value

```python
expected_shape = (99, 117, 95)
```

### Step 6: Assign expected_zooms = value

```python
expected_zooms = (2.0, 2.0, 2.0)
```


## Complete Example

```python
# Setup
# Fixtures: func, resolution

# Workflow
img = func(resolution=resolution)
assert isinstance(img, Nifti1Image)
check_type_fetcher(img)
if resolution is None:
    expected_shape = (197, 233, 189)
    expected_zooms = (1.0, 1.0, 1.0)
elif resolution == 2:
    expected_shape = (99, 117, 95)
    expected_zooms = (2.0, 2.0, 2.0)
assert img.shape == expected_shape
assert img.header.get_zooms() == expected_zooms
```

## Next Steps


---

*Source: test_struct.py:126 | Complexity: Intermediate | Last updated: 2026-05-18*