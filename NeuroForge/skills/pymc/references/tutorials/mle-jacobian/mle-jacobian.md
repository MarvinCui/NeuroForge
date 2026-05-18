# How To: Mle Jacobian

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test MAP / MLE estimation for distributions with flat priors.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `re`
- `numpy`
- `pytest`
- `numpy.testing`
- `pymc`
- `pymc.exceptions`
- `pymc.step_methods.metropolis`
- `pymc.testing`
- `pymc.tuning`
- `tests`
- `tests.models`

**Setup Required:**
```python
# Fixtures: bounded
```

## Step-by-Step Guide

### Step 1: 'Test MAP / MLE estimation for distributions with flat priors.'

```python
'Test MAP / MLE estimation for distributions with flat priors.'
```

**Verification:**
```python
assert_allclose(map_estimate['mu_i'], truth, rtol=rtol)
```

### Step 2: Assign truth = 10.0

```python
truth = 10.0
```

### Step 3: Assign rtol = 0.0001

```python
rtol = 0.0001
```

### Step 4: Assign unknown = models.simple_normal(...)

```python
start, model, _ = models.simple_normal(bounded_prior=bounded)
```

### Step 5: Call assert_allclose()

```python
assert_allclose(map_estimate['mu_i'], truth, rtol=rtol)
```

### Step 6: Assign map_estimate = find_MAP(...)

```python
map_estimate = find_MAP(method='BFGS', model=model)
```


## Complete Example

```python
# Setup
# Fixtures: bounded

# Workflow
'Test MAP / MLE estimation for distributions with flat priors.'
truth = 10.0
rtol = 0.0001
start, model, _ = models.simple_normal(bounded_prior=bounded)
with model:
    map_estimate = find_MAP(method='BFGS', model=model)
assert_allclose(map_estimate['mu_i'], truth, rtol=rtol)
```

## Next Steps


---

*Source: test_starting.py:32 | Complexity: Intermediate | Last updated: 2026-05-18*