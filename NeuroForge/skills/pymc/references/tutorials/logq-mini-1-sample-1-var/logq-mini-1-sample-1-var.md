# How To: Logq Mini 1 Sample 1 Var

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logq mini 1 sample 1 var

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `functools`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.testing`
- `pymc.variational`
- `pymc.variational.approximations`
- `tests.helpers`
- `cloudpickle`
- `cloudpickle`

**Setup Required:**
```python
# Fixtures: parametric_grouped_approxes, three_var_model
```

## Step-by-Step Guide

### Step 1: Assign unknown = parametric_grouped_approxes

```python
cls, kw = parametric_grouped_approxes
```

### Step 2: Assign approx = cls(...)

```python
approx = cls([three_var_model.one], model=three_var_model, **kw)
```

### Step 3: Assign logq = value

```python
logq = approx.logq
```

### Step 4: Assign logq = approx.set_size_and_deterministic(...)

```python
logq = approx.set_size_and_deterministic(logq, 1, 0)
```

### Step 5: Call logq.eval()

```python
logq.eval()
```


## Complete Example

```python
# Setup
# Fixtures: parametric_grouped_approxes, three_var_model

# Workflow
cls, kw = parametric_grouped_approxes
approx = cls([three_var_model.one], model=three_var_model, **kw)
logq = approx.logq
logq = approx.set_size_and_deterministic(logq, 1, 0)
logq.eval()
```

## Next Steps


---

*Source: test_opvi.py:250 | Complexity: Intermediate | Last updated: 2026-05-18*