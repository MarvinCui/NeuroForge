# How To: Sample Domain Regular

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test sample domain regular

## Prerequisites

**Required Modules:**
- `functools`
- `operator`
- `numpy`
- `numpy.testing`
- `scipy`
- `dipy.align`
- `dipy.align.parzenhist`
- `dipy.align.transforms`
- `dipy.core.interpolation`
- `dipy.core.ndindex`
- `dipy.data`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign shape = np.array(...)

```python
shape = np.array((10, 10), dtype=np.int32)
```

**Verification:**
```python
assert_raises(ValueError, sample_domain_regular, k, shape, invalid_affine, sigma=sigma)
```

### Step 2: Assign affine = np.eye(...)

```python
affine = np.eye(3)
```

**Verification:**
```python
assert_array_equal(samples.shape, [n // k, dim])
```

### Step 3: Assign invalid_affine = np.eye(...)

```python
invalid_affine = np.eye(2)
```

**Verification:**
```python
assert_equal(len(set(indices)), len(indices))
```

### Step 4: Assign sigma = 0

```python
sigma = 0
```

**Verification:**
```python
assert_equal((indices % k).sum(), 0)
```

### Step 5: Assign dim = len(...)

```python
dim = len(shape)
```

**Verification:**
```python
assert_raises(ValueError, sample_domain_regular, k, shape, invalid_affine, sigma=sigma)
```

### Step 6: Assign n = value

```python
n = shape[0] * shape[1]
```

**Verification:**
```python
assert_array_equal(samples.shape, [n // k, dim])
```

### Step 7: Assign k = 2

```python
k = 2
```

**Verification:**
```python
assert_equal(len(set(indices)), len(indices))
```

### Step 8: Call assert_raises()

```python
assert_raises(ValueError, sample_domain_regular, k, shape, invalid_affine, sigma=sigma)
```

**Verification:**
```python
assert_equal((indices % k).sum(), 0)
```

### Step 9: Assign samples = sample_domain_regular(...)

```python
samples = sample_domain_regular(k, shape, affine, sigma=sigma)
```

### Step 10: Assign isamples = np.array(...)

```python
isamples = np.array(samples, dtype=np.int32)
```

### Step 11: Assign indices = value

```python
indices = isamples[:, 0] * shape[1] + isamples[:, 1]
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(samples.shape, [n // k, dim])
```

### Step 13: Call assert_equal()

```python
assert_equal(len(set(indices)), len(indices))
```

### Step 14: Call assert_equal()

```python
assert_equal((indices % k).sum(), 0)
```

### Step 15: Assign shape = np.array(...)

```python
shape = np.array((5, 10, 10), dtype=np.int32)
```

### Step 16: Assign affine = np.eye(...)

```python
affine = np.eye(4)
```

### Step 17: Assign invalid_affine = np.eye(...)

```python
invalid_affine = np.eye(3)
```

### Step 18: Assign sigma = 0

```python
sigma = 0
```

### Step 19: Assign dim = len(...)

```python
dim = len(shape)
```

### Step 20: Assign n = value

```python
n = shape[0] * shape[1] * shape[2]
```

### Step 21: Assign k = 10

```python
k = 10
```

### Step 22: Call assert_raises()

```python
assert_raises(ValueError, sample_domain_regular, k, shape, invalid_affine, sigma=sigma)
```

### Step 23: Assign samples = sample_domain_regular(...)

```python
samples = sample_domain_regular(k, shape, affine, sigma=sigma)
```

### Step 24: Assign isamples = np.array(...)

```python
isamples = np.array(samples, dtype=np.int32)
```

### Step 25: Assign indices = value

```python
indices = isamples[:, 0] * shape[1] * shape[2] + isamples[:, 1] * shape[2] + isamples[:, 2]
```

### Step 26: Call assert_array_equal()

```python
assert_array_equal(samples.shape, [n // k, dim])
```

### Step 27: Call assert_equal()

```python
assert_equal(len(set(indices)), len(indices))
```

### Step 28: Call assert_equal()

```python
assert_equal((indices % k).sum(), 0)
```


## Complete Example

```python
# Workflow
shape = np.array((10, 10), dtype=np.int32)
affine = np.eye(3)
invalid_affine = np.eye(2)
sigma = 0
dim = len(shape)
n = shape[0] * shape[1]
k = 2
assert_raises(ValueError, sample_domain_regular, k, shape, invalid_affine, sigma=sigma)
samples = sample_domain_regular(k, shape, affine, sigma=sigma)
isamples = np.array(samples, dtype=np.int32)
indices = isamples[:, 0] * shape[1] + isamples[:, 1]
assert_array_equal(samples.shape, [n // k, dim])
assert_equal(len(set(indices)), len(indices))
assert_equal((indices % k).sum(), 0)
shape = np.array((5, 10, 10), dtype=np.int32)
affine = np.eye(4)
invalid_affine = np.eye(3)
sigma = 0
dim = len(shape)
n = shape[0] * shape[1] * shape[2]
k = 10
assert_raises(ValueError, sample_domain_regular, k, shape, invalid_affine, sigma=sigma)
samples = sample_domain_regular(k, shape, affine, sigma=sigma)
isamples = np.array(samples, dtype=np.int32)
indices = isamples[:, 0] * shape[1] * shape[2] + isamples[:, 1] * shape[2] + isamples[:, 2]
assert_array_equal(samples.shape, [n // k, dim])
assert_equal(len(set(indices)), len(indices))
assert_equal((indices % k).sum(), 0)
```

## Next Steps


---

*Source: test_parzenhist.py:550 | Complexity: Advanced | Last updated: 2026-05-18*