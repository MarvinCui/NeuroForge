# How To: Nlmeans 4D And Mask

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test 4D data with mask using classic method.

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

### Step 1: 'Test 4D data with mask using classic method.'

```python
'Test 4D data with mask using classic method.'
```

**Verification:**
```python
assert_equal(S0.shape, S0n.shape)
```

### Step 2: Assign S0 = value

```python
S0 = 200 * np.ones((20, 20, 20, 3), dtype='f8')
```

**Verification:**
```python
assert_equal(np.round(S0n[10, 10, 10]), 200)
```

### Step 3: Assign mask = np.zeros(...)

```python
mask = np.zeros((20, 20, 20))
```

**Verification:**
```python
assert_equal(S0n[8, 8, 8], 0)
```

### Step 4: Assign unknown = 1

```python
mask[10, 10, 10] = 1
```

### Step 5: Assign S0n = nlmeans(...)

```python
S0n = nlmeans(S0, sigma=1, mask=mask, rician=True, method='classic')
```

### Step 6: Call assert_equal()

```python
assert_equal(S0.shape, S0n.shape)
```

### Step 7: Call assert_equal()

```python
assert_equal(np.round(S0n[10, 10, 10]), 200)
```

### Step 8: Call assert_equal()

```python
assert_equal(S0n[8, 8, 8], 0)
```


## Complete Example

```python
# Workflow
'Test 4D data with mask using classic method.'
S0 = 200 * np.ones((20, 20, 20, 3), dtype='f8')
mask = np.zeros((20, 20, 20))
mask[10, 10, 10] = 1
S0n = nlmeans(S0, sigma=1, mask=mask, rician=True, method='classic')
assert_equal(S0.shape, S0n.shape)
assert_equal(np.round(S0n[10, 10, 10]), 200)
assert_equal(S0n[8, 8, 8], 0)
```

## Next Steps


---

*Source: test_nlmeans.py:95 | Complexity: Advanced | Last updated: 2026-05-18*