# How To: Check Inputs Length

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test check inputs length

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
# Fixtures: model
```

## Step-by-Step Guide

### Step 1: Assign iris = load_iris(...)

```python
iris = load_iris()
```

### Step 2: Assign unknown = value

```python
X, y = (iris.data, iris.target)
```

### Step 3: Assign y = value

```python
y = 2 * (y > 0) - 1
```

### Step 4: Assign unknown = to_niimgs(...)

```python
X_, mask = to_niimgs(X, (2, 2, 2))
```

### Step 5: Assign y = value

```python
y = y[:-10]
```

### Step 6: Call model.fit()

```python
model(mask=mask, screening_percentile=100.0, standardize='zscore_sample').fit(X_, y)
```


## Complete Example

```python
# Setup
# Fixtures: model

# Workflow
iris = load_iris()
X, y = (iris.data, iris.target)
y = 2 * (y > 0) - 1
X_, mask = to_niimgs(X, (2, 2, 2))
y = y[:-10]
with pytest.raises(ValueError, match='inconsistent numbers of samples'):
    model(mask=mask, screening_percentile=100.0, standardize='zscore_sample').fit(X_, y)
```

## Next Steps


---

*Source: test_decoder.py:418 | Complexity: Intermediate | Last updated: 2026-05-18*