# How To: Dirichlet Multinomial Dims

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test we can draw from a DM with a shape defined by dims in the JAX backend,
after freezing those dims.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `pymc`
- `pymc`
- `pymc.model.transform.optimization`

**Setup Required:**
```python
# Fixtures: mode
```

## Step-by-Step Guide

### Step 1: 'Test we can draw from a DM with a shape defined by dims in the JAX backend,\n    after freezing those dims.\n    '

```python
'Test we can draw from a DM with a shape defined by dims in the JAX backend,\n    after freezing those dims.\n    '
```

### Step 2: Assign dm_draws = pm.draw(...)

```python
dm_draws = pm.draw(dm, mode=mode, random_seed=36)
```

### Step 3: Call np.testing.assert_equal()

```python
np.testing.assert_equal(dm_draws, np.eye(3) * 5)
```

### Step 4: Assign frozen_dm = value

```python
frozen_dm = freeze_dims_and_data(m)['dm']
```

### Step 5: Assign frozen_dm_draws = pm.draw(...)

```python
frozen_dm_draws = pm.draw(frozen_dm, mode=mode, random_seed=36)
```

### Step 6: Call np.testing.assert_equal()

```python
np.testing.assert_equal(frozen_dm_draws, np.eye(3) * 5)
```

### Step 7: Assign dm = DirichletMultinomial(...)

```python
dm = DirichletMultinomial('dm', n=5, a=np.eye(3) * 1000000.0 + 0.01, dims=('trial', 'item'))
```


## Complete Example

```python
# Setup
# Fixtures: mode

# Workflow
'Test we can draw from a DM with a shape defined by dims in the JAX backend,\n    after freezing those dims.\n    '
with pm.Model(coords={'trial': range(3), 'item': range(3)}) as m:
    dm = DirichletMultinomial('dm', n=5, a=np.eye(3) * 1000000.0 + 0.01, dims=('trial', 'item'))
dm_draws = pm.draw(dm, mode=mode, random_seed=36)
np.testing.assert_equal(dm_draws, np.eye(3) * 5)
frozen_dm = freeze_dims_and_data(m)['dm']
frozen_dm_draws = pm.draw(frozen_dm, mode=mode, random_seed=36)
np.testing.assert_equal(frozen_dm_draws, np.eye(3) * 5)
```

## Next Steps


---

*Source: test_random_alternative_backends.py:38 | Complexity: Intermediate | Last updated: 2026-05-18*