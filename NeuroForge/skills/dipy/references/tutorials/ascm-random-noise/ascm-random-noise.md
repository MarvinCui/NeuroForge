# How To: Ascm Random Noise

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test ascm random noise

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
S0 = 100 + 2 * rng.standard_normal((22, 23, 30))
```

**Verification:**
```python
assert_(np.abs(S0n.mean() - S0.mean()) < 3.0)
```

### Step 2: Assign S0n1 = nlmeans(...)

```python
S0n1 = nlmeans(S0, sigma=1, rician=False, patch_radius=1, block_radius=1)
```

**Verification:**
```python
assert_(np.isfinite(S0n).all())
```

### Step 3: Assign S0n2 = nlmeans(...)

```python
S0n2 = nlmeans(S0, sigma=1, rician=False, patch_radius=2, block_radius=1)
```

**Verification:**
```python
assert_(not np.isnan(S0n).any())
```

### Step 4: Assign S0n = adaptive_soft_matching(...)

```python
S0n = adaptive_soft_matching(S0, S0n1, S0n2, 1)
```

**Verification:**
```python
assert_(S0n.std() < S0.std() * 1.5)
```

### Step 5: Call assert_()

```python
assert_(np.abs(S0n.mean() - S0.mean()) < 3.0)
```

**Verification:**
```python
assert_(S0n.min() > 0)
```

### Step 6: Call assert_()

```python
assert_(np.isfinite(S0n).all())
```

**Verification:**
```python
assert_(S0n.max() < 200)
```

### Step 7: Call assert_()

```python
assert_(not np.isnan(S0n).any())
```

**Verification:**
```python
assert_(np.mean(reasonable_values) > 0.95)
```

### Step 8: Call assert_()

```python
assert_(S0n.std() < S0.std() * 1.5)
```

### Step 9: Call assert_()

```python
assert_(S0n.min() > 0)
```

### Step 10: Call assert_()

```python
assert_(S0n.max() < 200)
```

### Step 11: Assign reasonable_values = value

```python
reasonable_values = np.abs(S0n - S0n.mean()) < 3 * S0n.std()
```

### Step 12: Call assert_()

```python
assert_(np.mean(reasonable_values) > 0.95)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
S0 = 100 + 2 * rng.standard_normal((22, 23, 30))
S0n1 = nlmeans(S0, sigma=1, rician=False, patch_radius=1, block_radius=1)
S0n2 = nlmeans(S0, sigma=1, rician=False, patch_radius=2, block_radius=1)
S0n = adaptive_soft_matching(S0, S0n1, S0n2, 1)
assert_(np.abs(S0n.mean() - S0.mean()) < 3.0)
assert_(np.isfinite(S0n).all())
assert_(not np.isnan(S0n).any())
assert_(S0n.std() < S0.std() * 1.5)
assert_(S0n.min() > 0)
assert_(S0n.max() < 200)
reasonable_values = np.abs(S0n - S0n.mean()) < 3 * S0n.std()
assert_(np.mean(reasonable_values) > 0.95)
```

## Next Steps


---

*Source: test_ascm.py:26 | Complexity: Advanced | Last updated: 2026-05-18*