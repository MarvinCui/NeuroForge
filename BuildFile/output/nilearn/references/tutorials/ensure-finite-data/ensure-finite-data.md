# How To: Ensure Finite Data

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test ensure finite data

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `warnings`
- `pathlib`
- `tempfile`
- `joblib`
- `numpy`
- `pytest`
- `nibabel`
- `nilearn._utils.niimg`
- `nilearn._utils.testing`
- `nilearn.image`

**Setup Required:**
```python
# Fixtures: img_binary
```

## Step-by-Step Guide

### Step 1: Assign data = _get_data(...)

```python
data = _get_data(img_binary)
```

**Verification:**
```python
assert np.array_equal(data_returned, expected_data)
```

### Step 2: Assign data_returned = ensure_finite_data(...)

```python
data_returned = ensure_finite_data(data)
```

### Step 3: Assign expected_data = np.ones(...)

```python
expected_data = np.ones((3, 3, 3, 3))
```

### Step 4: Assign unknown = 0

```python
expected_data[0, 0, 0, 0] = 0
```

### Step 5: Assign unknown = 0

```python
expected_data[1, 1, 1, 1] = 0
```

**Verification:**
```python
assert np.array_equal(data_returned, expected_data)
```


## Complete Example

```python
# Setup
# Fixtures: img_binary

# Workflow
data = _get_data(img_binary)
data_returned = ensure_finite_data(data)
expected_data = np.ones((3, 3, 3, 3))
expected_data[0, 0, 0, 0] = 0
expected_data[1, 1, 1, 1] = 0
assert np.array_equal(data_returned, expected_data)
```

## Next Steps


---

*Source: test_niimg.py:317 | Complexity: Intermediate | Last updated: 2026-05-18*