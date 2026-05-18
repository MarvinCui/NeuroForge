# How To: Full Adapt Adaptation Window

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test full adapt adaptation window

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.sparse`
- `pymc`
- `pymc.pytensorf`
- `pymc.step_methods.hmc`

**Setup Required:**
```python
# Fixtures: seed
```

## Step-by-Step Guide

### Step 1: Call np.random.seed()

```python
np.random.seed(seed)
```

**Verification:**
```python
assert pot._previous_update == window
```

### Step 2: Assign window = 10

```python
window = 10
```

**Verification:**
```python
assert pot.adaptation_window == window * pot.adaptation_window_multiplier
```

### Step 3: Assign pot = quadpotential.QuadPotentialFullAdapt(...)

```python
pot = quadpotential.QuadPotentialFullAdapt(2, np.zeros(2), np.eye(2), 1, adaptation_window=window)
```

**Verification:**
```python
assert pot._previous_update == window
```

### Step 4: Call pot.update()

```python
pot.update(np.random.randn(2), None, True)
```

**Verification:**
```python
assert pot.adaptation_window == window * pot.adaptation_window_multiplier
```

### Step 5: Assign pot = quadpotential.QuadPotentialFullAdapt(...)

```python
pot = quadpotential.QuadPotentialFullAdapt(2, np.zeros(2), np.eye(2), 1, adaptation_window=window)
```

### Step 6: Call pot.update()

```python
pot.update(np.random.randn(2), None, True)
```


## Complete Example

```python
# Setup
# Fixtures: seed

# Workflow
np.random.seed(seed)
window = 10
with pytest.warns(UserWarning, match='experimental feature'):
    pot = quadpotential.QuadPotentialFullAdapt(2, np.zeros(2), np.eye(2), 1, adaptation_window=window)
for i in range(window + 1):
    pot.update(np.random.randn(2), None, True)
assert pot._previous_update == window
assert pot.adaptation_window == window * pot.adaptation_window_multiplier
with pytest.warns(UserWarning, match='experimental feature'):
    pot = quadpotential.QuadPotentialFullAdapt(2, np.zeros(2), np.eye(2), 1, adaptation_window=window)
for i in range(window + 1):
    pot.update(np.random.randn(2), None, True)
assert pot._previous_update == window
assert pot.adaptation_window == window * pot.adaptation_window_multiplier
```

## Next Steps


---

*Source: test_quadpotential.py:236 | Complexity: Intermediate | Last updated: 2026-05-18*