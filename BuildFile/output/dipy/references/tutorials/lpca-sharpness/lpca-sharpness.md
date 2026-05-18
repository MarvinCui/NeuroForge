# How To: Lpca Sharpness

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test lpca sharpness

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
S0 = np.ones((30, 30, 30, 20), dtype=np.float64) * 100
```

**Verification:**
```python
assert_(edgs < 2)
```

### Step 2: Assign unknown = 50

```python
S0[10:20, 10:20, 10:20, :] = 50
```

### Step 3: Assign unknown = 0

```python
S0[20:30, 20:30, 20:30, :] = 0
```

### Step 4: Assign S0 = value

```python
S0 = S0 + 20 * rng.standard_normal((30, 30, 30, 20))
```

### Step 5: Assign S0ns = localpca(...)

```python
S0ns = localpca(S0, sigma=20.0)
```

### Step 6: Assign edgs = np.abs(...)

```python
edgs = np.abs(np.mean(S0ns[8, 10:20, 10:20] - S0ns[12, 10:20, 10:20]) - 50)
```

### Step 7: Call assert_()

```python
assert_(edgs < 2)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
S0 = np.ones((30, 30, 30, 20), dtype=np.float64) * 100
S0[10:20, 10:20, 10:20, :] = 50
S0[20:30, 20:30, 20:30, :] = 0
S0 = S0 + 20 * rng.standard_normal((30, 30, 30, 20))
S0ns = localpca(S0, sigma=20.0)
edgs = np.abs(np.mean(S0ns[8, 10:20, 10:20] - S0ns[12, 10:20, 10:20]) - 50)
assert_(edgs < 2)
```

## Next Steps


---

*Source: test_lpca.py:215 | Complexity: Intermediate | Last updated: 2026-05-18*