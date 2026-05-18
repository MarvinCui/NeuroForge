# How To: Dwi Params

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test dwi params

## Prerequisites

**Required Modules:**
- `gzip`
- `copy`
- `decimal`
- `hashlib`
- `os.path`
- `os.path`
- `unittest`
- `numpy`
- `pytest`
- `numpy.testing`
- `openers`
- `tests.nibabel_data`
- `volumeutils`


## Step-by-Step Guide

### Step 1: Assign dw = didw.wrapper_from_data(...)

```python
dw = didw.wrapper_from_data(DATA)
```

**Verification:**
```python
assert b_matrix.shape == (3, 3)
```

### Step 2: Assign b_matrix = value

```python
b_matrix = dw.b_matrix
```

**Verification:**
```python
assert_array_almost_equal(b, EXPECTED_PARAMS[0])
```

### Step 3: Assign q = value

```python
q = dw.q_vector
```

**Verification:**
```python
assert_array_almost_equal(g, EXPECTED_PARAMS[1])
```

### Step 4: Assign b = np.sqrt(...)

```python
b = np.sqrt(np.sum(q * q))
```

### Step 5: Assign g = value

```python
g = q / b
```

### Step 6: Call assert_array_almost_equal()

```python
assert_array_almost_equal(b, EXPECTED_PARAMS[0])
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(g, EXPECTED_PARAMS[1])
```


## Complete Example

```python
# Workflow
dw = didw.wrapper_from_data(DATA)
b_matrix = dw.b_matrix
assert b_matrix.shape == (3, 3)
q = dw.q_vector
b = np.sqrt(np.sum(q * q))
g = q / b
assert_array_almost_equal(b, EXPECTED_PARAMS[0])
assert_array_almost_equal(g, EXPECTED_PARAMS[1])
```

## Next Steps


---

*Source: test_dicomwrappers.py:202 | Complexity: Intermediate | Last updated: 2026-05-18*