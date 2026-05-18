# How To: Cross Validation

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Check cross-validation scheme and fit attribute with groups enabled.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `collections`
- `numbers`
- `warnings`
- `numpy`
- `pytest`
- `nibabel`
- `numpy.testing`
- `sklearn`
- `sklearn`
- `sklearn.datasets`
- `sklearn.dummy`
- `sklearn.ensemble`
- `sklearn.exceptions`
- `sklearn.linear_model`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.preprocessing`
- `sklearn.svm`
- `sklearn.utils._testing`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.decoding`
- `nilearn.decoding._utils`
- `nilearn.decoding.decoder`
- `nilearn.decoding.tests.test_same_api`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: estimator, data, cv
```

## Step-by-Step Guide

### Step 1: 'Check cross-validation scheme and fit attribute with groups enabled.'

```python
'Check cross-validation scheme and fit attribute with groups enabled.'
```

**Verification:**
```python
assert n_cv == 10
```

### Step 2: Assign unknown = data

```python
X, y, mask = data
```

**Verification:**
```python
assert n_cv == 30
```

### Step 3: Assign model = estimator(...)

```python
model = estimator(mask=mask, cv=cv)
```

**Verification:**
```python
assert accuracy_score(y, y_pred) > 0.9
```

### Step 4: Assign groups = None

```python
groups = None
```

**Verification:**
```python
assert r2_score(y, y_pred) > 0.9
```

### Step 5: Call model.fit()

```python
model.fit(X, y, groups=groups)
```

### Step 6: Assign y_pred = model.predict(...)

```python
y_pred = model.predict(X)
```

### Step 7: Assign groups = _rng.binomial(...)

```python
groups = _rng(0).binomial(2, 0.3, size=len(y))
```

### Step 8: Assign n_cv = len(...)

```python
n_cv = len(model.cv_)
```

**Verification:**
```python
assert accuracy_score(y, y_pred) > 0.9
```


## Complete Example

```python
# Setup
# Fixtures: estimator, data, cv

# Workflow
'Check cross-validation scheme and fit attribute with groups enabled.'
X, y, mask = data
model = estimator(mask=mask, cv=cv)
groups = None
if isinstance(cv, LeaveOneGroupOut):
    groups = _rng(0).binomial(2, 0.3, size=len(y))
model.fit(X, y, groups=groups)
y_pred = model.predict(X)
if cv is None:
    n_cv = len(model.cv_)
    if isinstance(model, (Decoder, DecoderRegressor)):
        assert n_cv == 10
    else:
        assert n_cv == 30
if isinstance(model, Decoder):
    assert accuracy_score(y, y_pred) > 0.9
elif isinstance(model, DecoderRegressor):
    assert r2_score(y, y_pred) > 0.9
```

## Next Steps


---

*Source: test_decoder.py:754 | Complexity: Advanced | Last updated: 2026-05-18*