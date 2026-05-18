# How To: Generate Force Simulations Compute Dki

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: generate_force_simulations with compute_dki=True returns AK/RK/MK/KFA.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `dipy.sims.force`
- `dipy.sims.force`
- `dipy.core.gradients`
- `dipy.sims.force`
- `dipy.sims.force`
- `dipy.sims.force`


## Step-by-Step Guide

### Step 1: 'generate_force_simulations with compute_dki=True returns AK/RK/MK/KFA.'

```python
'generate_force_simulations with compute_dki=True returns AK/RK/MK/KFA.'
```

**Verification:**
```python
assert key in sims, f"Key '{key}' missing from simulations"
```

### Step 2: Assign gtab = _make_gtab(...)

```python
gtab = _make_gtab([1000, 2000])
```

**Verification:**
```python
assert arr.shape == (20,), f"Expected shape (20,) for '{key}', got {arr.shape}"
```

### Step 3: Assign sims = generate_force_simulations(...)

```python
sims = generate_force_simulations(gtab, num_simulations=20, batch_size=20, num_cpus=1, compute_dti=True, compute_dki=True, verbose=False)
```

**Verification:**
```python
assert np.any(arr != 0), f"'{key}' is all-zeros – DKI fitting appears skipped"
```

### Step 4: Assign dki_keys = value

```python
dki_keys = ('ak', 'rk', 'mk', 'kfa')
```

**Verification:**
```python
assert key in sims, f"DTI key '{key}' missing"
```

### Step 5: Assign arr = value

```python
arr = sims[key]
```

**Verification:**
```python
assert arr.shape == (20,), f"Expected shape (20,) for '{key}', got {arr.shape}"
```


## Complete Example

```python
# Workflow
'generate_force_simulations with compute_dki=True returns AK/RK/MK/KFA.'
from dipy.sims.force import generate_force_simulations
gtab = _make_gtab([1000, 2000])
sims = generate_force_simulations(gtab, num_simulations=20, batch_size=20, num_cpus=1, compute_dti=True, compute_dki=True, verbose=False)
dki_keys = ('ak', 'rk', 'mk', 'kfa')
for key in dki_keys:
    assert key in sims, f"Key '{key}' missing from simulations"
    arr = sims[key]
    assert arr.shape == (20,), f"Expected shape (20,) for '{key}', got {arr.shape}"
    assert np.any(arr != 0), f"'{key}' is all-zeros – DKI fitting appears skipped"
for key in ('fa', 'md', 'rd'):
    assert key in sims, f"DTI key '{key}' missing"
```

## Next Steps


---

*Source: test_force.py:194 | Complexity: Intermediate | Last updated: 2026-05-18*