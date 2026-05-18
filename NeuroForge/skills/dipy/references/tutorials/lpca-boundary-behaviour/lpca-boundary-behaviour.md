# How To: Lpca Boundary Behaviour

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test lpca boundary behaviour

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign S0 = value

```python
S0 = 100 * np.ones((20, 20, 20, 20), dtype='f8')
```

**Verification:**
```python
assert_(rmses > 0.0001)
```

### Step 2: Assign unknown = value

```python
S0[:, :, 0, :] = S0[:, :, 0, :] + 2 * rng.standard_normal((20, 20, 20))
```

**Verification:**
```python
assert_equal(np.round(S0ns_first.mean()), 100)
```

### Step 3: Assign S0_first = value

```python
S0_first = S0[:, :, 0, :]
```

**Verification:**
```python
assert_(rmses > 0.0001)
```

### Step 4: Assign S0ns = localpca(...)

```python
S0ns = localpca(S0, sigma=np.std(S0))
```

**Verification:**
```python
assert_equal(np.round(S0ns_first.mean()), 100)
```

### Step 5: Assign S0ns_first = value

```python
S0ns_first = S0ns[:, :, 0, :]
```

### Step 6: Assign rmses = value

```python
rmses = np.sum(np.abs(S0ns_first - S0_first)) / (100.0 * 20.0 * 20.0 * 20.0)
```

### Step 7: Call assert_()

```python
assert_(rmses > 0.0001)
```

### Step 8: Call assert_equal()

```python
assert_equal(np.round(S0ns_first.mean()), 100)
```

### Step 9: Assign rmses = value

```python
rmses = np.sum(np.abs(S0ns_first - S0_first)) / (100.0 * 20.0 * 20.0 * 20.0)
```

### Step 10: Call assert_()

```python
assert_(rmses > 0.0001)
```

### Step 11: Call assert_equal()

```python
assert_equal(np.round(S0ns_first.mean()), 100)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
S0 = 100 * np.ones((20, 20, 20, 20), dtype='f8')
S0[:, :, 0, :] = S0[:, :, 0, :] + 2 * rng.standard_normal((20, 20, 20))
S0_first = S0[:, :, 0, :]
S0ns = localpca(S0, sigma=np.std(S0))
S0ns_first = S0ns[:, :, 0, :]
rmses = np.sum(np.abs(S0ns_first - S0_first)) / (100.0 * 20.0 * 20.0 * 20.0)
assert_(rmses > 0.0001)
assert_equal(np.round(S0ns_first.mean()), 100)
rmses = np.sum(np.abs(S0ns_first - S0_first)) / (100.0 * 20.0 * 20.0 * 20.0)
assert_(rmses > 0.0001)
assert_equal(np.round(S0ns_first.mean()), 100)
```

## Next Steps


---

*Source: test_lpca.py:151 | Complexity: Advanced | Last updated: 2026-05-18*