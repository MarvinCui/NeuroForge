# How To: Fixed Effect Contrast Nonzero Effect

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test fixed effect contrast nonzero effect

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `scipy.stats`
- `numpy.testing`
- `sklearn.datasets`
- `sklearn.linear_model`
- `nilearn.glm.contrasts`
- `nilearn.glm.first_level`


## Step-by-Step Guide

### Step 1: Assign unknown = make_regression(...)

```python
X, y = make_regression(n_features=5, n_samples=20, random_state=0)
```

**Verification:**
```python
assert_almost_equal(fixed_effect.effect_size(), coef.ravel()[i])
```

### Step 2: Assign y = value

```python
y = y[:, None]
```

**Verification:**
```python
assert_almost_equal(fixed_effect.effect_size(), coef.ravel()[i])
```

### Step 3: Assign unknown = run_glm(...)

```python
labels, results = run_glm(y, X, 'ols')
```

### Step 4: Assign coef = value

```python
coef = LinearRegression(fit_intercept=False).fit(X, y).coef_
```

### Step 5: Assign contrast = np.zeros(...)

```python
contrast = np.zeros(X.shape[1])
```

### Step 6: Assign unknown = 1.0

```python
contrast[i] = 1.0
```

### Step 7: Assign fixed_effect = compute_fixed_effect_contrast(...)

```python
fixed_effect = compute_fixed_effect_contrast([labels], [results], [contrast])
```

### Step 8: Call assert_almost_equal()

```python
assert_almost_equal(fixed_effect.effect_size(), coef.ravel()[i])
```

### Step 9: Assign fixed_effect = compute_fixed_effect_contrast(...)

```python
fixed_effect = compute_fixed_effect_contrast([labels] * 3, [results] * 3, [contrast] * 3)
```

### Step 10: Call assert_almost_equal()

```python
assert_almost_equal(fixed_effect.effect_size(), coef.ravel()[i])
```


## Complete Example

```python
# Workflow
X, y = make_regression(n_features=5, n_samples=20, random_state=0)
y = y[:, None]
labels, results = run_glm(y, X, 'ols')
coef = LinearRegression(fit_intercept=False).fit(X, y).coef_
for i in range(X.shape[1]):
    contrast = np.zeros(X.shape[1])
    contrast[i] = 1.0
    fixed_effect = compute_fixed_effect_contrast([labels], [results], [contrast])
    assert_almost_equal(fixed_effect.effect_size(), coef.ravel()[i])
    fixed_effect = compute_fixed_effect_contrast([labels] * 3, [results] * 3, [contrast] * 3)
    assert_almost_equal(fixed_effect.effect_size(), coef.ravel()[i])
```

## Next Steps


---

*Source: test_contrasts.py:113 | Complexity: Advanced | Last updated: 2026-05-18*