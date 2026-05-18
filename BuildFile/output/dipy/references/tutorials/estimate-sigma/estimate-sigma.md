# How To: Estimate Sigma

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test estimate sigma

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

### Step 1: Assign sigma = estimate_sigma(...)

```python
sigma = estimate_sigma(np.ones((7, 7, 7)), disable_background_masking=True)
```

**Verification:**
```python
assert_equal(sigma, 0.0)
```

### Step 2: Call assert_equal()

```python
assert_equal(sigma, 0.0)
```

**Verification:**
```python
assert_equal(sigma, np.array([0.0, 0.0, 0.0]))
```

### Step 3: Assign sigma = estimate_sigma(...)

```python
sigma = estimate_sigma(np.ones((7, 7, 7, 3)), disable_background_masking=True)
```

**Verification:**
```python
assert_equal(sigma, 0.0)
```

### Step 4: Call assert_equal()

```python
assert_equal(sigma, np.array([0.0, 0.0, 0.0]))
```

**Verification:**
```python
assert_equal(sigma, np.array([0.0, 0.0, 0.0]))
```

### Step 5: Assign sigma = estimate_sigma(...)

```python
sigma = estimate_sigma(5 * np.ones((7, 7, 7)), disable_background_masking=False)
```

**Verification:**
```python
assert_array_almost_equal(sigma, 0.10286889997472792 / np.sqrt(0.42920367320510366))
```

### Step 6: Call assert_equal()

```python
assert_equal(sigma, 0.0)
```

**Verification:**
```python
assert_array_almost_equal(sigma, np.array([0.10286889997472792 / np.sqrt(0.42920367320510366), 0.10286889997472792 / np.sqrt(0.42920367320510366), 0.10286889997472792 / np.sqrt(0.42920367320510366)]))
```

### Step 7: Assign sigma = estimate_sigma(...)

```python
sigma = estimate_sigma(5 * np.ones((7, 7, 7, 3)), disable_background_masking=False)
```

**Verification:**
```python
assert_array_almost_equal(sigma, 0.46291005 / np.sqrt(0.4834941393603609))
```

### Step 8: Call assert_equal()

```python
assert_equal(sigma, np.array([0.0, 0.0, 0.0]))
```

**Verification:**
```python
assert_array_almost_equal(sigma, 0.46291005 / np.sqrt(1))
```

### Step 9: Assign arr = np.zeros(...)

```python
arr = np.zeros((3, 3, 3))
```

**Verification:**
```python
assert_array_almost_equal(sigma, np.array([0.46291005 / np.sqrt(0.4946862482541263), 0.46291005 / np.sqrt(0.4946862482541263), 0.46291005 / np.sqrt(0.4946862482541263)]))
```

### Step 10: Assign unknown = 1

```python
arr[0, 0, 0] = 1
```

### Step 11: Assign sigma = estimate_sigma(...)

```python
sigma = estimate_sigma(arr, disable_background_masking=False, N=1)
```

### Step 12: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sigma, 0.10286889997472792 / np.sqrt(0.42920367320510366))
```

### Step 13: Assign arr = np.zeros(...)

```python
arr = np.zeros((3, 3, 3, 3))
```

### Step 14: Assign unknown = 1

```python
arr[0, 0, 0] = 1
```

### Step 15: Assign sigma = estimate_sigma(...)

```python
sigma = estimate_sigma(arr, disable_background_masking=False, N=1)
```

### Step 16: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sigma, np.array([0.10286889997472792 / np.sqrt(0.42920367320510366), 0.10286889997472792 / np.sqrt(0.42920367320510366), 0.10286889997472792 / np.sqrt(0.42920367320510366)]))
```

### Step 17: Assign arr = np.zeros(...)

```python
arr = np.zeros((3, 3, 3))
```

### Step 18: Assign unknown = 1

```python
arr[0, 0, 0] = 1
```

### Step 19: Assign sigma = estimate_sigma(...)

```python
sigma = estimate_sigma(arr, disable_background_masking=True, N=4)
```

### Step 20: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sigma, 0.46291005 / np.sqrt(0.4834941393603609))
```

### Step 21: Assign arr = np.zeros(...)

```python
arr = np.zeros((3, 3, 3))
```

### Step 22: Assign unknown = 1

```python
arr[0, 0, 0] = 1
```

### Step 23: Assign sigma = estimate_sigma(...)

```python
sigma = estimate_sigma(arr, disable_background_masking=True, N=0)
```

### Step 24: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sigma, 0.46291005 / np.sqrt(1))
```

### Step 25: Assign arr = np.zeros(...)

```python
arr = np.zeros((3, 3, 3, 3))
```

### Step 26: Assign unknown = 1

```python
arr[0, 0, 0] = 1
```

### Step 27: Assign sigma = estimate_sigma(...)

```python
sigma = estimate_sigma(arr, disable_background_masking=True, N=12)
```

### Step 28: Call assert_array_almost_equal()

```python
assert_array_almost_equal(sigma, np.array([0.46291005 / np.sqrt(0.4946862482541263), 0.46291005 / np.sqrt(0.4946862482541263), 0.46291005 / np.sqrt(0.4946862482541263)]))
```


## Complete Example

```python
# Workflow
sigma = estimate_sigma(np.ones((7, 7, 7)), disable_background_masking=True)
assert_equal(sigma, 0.0)
sigma = estimate_sigma(np.ones((7, 7, 7, 3)), disable_background_masking=True)
assert_equal(sigma, np.array([0.0, 0.0, 0.0]))
sigma = estimate_sigma(5 * np.ones((7, 7, 7)), disable_background_masking=False)
assert_equal(sigma, 0.0)
sigma = estimate_sigma(5 * np.ones((7, 7, 7, 3)), disable_background_masking=False)
assert_equal(sigma, np.array([0.0, 0.0, 0.0]))
arr = np.zeros((3, 3, 3))
arr[0, 0, 0] = 1
sigma = estimate_sigma(arr, disable_background_masking=False, N=1)
assert_array_almost_equal(sigma, 0.10286889997472792 / np.sqrt(0.42920367320510366))
arr = np.zeros((3, 3, 3, 3))
arr[0, 0, 0] = 1
sigma = estimate_sigma(arr, disable_background_masking=False, N=1)
assert_array_almost_equal(sigma, np.array([0.10286889997472792 / np.sqrt(0.42920367320510366), 0.10286889997472792 / np.sqrt(0.42920367320510366), 0.10286889997472792 / np.sqrt(0.42920367320510366)]))
arr = np.zeros((3, 3, 3))
arr[0, 0, 0] = 1
sigma = estimate_sigma(arr, disable_background_masking=True, N=4)
assert_array_almost_equal(sigma, 0.46291005 / np.sqrt(0.4834941393603609))
arr = np.zeros((3, 3, 3))
arr[0, 0, 0] = 1
sigma = estimate_sigma(arr, disable_background_masking=True, N=0)
assert_array_almost_equal(sigma, 0.46291005 / np.sqrt(1))
arr = np.zeros((3, 3, 3, 3))
arr[0, 0, 0] = 1
sigma = estimate_sigma(arr, disable_background_masking=True, N=12)
assert_array_almost_equal(sigma, np.array([0.46291005 / np.sqrt(0.4946862482541263), 0.46291005 / np.sqrt(0.4946862482541263), 0.46291005 / np.sqrt(0.4946862482541263)]))
```

## Next Steps


---

*Source: test_noise_estimate.py:132 | Complexity: Advanced | Last updated: 2026-05-18*