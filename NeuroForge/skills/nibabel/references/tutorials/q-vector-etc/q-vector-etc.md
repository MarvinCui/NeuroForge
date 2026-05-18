# How To: Q Vector Etc

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test q vector etc

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

### Step 1: Assign dw = didw.Wrapper(...)

```python
dw = didw.Wrapper(DATA)
```

**Verification:**
```python
assert dw.q_vector is None
```

### Step 2: Assign dw = didw.Wrapper(...)

```python
dw = didw.Wrapper(DATA)
```

**Verification:**
```python
assert dw.b_value is None
```

### Step 3: Assign dw.q_vector = np.array(...)

```python
dw.q_vector = np.array([0, 0, 1e-06])
```

**Verification:**
```python
assert dw.b_vector is None
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(dw.b_vector, np.zeros((3,)))
```

**Verification:**
```python
assert_array_equal(dw.q_vector, q_vec)
```

### Step 5: Assign sdw = didw.MosaicWrapper(...)

```python
sdw = didw.MosaicWrapper(DATA)
```

**Verification:**
```python
assert dw.b_value == 10
```

### Step 6: Assign unknown = EXPECTED_PARAMS

```python
exp_b, exp_g = EXPECTED_PARAMS
```

**Verification:**
```python
assert_array_equal(dw.b_vector, q_vec / 10.0)
```

### Step 7: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sdw.q_vector, exp_b * np.array(exp_g), 5)
```

**Verification:**
```python
assert dw.b_value == 0
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sdw.b_value, exp_b)
```

**Verification:**
```python
assert_array_equal(dw.b_vector, np.zeros((3,)))
```

### Step 9: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sdw.b_vector, exp_g)
```

**Verification:**
```python
assert_array_almost_equal(sdw.q_vector, exp_b * np.array(exp_g), 5)
```

### Step 10: Assign sdw = didw.MosaicWrapper(...)

```python
sdw = didw.MosaicWrapper(DATA)
```

**Verification:**
```python
assert_array_almost_equal(sdw.b_value, exp_b)
```

### Step 11: Assign sdw.q_vector = np.array(...)

```python
sdw.q_vector = np.array([0, 0, 1e-06])
```

**Verification:**
```python
assert_array_almost_equal(sdw.b_vector, exp_g)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(sdw.b_vector, np.zeros((3,)))
```

**Verification:**
```python
assert sdw.b_value == 0
```

### Step 13: Assign q_vec = np.zeros(...)

```python
q_vec = np.zeros((3,))
```

**Verification:**
```python
assert_array_equal(sdw.b_vector, np.zeros((3,)))
```

### Step 14: Assign unknown = 10.0

```python
q_vec[pos] = 10.0
```

### Step 15: Assign dw = didw.Wrapper(...)

```python
dw = didw.Wrapper(DATA)
```

### Step 16: Assign dw.q_vector = q_vec

```python
dw.q_vector = q_vec
```

### Step 17: Call assert_array_equal()

```python
assert_array_equal(dw.q_vector, q_vec)
```

**Verification:**
```python
assert dw.b_value == 10
```

### Step 18: Call assert_array_equal()

```python
assert_array_equal(dw.b_vector, q_vec / 10.0)
```


## Complete Example

```python
# Workflow
dw = didw.Wrapper(DATA)
assert dw.q_vector is None
assert dw.b_value is None
assert dw.b_vector is None
for pos in range(3):
    q_vec = np.zeros((3,))
    q_vec[pos] = 10.0
    dw = didw.Wrapper(DATA)
    dw.q_vector = q_vec
    assert_array_equal(dw.q_vector, q_vec)
    assert dw.b_value == 10
    assert_array_equal(dw.b_vector, q_vec / 10.0)
dw = didw.Wrapper(DATA)
dw.q_vector = np.array([0, 0, 1e-06])
assert dw.b_value == 0
assert_array_equal(dw.b_vector, np.zeros((3,)))
sdw = didw.MosaicWrapper(DATA)
exp_b, exp_g = EXPECTED_PARAMS
assert_array_almost_equal(sdw.q_vector, exp_b * np.array(exp_g), 5)
assert_array_almost_equal(sdw.b_value, exp_b)
assert_array_almost_equal(sdw.b_vector, exp_g)
sdw = didw.MosaicWrapper(DATA)
sdw.q_vector = np.array([0, 0, 1e-06])
assert sdw.b_value == 0
assert_array_equal(sdw.b_vector, np.zeros((3,)))
```

## Next Steps


---

*Source: test_dicomwrappers.py:214 | Complexity: Advanced | Last updated: 2026-05-18*