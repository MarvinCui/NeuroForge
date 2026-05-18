# How To: Kurtosis To Smt2 Conversion

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test kurtosis to smt2 conversion

## Prerequisites

**Required Modules:**
- `random`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.reconst.msdki`
- `dipy.reconst.msdki`
- `dipy.sims.voxel`


## Step-by-Step Guide

### Step 1: Assign awf0 = 0

```python
awf0 = 0
```

**Verification:**
```python
assert_almost_equal(kest0, kexp0)
```

### Step 2: Assign kexp0 = 0

```python
kexp0 = 0
```

**Verification:**
```python
assert_almost_equal(kest1, kexp1)
```

### Step 3: Assign kest0 = msk_from_awf(...)

```python
kest0 = msk_from_awf(awf0)
```

**Verification:**
```python
assert_array_almost_equal(awf_from_k, awf_test_array)
```

### Step 4: Call assert_almost_equal()

```python
assert_almost_equal(kest0, kexp0)
```

**Verification:**
```python
assert_array_almost_equal(awf_from_msk(np.array([-0.1, 2.5])), np.array([0.0, 1.0]))
```

### Step 5: Assign awf1 = 1

```python
awf1 = 1
```

**Verification:**
```python
assert_(np.isnan(awf_from_msk(np.array(np.nan))))
```

### Step 6: Assign kexp1 = 2.4

```python
kexp1 = 2.4
```

### Step 7: Assign kest1 = msk_from_awf(...)

```python
kest1 = msk_from_awf(awf1)
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(kest1, kexp1)
```

### Step 9: Assign awf_test_array = np.linspace(...)

```python
awf_test_array = np.linspace(0, 1, 100)
```

### Step 10: Assign k_exp = msk_from_awf(...)

```python
k_exp = msk_from_awf(awf_test_array)
```

### Step 11: Assign awf_from_k = awf_from_msk(...)

```python
awf_from_k = awf_from_msk(k_exp)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(awf_from_k, awf_test_array)
```

### Step 13: Call assert_array_almost_equal()

```python
assert_array_almost_equal(awf_from_msk(np.array([-0.1, 2.5])), np.array([0.0, 1.0]))
```

### Step 14: Call assert_()

```python
assert_(np.isnan(awf_from_msk(np.array(np.nan))))
```


## Complete Example

```python
# Workflow
awf0 = 0
kexp0 = 0
kest0 = msk_from_awf(awf0)
assert_almost_equal(kest0, kexp0)
awf1 = 1
kexp1 = 2.4
kest1 = msk_from_awf(awf1)
assert_almost_equal(kest1, kexp1)
awf_test_array = np.linspace(0, 1, 100)
k_exp = msk_from_awf(awf_test_array)
awf_from_k = awf_from_msk(k_exp)
assert_array_almost_equal(awf_from_k, awf_test_array)
assert_array_almost_equal(awf_from_msk(np.array([-0.1, 2.5])), np.array([0.0, 1.0]))
assert_(np.isnan(awf_from_msk(np.array(np.nan))))
```

## Next Steps


---

*Source: test_msdki.py:236 | Complexity: Advanced | Last updated: 2026-05-18*