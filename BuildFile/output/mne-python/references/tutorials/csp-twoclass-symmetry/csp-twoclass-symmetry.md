# How To: Csp Twoclass Symmetry

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test that CSP is symmetric when swapping classes.

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `sklearn.linear_model`
- `sklearn.model_selection`
- `sklearn.pipeline`
- `sklearn.svm`
- `sklearn.utils.estimator_checks`
- `mne`
- `mne.decoding`
- `mne.decoding.csp`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test that CSP is symmetric when swapping classes.'

```python
'Test that CSP is symmetric when swapping classes.'
```

**Verification:**
```python
assert_array_almost_equal(log_power_ratio_ab, log_power_ratio_ba)
```

### Step 2: Assign unknown = deterministic_toy_data(...)

```python
x, y = deterministic_toy_data(['class_a', 'class_b'])
```

### Step 3: Assign csp = CSP(...)

```python
csp = CSP(norm_trace=False, transform_into='average_power', log=True)
```

### Step 4: Assign log_power = csp.fit_transform(...)

```python
log_power = csp.fit_transform(x, y)
```

### Step 5: Assign log_power_ratio_ab = value

```python
log_power_ratio_ab = log_power[0] - log_power[1]
```

### Step 6: Assign unknown = deterministic_toy_data(...)

```python
x, y = deterministic_toy_data(['class_b', 'class_a'])
```

### Step 7: Assign csp = CSP(...)

```python
csp = CSP(norm_trace=False, transform_into='average_power', log=True)
```

### Step 8: Assign log_power = csp.fit_transform(...)

```python
log_power = csp.fit_transform(x, y)
```

### Step 9: Assign log_power_ratio_ba = value

```python
log_power_ratio_ba = log_power[0] - log_power[1]
```

### Step 10: Call assert_array_almost_equal()

```python
assert_array_almost_equal(log_power_ratio_ab, log_power_ratio_ba)
```


## Complete Example

```python
# Workflow
'Test that CSP is symmetric when swapping classes.'
x, y = deterministic_toy_data(['class_a', 'class_b'])
csp = CSP(norm_trace=False, transform_into='average_power', log=True)
log_power = csp.fit_transform(x, y)
log_power_ratio_ab = log_power[0] - log_power[1]
x, y = deterministic_toy_data(['class_b', 'class_a'])
csp = CSP(norm_trace=False, transform_into='average_power', log=True)
log_power = csp.fit_transform(x, y)
log_power_ratio_ba = log_power[0] - log_power[1]
assert_array_almost_equal(log_power_ratio_ab, log_power_ratio_ba)
```

## Next Steps


---

*Source: test_csp.py:460 | Complexity: Advanced | Last updated: 2026-05-18*