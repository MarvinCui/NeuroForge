# How To: Nlmeans Rician Noise Reduction

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: Test rician=True output is non-negative and reduces variance.

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test rician=True output is non-negative and reduces variance.'

```python
'Test rician=True output is non-negative and reduces variance.'
```

**Verification:**
```python
assert_(np.all(denoised >= 0))
```

### Step 2: Assign clean = np.zeros(...)

```python
clean = np.zeros((30, 30, 30), dtype='f8')
```

**Verification:**
```python
assert_(np.var(denoised[core]) < np.var(noisy[core]))
```

### Step 3: Assign unknown = 100.0

```python
clean[8:22, 8:22, 8:22] = 100.0
```

### Step 4: Assign noisy = np.abs(...)

```python
noisy = np.abs(clean + 15.0 * rng.standard_normal((30, 30, 30)))
```

### Step 5: Assign core = value

```python
core = np.s_[10:20, 10:20, 10:20]
```

### Step 6: Assign denoised = nlmeans(...)

```python
denoised = nlmeans(noisy, sigma=15.0, rician=True, method=method, patch_radius=1, block_radius=2)
```

### Step 7: Call assert_()

```python
assert_(np.all(denoised >= 0))
```

### Step 8: Call assert_()

```python
assert_(np.var(denoised[core]) < np.var(noisy[core]))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test rician=True output is non-negative and reduces variance.'
clean = np.zeros((30, 30, 30), dtype='f8')
clean[8:22, 8:22, 8:22] = 100.0
noisy = np.abs(clean + 15.0 * rng.standard_normal((30, 30, 30)))
core = np.s_[10:20, 10:20, 10:20]
for method in ('classic', 'blockwise'):
    denoised = nlmeans(noisy, sigma=15.0, rician=True, method=method, patch_radius=1, block_radius=2)
    assert_(np.all(denoised >= 0))
    assert_(np.var(denoised[core]) < np.var(noisy[core]))
```

## Next Steps


---

*Source: test_nlmeans.py:75 | Complexity: Advanced | Last updated: 2026-05-18*