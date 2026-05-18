# How To: Screening Space Net

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test screening space net

## Prerequisites

**Required Modules:**
- `functools`
- `numpy`
- `pytest`
- `numpy.testing`
- `scipy`
- `sklearn.datasets`
- `sklearn.linear_model`
- `sklearn.linear_model._coordinate_descent`
- `sklearn.metrics`
- `sklearn.model_selection`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.decoding._utils`
- `nilearn.decoding.space_net`
- `nilearn.decoding.space_net_solvers`
- `nilearn.decoding.tests._testing`
- `nilearn.decoding.tests.test_same_api`
- `nilearn.image`
- `nilearn.maskers`


## Step-by-Step Guide

### Step 1: Assign size = 4

```python
size = 4
```

**Verification:**
```python
assert screening_percentile == 100
```

### Step 2: Assign unknown = create_graph_net_simulation_data(...)

```python
X_, *_ = create_graph_net_simulation_data(snr=1.0, n_samples=10, size=size, n_points=5, random_state=42)
```

### Step 3: Assign unknown = to_niimgs(...)

```python
_, mask = to_niimgs(X_, [size] * 3)
```

**Verification:**
```python
assert screening_percentile == 100
```

### Step 4: Assign screening_percentile = adjust_screening_percentile(...)

```python
screening_percentile = adjust_screening_percentile(10, mask)
```

### Step 5: Assign screening_percentile = adjust_screening_percentile(...)

```python
screening_percentile = adjust_screening_percentile(10, mask, verbose)
```


## Complete Example

```python
# Workflow
size = 4
X_, *_ = create_graph_net_simulation_data(snr=1.0, n_samples=10, size=size, n_points=5, random_state=42)
_, mask = to_niimgs(X_, [size] * 3)
for verbose in [0, 1]:
    with pytest.warns(UserWarning):
        screening_percentile = adjust_screening_percentile(10, mask, verbose)
with pytest.warns(UserWarning):
    screening_percentile = adjust_screening_percentile(10, mask)
assert screening_percentile == 100
```

## Next Steps


---

*Source: test_space_net.py:151 | Complexity: Intermediate | Last updated: 2026-05-18*