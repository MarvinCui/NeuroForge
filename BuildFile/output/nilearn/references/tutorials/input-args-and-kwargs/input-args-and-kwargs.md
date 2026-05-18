# How To: Input Args And Kwargs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: pytest

## Overview

Instantiate mfista: test input args and kwargs

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn.decoding._objective_functions`
- `nilearn.decoding._proximal_operators`
- `nilearn.decoding.fista`

**Setup Required:**
```python
# Fixtures: cb_retval, verbose, dgap_factor, rng
```

## Step-by-Step Guide

### Step 1: Assign unknown = mfista(...)

```python
best_w, objective, init = mfista(f1_grad, f2_prox, total_energy, 1.0, p, dgap_factor=dgap_factor, callback=lambda _: cb_retval, verbose=verbose, max_iter=100)
```


## Complete Example

```python
# Setup
# Fixtures: cb_retval, verbose, dgap_factor, rng

# Workflow
best_w, objective, init = mfista(f1_grad, f2_prox, total_energy, 1.0, p, dgap_factor=dgap_factor, callback=lambda _: cb_retval, verbose=verbose, max_iter=100)
```

## Next Steps


---

*Source: test_fista.py:71 | Complexity: Beginner | Last updated: 2026-05-18*