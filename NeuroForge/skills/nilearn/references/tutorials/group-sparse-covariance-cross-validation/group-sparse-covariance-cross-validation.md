# How To: Group Sparse Covariance Cross Validation

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test group sparse covariance cross validation

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `sklearn.model_selection`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.connectome`
- `nilearn.connectome.group_sparse_cov`

**Setup Required:**
```python
# Fixtures: rng, cv, alphas, n_refinements
```

## Step-by-Step Guide

### Step 1: Assign unknown = generate_group_sparse_gaussian_graphs(...)

```python
signals, _, _ = generate_group_sparse_gaussian_graphs(density=0.1, n_subjects=5, n_features=10, min_n_samples=100, max_n_samples=151, random_state=rng)
```

**Verification:**
```python
assert isinstance(cv_alphas_, list)
```

### Step 2: Assign gsc = GroupSparseCovarianceCV(...)

```python
gsc = GroupSparseCovarianceCV(alphas=alphas, n_refinements=n_refinements, cv=cv)
```

**Verification:**
```python
assert len(cv_alphas_) == alphas * n_refinements
```

### Step 3: Call gsc.fit()

```python
gsc.fit(signals)
```

**Verification:**
```python
assert cv_scores_.shape == (alphas * n_refinements,)
```

### Step 4: Assign cv_alphas_ = value

```python
cv_alphas_ = gsc.cv_alphas_
```

**Verification:**
```python
assert isinstance(cv_alphas_, list)
```

### Step 5: Assign cv_scores_ = value

```python
cv_scores_ = gsc.cv_scores_
```

**Verification:**
```python
assert cv_scores_.shape == (alphas * n_refinements,)
```


## Complete Example

```python
# Setup
# Fixtures: rng, cv, alphas, n_refinements

# Workflow
signals, _, _ = generate_group_sparse_gaussian_graphs(density=0.1, n_subjects=5, n_features=10, min_n_samples=100, max_n_samples=151, random_state=rng)
gsc = GroupSparseCovarianceCV(alphas=alphas, n_refinements=n_refinements, cv=cv)
gsc.fit(signals)
cv_alphas_ = gsc.cv_alphas_
assert isinstance(cv_alphas_, list)
assert len(cv_alphas_) == alphas * n_refinements
cv_scores_ = gsc.cv_scores_
assert cv_scores_.shape == (alphas * n_refinements,)
```

## Next Steps


---

*Source: test_group_sparse_cov.py:205 | Complexity: Intermediate | Last updated: 2026-05-18*