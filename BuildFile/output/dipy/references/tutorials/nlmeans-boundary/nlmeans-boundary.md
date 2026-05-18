# How To: Nlmeans Boundary

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test boundary preservation with classic method.

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

### Step 1: 'Test boundary preservation with classic method.'

```python
'Test boundary preservation with classic method.'
```

**Verification:**
```python
assert_(S0_denoised[9, 9, 9] > 290)
```

### Step 2: Assign S0 = value

```python
S0 = 100 + np.zeros((20, 20, 20))
```

**Verification:**
```python
assert_(S0_denoised[10, 10, 10] < 110)
```

### Step 3: Assign noise = value

```python
noise = 2 * rng.standard_normal((20, 20, 20))
```

### Step 4: Assign unknown = value

```python
S0[:10, :10, :10] = 300 + noise[:10, :10, :10]
```

### Step 5: Assign S0_denoised = nlmeans(...)

```python
S0_denoised = nlmeans(S0, sigma=np.std(noise), rician=False, method='classic')
```

### Step 6: Call assert_()

```python
assert_(S0_denoised[9, 9, 9] > 290)
```

### Step 7: Call assert_()

```python
assert_(S0_denoised[10, 10, 10] < 110)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test boundary preservation with classic method.'
S0 = 100 + np.zeros((20, 20, 20))
noise = 2 * rng.standard_normal((20, 20, 20))
S0 += noise
S0[:10, :10, :10] = 300 + noise[:10, :10, :10]
S0_denoised = nlmeans(S0, sigma=np.std(noise), rician=False, method='classic')
assert_(S0_denoised[9, 9, 9] > 290)
assert_(S0_denoised[10, 10, 10] < 110)
```

## Next Steps


---

*Source: test_nlmeans.py:61 | Complexity: Intermediate | Last updated: 2026-05-18*