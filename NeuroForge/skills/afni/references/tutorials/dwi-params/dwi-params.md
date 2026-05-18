# How To: Dwi Params

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dwi params

## Prerequisites

**Required Modules:**
- `os.path`
- `gzip`
- `numpy`
- `nose.tools`
- `numpy.testing`
- `dicom`


## Step-by-Step Guide

### Step 1: Assign dw = didw.wrapper_from_data(...)

```python
dw = didw.wrapper_from_data(DATA)
```

**Verification:**
```python
assert_equal(b_matrix.shape, (3, 3))
```

### Step 2: Assign b_matrix = value

```python
b_matrix = dw.b_matrix
```

**Verification:**
```python
assert_array_almost_equal(b, EXPECTED_PARAMS[0])
```

### Step 3: Call assert_equal()

```python
assert_equal(b_matrix.shape, (3, 3))
```

**Verification:**
```python
assert_array_almost_equal(g, EXPECTED_PARAMS[1])
```

### Step 4: Assign q = value

```python
q = dw.q_vector
```

### Step 5: Assign b = np.sqrt(...)

```python
b = np.sqrt(np.sum(q * q))
```

### Step 6: Assign g = value

```python
g = q / b
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(b, EXPECTED_PARAMS[0])
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(g, EXPECTED_PARAMS[1])
```


## Complete Example

```python
# Workflow
dw = didw.wrapper_from_data(DATA)
b_matrix = dw.b_matrix
assert_equal(b_matrix.shape, (3, 3))
q = dw.q_vector
b = np.sqrt(np.sum(q * q))
g = q / b
assert_array_almost_equal(b, EXPECTED_PARAMS[0])
assert_array_almost_equal(g, EXPECTED_PARAMS[1])
```

## Next Steps


---

*Source: test_dicomwrappers.py:96 | Complexity: Advanced | Last updated: 2026-05-18*