# How To: Sharpness

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: test sharpness

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
assert_(edg2 > edg1)
```

### Step 2: Assign unknown = 50

```python
S0[10:20, 10:20, 10:20] = 50
```

**Verification:**
```python
assert_(edg2 > edg)
```

### Step 3: Assign unknown = 0

```python
S0[20:30, 20:30, 20:30] = 0
```

**Verification:**
```python
assert_(np.abs(edg1 - edg) < 1.5)
```

### Step 4: Assign S0_noise = value

```python
S0_noise = S0 + 20 * rng.standard_normal((30, 30, 30))
```

### Step 5: Assign S0n1 = nlmeans(...)

```python
S0n1 = nlmeans(S0_noise, sigma=400, rician=False, patch_radius=1, block_radius=1)
```

### Step 6: Assign edg1 = np.abs(...)

```python
edg1 = np.abs(np.mean(S0n1[8, 10:20, 10:20] - S0n1[12, 10:20, 10:20]) - 50)
```

### Step 7: Call print()

```python
print('Edge gradient smaller patch', edg1)
```

### Step 8: Assign S0n2 = nlmeans(...)

```python
S0n2 = nlmeans(S0_noise, sigma=400, rician=False, patch_radius=2, block_radius=2)
```

### Step 9: Assign edg2 = np.abs(...)

```python
edg2 = np.abs(np.mean(S0n2[8, 10:20, 10:20] - S0n2[12, 10:20, 10:20]) - 50)
```

### Step 10: Call print()

```python
print('Edge gradient larger patch', edg2)
```

### Step 11: Assign S0n = adaptive_soft_matching(...)

```python
S0n = adaptive_soft_matching(S0, S0n1, S0n2, 400)
```

### Step 12: Assign edg = np.abs(...)

```python
edg = np.abs(np.mean(S0n[8, 10:20, 10:20] - S0n[12, 10:20, 10:20]) - 50)
```

### Step 13: Call print()

```python
print('Edge gradient ASCM', edg)
```

### Step 14: Call assert_()

```python
assert_(edg2 > edg1)
```

### Step 15: Call assert_()

```python
assert_(edg2 > edg)
```

### Step 16: Call assert_()

```python
assert_(np.abs(edg1 - edg) < 1.5)
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
S0n1 = nlmeans(S0_noise, sigma=400, rician=False, patch_radius=1, block_radius=1)
edg1 = np.abs(np.mean(S0n1[8, 10:20, 10:20] - S0n1[12, 10:20, 10:20]) - 50)
print('Edge gradient smaller patch', edg1)
S0n2 = nlmeans(S0_noise, sigma=400, rician=False, patch_radius=2, block_radius=2)
edg2 = np.abs(np.mean(S0n2[8, 10:20, 10:20] - S0n2[12, 10:20, 10:20]) - 50)
print('Edge gradient larger patch', edg2)
S0n = adaptive_soft_matching(S0, S0n1, S0n2, 400)
edg = np.abs(np.mean(S0n[8, 10:20, 10:20] - S0n[12, 10:20, 10:20]) - 50)
print('Edge gradient ASCM', edg)
assert_(edg2 > edg1)
assert_(edg2 > edg)
assert_(np.abs(edg1 - edg) < 1.5)
```

## Next Steps


---

*Source: test_ascm.py:70 | Complexity: Advanced | Last updated: 2026-05-18*