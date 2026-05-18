# How To: Lpca Dtype

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test lpca dtype

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `scipy.special`
- `dipy.core.gradients`
- `dipy.denoise.localpca`
- `dipy.sims.voxel`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign S0 = value

```python
S0 = 200 * np.ones((20, 20, 20, 3), dtype=np.float64)
```

**Verification:**
```python
assert_equal(S0.dtype, S0ns.dtype)
```

### Step 2: Assign S0ns = localpca(...)

```python
S0ns = localpca(S0, sigma=1)
```

**Verification:**
```python
assert_equal(S0.dtype, S0ns.dtype)
```

### Step 3: Call assert_equal()

```python
assert_equal(S0.dtype, S0ns.dtype)
```

**Verification:**
```python
assert_equal(np.float32, S0ns.dtype)
```

### Step 4: Assign S0 = value

```python
S0 = 200 * np.ones((20, 20, 20, 20), dtype=np.uint16)
```

**Verification:**
```python
assert_(np.all(S0ns >= 0))
```

### Step 5: Assign S0ns = localpca(...)

```python
S0ns = localpca(S0, sigma=np.ones((20, 20, 20)))
```

**Verification:**
```python
assert_(np.all(S0ns <= 200))
```

### Step 6: Call assert_equal()

```python
assert_equal(S0.dtype, S0ns.dtype)
```

### Step 7: Assign S0 = value

```python
S0 = 200 * np.ones((20, 20, 20, 20), dtype=np.uint16)
```

### Step 8: Assign S0ns = localpca(...)

```python
S0ns = localpca(S0, sigma=np.ones((20, 20, 20)), out_dtype=np.float32)
```

### Step 9: Call assert_equal()

```python
assert_equal(np.float32, S0ns.dtype)
```

### Step 10: Assign unknown = 0

```python
S0[5:8, 5:8, 5:8] = 0
```

### Step 11: Assign S0ns = localpca(...)

```python
S0ns = localpca(S0, sigma=np.ones((20, 20, 20)), out_dtype=np.uint16)
```

### Step 12: Call assert_()

```python
assert_(np.all(S0ns >= 0))
```

### Step 13: Call assert_()

```python
assert_(np.all(S0ns <= 200))
```


## Complete Example

```python
# Workflow
S0 = 200 * np.ones((20, 20, 20, 3), dtype=np.float64)
S0ns = localpca(S0, sigma=1)
assert_equal(S0.dtype, S0ns.dtype)
S0 = 200 * np.ones((20, 20, 20, 20), dtype=np.uint16)
S0ns = localpca(S0, sigma=np.ones((20, 20, 20)))
assert_equal(S0.dtype, S0ns.dtype)
S0 = 200 * np.ones((20, 20, 20, 20), dtype=np.uint16)
S0ns = localpca(S0, sigma=np.ones((20, 20, 20)), out_dtype=np.float32)
assert_equal(np.float32, S0ns.dtype)
S0[5:8, 5:8, 5:8] = 0
S0ns = localpca(S0, sigma=np.ones((20, 20, 20)), out_dtype=np.uint16)
assert_(np.all(S0ns >= 0))
assert_(np.all(S0ns <= 200))
```

## Next Steps


---

*Source: test_lpca.py:226 | Complexity: Advanced | Last updated: 2026-05-18*