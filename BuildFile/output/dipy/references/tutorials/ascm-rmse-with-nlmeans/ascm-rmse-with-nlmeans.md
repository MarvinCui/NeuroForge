# How To: Ascm Rmse With Nlmeans

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test ascm rmse with nlmeans

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `nibabel`
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.denoise.adaptive_soft_matching`
- `dipy.denoise.nlmeans`
- `dipy.denoise.noise_estimate`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign S0 = value

```python
S0 = np.ones((30, 30, 30)) * 100
```

**Verification:**
```python
assert_(np.sum(np.abs(S0 - S0n)) / np.sum(S0) < np.sum(np.abs(S0 - S0n1)) / np.sum(S0))
```

### Step 2: Assign unknown = 50

```python
S0[10:20, 10:20, 10:20] = 50
```

**Verification:**
```python
assert_(np.sum(np.abs(S0 - S0n)) / np.sum(S0) < np.sum(np.abs(S0 - S0_noise)) / np.sum(S0))
```

### Step 3: Assign unknown = 0

```python
S0[20:30, 20:30, 20:30] = 0
```

**Verification:**
```python
assert_(90 < np.mean(S0n) < 110)
```

### Step 4: Assign S0_noise = value

```python
S0_noise = S0 + 20 * rng.standard_normal((30, 30, 30))
```

### Step 5: Call print()

```python
print('Original RMSE', np.sum(np.abs(S0 - S0_noise)) / np.sum(S0))
```

### Step 6: Assign S0n1 = nlmeans(...)

```python
S0n1 = nlmeans(S0_noise, sigma=400, rician=False, patch_radius=1, block_radius=1)
```

### Step 7: Call print()

```python
print('Smaller patch RMSE', np.sum(np.abs(S0 - S0n1)) / np.sum(S0))
```

### Step 8: Assign S0n2 = nlmeans(...)

```python
S0n2 = nlmeans(S0_noise, sigma=400, rician=False, patch_radius=2, block_radius=2)
```

### Step 9: Call print()

```python
print('Larger patch RMSE', np.sum(np.abs(S0 - S0n2)) / np.sum(S0))
```

### Step 10: Assign S0n = adaptive_soft_matching(...)

```python
S0n = adaptive_soft_matching(S0, S0n1, S0n2, 400)
```

### Step 11: Call print()

```python
print('ASCM RMSE', np.sum(np.abs(S0 - S0n)) / np.sum(S0))
```

### Step 12: Call assert_()

```python
assert_(np.sum(np.abs(S0 - S0n)) / np.sum(S0) < np.sum(np.abs(S0 - S0n1)) / np.sum(S0))
```

### Step 13: Call assert_()

```python
assert_(np.sum(np.abs(S0 - S0n)) / np.sum(S0) < np.sum(np.abs(S0 - S0_noise)) / np.sum(S0))
```

### Step 14: Call assert_()

```python
assert_(90 < np.mean(S0n) < 110)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
S0 = np.ones((30, 30, 30)) * 100
S0[10:20, 10:20, 10:20] = 50
S0[20:30, 20:30, 20:30] = 0
S0_noise = S0 + 20 * rng.standard_normal((30, 30, 30))
print('Original RMSE', np.sum(np.abs(S0 - S0_noise)) / np.sum(S0))
S0n1 = nlmeans(S0_noise, sigma=400, rician=False, patch_radius=1, block_radius=1)
print('Smaller patch RMSE', np.sum(np.abs(S0 - S0n1)) / np.sum(S0))
S0n2 = nlmeans(S0_noise, sigma=400, rician=False, patch_radius=2, block_radius=2)
print('Larger patch RMSE', np.sum(np.abs(S0 - S0n2)) / np.sum(S0))
S0n = adaptive_soft_matching(S0, S0n1, S0n2, 400)
print('ASCM RMSE', np.sum(np.abs(S0 - S0n)) / np.sum(S0))
assert_(np.sum(np.abs(S0 - S0n)) / np.sum(S0) < np.sum(np.abs(S0 - S0n1)) / np.sum(S0))
assert_(np.sum(np.abs(S0 - S0n)) / np.sum(S0) < np.sum(np.abs(S0 - S0_noise)) / np.sum(S0))
assert_(90 < np.mean(S0n) < 110)
```

## Next Steps


---

*Source: test_ascm.py:44 | Complexity: Advanced | Last updated: 2026-05-18*