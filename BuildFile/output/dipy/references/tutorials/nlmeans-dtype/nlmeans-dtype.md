# How To: Nlmeans Dtype

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test dtype preservation with classic method.

## Prerequisites

**Required Modules:**
- `time`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.denoise.denspeed`
- `dipy.denoise.nlmeans`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.omp`


## Step-by-Step Guide

### Step 1: 'Test dtype preservation with classic method.'

```python
'Test dtype preservation with classic method.'
```

**Verification:**
```python
assert_equal(S0.dtype, S0n.dtype)
```

### Step 2: Assign S0 = value

```python
S0 = 200 * np.ones((20, 20, 20, 3), dtype='f4')
```

**Verification:**
```python
assert_equal(S0.dtype, S0n.dtype)
```

### Step 3: Assign mask = np.zeros(...)

```python
mask = np.zeros((20, 20, 20))
```

**Verification:**
```python
assert_equal(S0.dtype, S0n.dtype)
```

### Step 4: Assign unknown = 1

```python
mask[10:14, 10:14, 10:14] = 1
```

### Step 5: Assign S0n = nlmeans(...)

```python
S0n = nlmeans(S0, sigma=1, mask=mask, rician=True, method='classic')
```

### Step 6: Call assert_equal()

```python
assert_equal(S0.dtype, S0n.dtype)
```

### Step 7: Assign S0 = value

```python
S0 = 200 * np.ones((20, 20, 20), dtype=np.uint16)
```

### Step 8: Assign mask = np.zeros(...)

```python
mask = np.zeros((20, 20, 20))
```

### Step 9: Assign unknown = 1

```python
mask[10:14, 10:14, 10:14] = 1
```

### Step 10: Assign S0n = nlmeans(...)

```python
S0n = nlmeans(S0, sigma=1, mask=mask, rician=True, method='classic')
```

### Step 11: Call assert_equal()

```python
assert_equal(S0.dtype, S0n.dtype)
```

### Step 12: Assign S0n = nlmeans(...)

```python
S0n = nlmeans(S0, sigma=np.ones((20, 20, 20)), mask=mask, rician=True, method='classic')
```

### Step 13: Call assert_equal()

```python
assert_equal(S0.dtype, S0n.dtype)
```


## Complete Example

```python
# Workflow
'Test dtype preservation with classic method.'
S0 = 200 * np.ones((20, 20, 20, 3), dtype='f4')
mask = np.zeros((20, 20, 20))
mask[10:14, 10:14, 10:14] = 1
S0n = nlmeans(S0, sigma=1, mask=mask, rician=True, method='classic')
assert_equal(S0.dtype, S0n.dtype)
S0 = 200 * np.ones((20, 20, 20), dtype=np.uint16)
mask = np.zeros((20, 20, 20))
mask[10:14, 10:14, 10:14] = 1
S0n = nlmeans(S0, sigma=1, mask=mask, rician=True, method='classic')
assert_equal(S0.dtype, S0n.dtype)
S0n = nlmeans(S0, sigma=np.ones((20, 20, 20)), mask=mask, rician=True, method='classic')
assert_equal(S0.dtype, S0n.dtype)
```

## Next Steps


---

*Source: test_nlmeans.py:107 | Complexity: Advanced | Last updated: 2026-05-18*