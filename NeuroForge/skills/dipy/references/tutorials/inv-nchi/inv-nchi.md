# How To: Inv Nchi

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test inv nchi

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.denoise.noise_estimate`
- `dipy.denoise.pca_noise_estimate`
- `dipy.io.image`
- `dipy.testing`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign N = 8

```python
N = 8
```

**Verification:**
```python
assert_almost_equal(lambdaMinus, 6.464855180579397)
```

### Step 2: Assign K = 20

```python
K = 20
```

**Verification:**
```python
assert_almost_equal(lambdaPlus, 9.722849086419043)
```

### Step 3: Assign alpha = 0.01

```python
alpha = 0.01
```

### Step 4: Assign lambdaMinus = _inv_nchi_cdf(...)

```python
lambdaMinus = _inv_nchi_cdf(N, K, alpha / 2)
```

### Step 5: Assign lambdaPlus = _inv_nchi_cdf(...)

```python
lambdaPlus = _inv_nchi_cdf(N, K, 1 - alpha / 2)
```

### Step 6: Call assert_almost_equal()

```python
assert_almost_equal(lambdaMinus, 6.464855180579397)
```

### Step 7: Call assert_almost_equal()

```python
assert_almost_equal(lambdaPlus, 9.722849086419043)
```


## Complete Example

```python
# Workflow
N = 8
K = 20
alpha = 0.01
lambdaMinus = _inv_nchi_cdf(N, K, alpha / 2)
lambdaPlus = _inv_nchi_cdf(N, K, 1 - alpha / 2)
assert_almost_equal(lambdaMinus, 6.464855180579397)
assert_almost_equal(lambdaPlus, 9.722849086419043)
```

## Next Steps


---

*Source: test_noise_estimate.py:23 | Complexity: Intermediate | Last updated: 2026-05-18*