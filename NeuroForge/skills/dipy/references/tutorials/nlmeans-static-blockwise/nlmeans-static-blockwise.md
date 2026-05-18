# How To: Nlmeans Static Blockwise

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test static image denoising with blockwise method.

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

### Step 1: 'Test static image denoising with blockwise method.'

```python
'Test static image denoising with blockwise method.'
```

**Verification:**
```python
assert_equal(S0.shape, S0nb.shape)
```

### Step 2: Assign S0 = value

```python
S0 = 100 * np.ones((20, 20, 20), dtype='f8')
```

**Verification:**
```python
assert np.abs(np.mean(S0nb) - 100) < 20
```

### Step 3: Assign S0nb = nlmeans(...)

```python
S0nb = nlmeans(S0, sigma=1.0, rician=False, method='blockwise')
```

**Verification:**
```python
assert np.all(S0nb >= 0)
```

### Step 4: Call assert_equal()

```python
assert_equal(S0.shape, S0nb.shape)
```

**Verification:**
```python
assert_equal(S0.shape, S0nb.shape)
```

### Step 5: Assign S0 = value

```python
S0 = 100 * np.ones((20, 20, 20, 3), dtype='f8')
```

**Verification:**
```python
assert np.abs(np.mean(S0nb) - 100) < 20
```

### Step 6: Assign S0nb = nlmeans(...)

```python
S0nb = nlmeans(S0, sigma=1.0, rician=False, method='blockwise')
```

**Verification:**
```python
assert_equal(S0.shape, S0nb.shape)
```

### Step 7: Call assert_equal()

```python
assert_equal(S0.shape, S0nb.shape)
```

**Verification:**
```python
assert np.abs(np.mean(S0nb) - 100) < 20
```

### Step 8: Assign S0nb = nlmeans(...)

```python
S0nb = nlmeans(S0, sigma=np.array(1.0), rician=False, method='blockwise')
```

**Verification:**
```python
assert_equal(S0.shape, S0nb.shape)
```

### Step 9: Call assert_equal()

```python
assert_equal(S0.shape, S0nb.shape)
```

**Verification:**
```python
assert np.abs(np.mean(S0nb) - 100) < 20
```

### Step 10: Assign S0nb = nlmeans(...)

```python
S0nb = nlmeans(S0, sigma=np.array([1.0]), rician=False, method='blockwise')
```

### Step 11: Call assert_equal()

```python
assert_equal(S0.shape, S0nb.shape)
```

**Verification:**
```python
assert np.abs(np.mean(S0nb) - 100) < 20
```


## Complete Example

```python
# Workflow
'Test static image denoising with blockwise method.'
S0 = 100 * np.ones((20, 20, 20), dtype='f8')
S0nb = nlmeans(S0, sigma=1.0, rician=False, method='blockwise')
assert_equal(S0.shape, S0nb.shape)
assert np.abs(np.mean(S0nb) - 100) < 20
assert np.all(S0nb >= 0)
S0 = 100 * np.ones((20, 20, 20, 3), dtype='f8')
S0nb = nlmeans(S0, sigma=1.0, rician=False, method='blockwise')
assert_equal(S0.shape, S0nb.shape)
assert np.abs(np.mean(S0nb) - 100) < 20
S0nb = nlmeans(S0, sigma=np.array(1.0), rician=False, method='blockwise')
assert_equal(S0.shape, S0nb.shape)
assert np.abs(np.mean(S0nb) - 100) < 20
S0nb = nlmeans(S0, sigma=np.array([1.0]), rician=False, method='blockwise')
assert_equal(S0.shape, S0nb.shape)
assert np.abs(np.mean(S0nb) - 100) < 20
```

## Next Steps


---

*Source: test_nlmeans.py:153 | Complexity: Advanced | Last updated: 2026-05-18*