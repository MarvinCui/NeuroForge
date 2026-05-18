# How To: Calculate Tfce

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test calculate_tfce.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `math`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy.ndimage`
- `nilearn.conftest`
- `nilearn.mass_univariate`
- `nilearn.mass_univariate.tests._testing`

**Setup Required:**
```python
# Fixtures: two_sided_test, dh, true_max_tfce
```

## Step-by-Step Guide

### Step 1: 'Test calculate_tfce.'

```python
'Test calculate_tfce.'
```

**Verification:**
```python
assert test_tfce_arr4d.shape == arr4d.shape
```

### Step 2: Assign arr4d = np.zeros(...)

```python
arr4d = np.zeros((10, 10, 10, 1))
```

**Verification:**
```python
assert np.max(np.abs(test_tfce_arr4d)) == true_max_tfce
```

### Step 3: Assign bin_struct = generate_binary_structure(...)

```python
bin_struct = generate_binary_structure(3, 1)
```

### Step 4: Assign unknown = 10

```python
arr4d[:2, :2, :2, 0] = 10
```

### Step 5: Assign unknown = 10

```python
arr4d[0, 2, 0, 0] = 10
```

### Step 6: Assign unknown = 10

```python
arr4d[2, 0, 0, 0] = 10
```

### Step 7: Assign unknown = value

```python
arr4d[3:5, 3:5, 3:5, 0] = -11
```

### Step 8: Assign unknown = value

```python
arr4d[3, 5, 3, 0] = -11
```

### Step 9: Assign unknown = value

```python
arr4d[5, 3, 3, 0] = -11
```

### Step 10: Assign test_tfce_arr4d = _utils.calculate_tfce(...)

```python
test_tfce_arr4d = _utils.calculate_tfce(arr4d, bin_struct=bin_struct, E=1, H=1, dh=dh, two_sided_test=two_sided_test)
```

**Verification:**
```python
assert test_tfce_arr4d.shape == arr4d.shape
```


## Complete Example

```python
# Setup
# Fixtures: two_sided_test, dh, true_max_tfce

# Workflow
'Test calculate_tfce.'
arr4d = np.zeros((10, 10, 10, 1))
bin_struct = generate_binary_structure(3, 1)
arr4d[:2, :2, :2, 0] = 10
arr4d[0, 2, 0, 0] = 10
arr4d[2, 0, 0, 0] = 10
arr4d[3:5, 3:5, 3:5, 0] = -11
arr4d[3, 5, 3, 0] = -11
arr4d[5, 3, 3, 0] = -11
test_tfce_arr4d = _utils.calculate_tfce(arr4d, bin_struct=bin_struct, E=1, H=1, dh=dh, two_sided_test=two_sided_test)
assert test_tfce_arr4d.shape == arr4d.shape
assert np.max(np.abs(test_tfce_arr4d)) == true_max_tfce
```

## Next Steps


---

*Source: test_utils.py:39 | Complexity: Advanced | Last updated: 2026-05-18*