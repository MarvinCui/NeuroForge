# How To: Get Coef Inverse Transform

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test get_coef with and without inverse_transform.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `platform`
- `contextlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn`
- `sklearn.base`
- `sklearn.base`
- `sklearn.base`
- `sklearn.decomposition`
- `sklearn.discriminant_analysis`
- `sklearn.linear_model`
- `sklearn.model_selection`
- `sklearn.multiclass`
- `sklearn.pipeline`
- `sklearn.preprocessing`
- `sklearn.utils.estimator_checks`
- `mne`
- `mne.decoding`
- `mne.decoding.base`
- `mne.decoding.search_light`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: inverse, clf
```

## Step-by-Step Guide

### Step 1: 'Test get_coef with and without inverse_transform.'

```python
'Test get_coef with and without inverse_transform.'
```

**Verification:**
```python
assert_array_equal(filters.shape, patterns.shape, X.shape[1:])
```

### Step 2: Assign unknown = _make_data(...)

```python
X, y, A = _make_data(n_samples=1000, n_features=3, n_targets=1)
```

**Verification:**
```python
assert_equal(patterns[0, 0], -patterns[0, 1])
```

### Step 3: Assign X = np.transpose(...)

```python
X = np.transpose([X, -X], [1, 2, 0])
```

**Verification:**
```python
assert_equal(filters_t, filters[:, t])
```

### Step 4: Call clf.fit()

```python
clf.fit(X, y)
```

### Step 5: Assign patterns = get_coef(...)

```python
patterns = get_coef(clf, 'patterns_', inverse)
```

### Step 6: Assign filters = get_coef(...)

```python
filters = get_coef(clf, 'filters_', inverse)
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(filters.shape, patterns.shape, X.shape[1:])
```

### Step 8: Call assert_equal()

```python
assert_equal(patterns[0, 0], -patterns[0, 1])
```

### Step 9: Call assert_equal()

```python
assert_equal(filters_t, filters[:, t])
```

### Step 10: Assign est_t = value

```python
est_t = clf.named_steps['slidingestimator'].estimators_[t]
```

### Step 11: Assign filters_t = get_coef(...)

```python
filters_t = get_coef(est_t, 'filters_', inverse)
```

### Step 12: Assign est_t = value

```python
est_t = clf.estimators_[t]
```

### Step 13: Assign filters_t = get_coef(...)

```python
filters_t = get_coef(est_t, 'filters_', inverse)
```

### Step 14: Assign filters_t = value

```python
filters_t = clf[0].inverse_transform(filters_t.reshape(1, -1))[0]
```


## Complete Example

```python
# Setup
# Fixtures: inverse, clf

# Workflow
'Test get_coef with and without inverse_transform.'
X, y, A = _make_data(n_samples=1000, n_features=3, n_targets=1)
X = np.transpose([X, -X], [1, 2, 0])
clf.fit(X, y)
patterns = get_coef(clf, 'patterns_', inverse)
filters = get_coef(clf, 'filters_', inverse)
assert_array_equal(filters.shape, patterns.shape, X.shape[1:])
assert_equal(patterns[0, 0], -patterns[0, 1])
for t in [0, 1]:
    if hasattr(clf, 'named_steps'):
        est_t = clf.named_steps['slidingestimator'].estimators_[t]
        filters_t = get_coef(est_t, 'filters_', inverse)
        if inverse:
            filters_t = clf[0].inverse_transform(filters_t.reshape(1, -1))[0]
    else:
        est_t = clf.estimators_[t]
        filters_t = get_coef(est_t, 'filters_', inverse)
    assert_equal(filters_t, filters[:, t])
```

## Next Steps


---

*Source: test_base.py:267 | Complexity: Advanced | Last updated: 2026-05-18*