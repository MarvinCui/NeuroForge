# How To: Ascm Static

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test ascm static

## Prerequisites

**Required Modules:**
- `nibabel`
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.denoise.adaptive_soft_matching`
- `dipy.denoise.nlmeans`
- `dipy.denoise.noise_estimate`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign S0 = value

```python
S0 = 100 * np.ones((20, 20, 20), dtype='f8')
```

**Verification:**
```python
assert_equal(np.round(S0n.mean()), 100)
```

### Step 2: Assign S0n1 = nlmeans(...)

```python
S0n1 = nlmeans(S0, sigma=0, rician=False, patch_radius=1, block_radius=1)
```

**Verification:**
```python
assert_(np.abs(S0n.mean() - S0.mean()) < 1.0)
```

### Step 3: Assign S0n2 = nlmeans(...)

```python
S0n2 = nlmeans(S0, sigma=0, rician=False, patch_radius=2, block_radius=1)
```

**Verification:**
```python
assert_(np.sum(close_values) / S0.size > 0.95)
```

### Step 4: Assign S0n = adaptive_soft_matching(...)

```python
S0n = adaptive_soft_matching(S0, S0n1, S0n2, 0)
```

### Step 5: Call assert_equal()

```python
assert_equal(np.round(S0n.mean()), 100)
```

### Step 6: Call assert_()

```python
assert_(np.abs(S0n.mean() - S0.mean()) < 1.0)
```

### Step 7: Assign close_values = value

```python
close_values = np.abs(S0n - S0) < 10.0
```

### Step 8: Call assert_()

```python
assert_(np.sum(close_values) / S0.size > 0.95)
```


## Complete Example

```python
# Workflow
S0 = 100 * np.ones((20, 20, 20), dtype='f8')
S0n1 = nlmeans(S0, sigma=0, rician=False, patch_radius=1, block_radius=1)
S0n2 = nlmeans(S0, sigma=0, rician=False, patch_radius=2, block_radius=1)
S0n = adaptive_soft_matching(S0, S0n1, S0n2, 0)
assert_equal(np.round(S0n.mean()), 100)
assert_(np.abs(S0n.mean() - S0.mean()) < 1.0)
close_values = np.abs(S0n - S0) < 10.0
assert_(np.sum(close_values) / S0.size > 0.95)
```

## Next Steps


---

*Source: test_ascm.py:12 | Complexity: Advanced | Last updated: 2026-05-18*