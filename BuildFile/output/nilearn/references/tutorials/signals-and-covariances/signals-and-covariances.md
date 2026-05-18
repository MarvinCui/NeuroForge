# How To: Signals And Covariances

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: signals and covariances

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `copy`
- `warnings`
- `math`
- `numpy`
- `pytest`
- `numpy.testing`
- `pandas`
- `scipy`
- `sklearn.covariance`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.extmath`
- `nilearn._utils.versions`
- `nilearn.connectome.connectivity_matrices`
- `nilearn.tests.test_signal`

**Setup Required:**
```python
# Fixtures: cov_estimator
```

## Step-by-Step Guide

### Step 1: Assign unknown = _signals(...)

```python
signals, _ = _signals()
```

### Step 2: Assign emp_covs = value

```python
emp_covs = []
```

### Step 3: Assign ledoit_covs = value

```python
ledoit_covs = []
```

### Step 4: Assign ledoit_estimator = LedoitWolf(...)

```python
ledoit_estimator = LedoitWolf()
```

### Step 5: Assign n_samples = value

```python
n_samples = 200 + k
```

### Step 6: Call emp_covs.append()

```python
emp_covs.append(signal_.T.dot(signal_) / n_samples)
```

### Step 7: Call ledoit_covs.append()

```python
ledoit_covs.append(ledoit_estimator.fit(signal_).covariance_)
```


## Complete Example

```python
# Setup
# Fixtures: cov_estimator

# Workflow
signals, _ = _signals()
emp_covs = []
ledoit_covs = []
ledoit_estimator = LedoitWolf()
for k, signal_ in enumerate(signals):
    n_samples = 200 + k
    signal_ -= signal_.mean(axis=0)
    emp_covs.append(signal_.T.dot(signal_) / n_samples)
    ledoit_covs.append(ledoit_estimator.fit(signal_).covariance_)
if isinstance(cov_estimator, LedoitWolf):
    return (signals, ledoit_covs)
elif isinstance(cov_estimator, EmpiricalCovariance):
    return (signals, emp_covs)
```

## Next Steps


---

*Source: test_connectivity_matrices.py:194 | Complexity: Intermediate | Last updated: 2026-05-18*