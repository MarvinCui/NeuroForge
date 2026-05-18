# How To: Map Effects

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test ANOVA effects parsing.

## Prerequisites

**Required Modules:**
- `functools`
- `itertools`
- `numpy`
- `pytest`
- `scipy.stats`
- `numpy.testing`
- `mne`
- `mne.stats.parametric`


## Step-by-Step Guide

### Step 1: 'Test ANOVA effects parsing.'

```python
'Test ANOVA effects parsing.'
```

**Verification:**
```python
assert names == ['A']
```

### Step 2: Assign unknown = _map_effects(...)

```python
selection, names = _map_effects(n_factors=2, effects='A')
```

**Verification:**
```python
assert names == ['A', 'A:B']
```

### Step 3: Assign unknown = _map_effects(...)

```python
selection, names = _map_effects(n_factors=2, effects=['A', 'A:B'])
```

**Verification:**
```python
assert names == ['A', 'B', 'A:B']
```

### Step 4: Assign unknown = _map_effects(...)

```python
selection, names = _map_effects(n_factors=3, effects='A*B')
```

**Verification:**
```python
assert names == ['A', 'B', 'A:B', 'C', 'A:C']
```

### Step 5: Assign unknown = _map_effects(...)

```python
selection, names = _map_effects(n_factors=3, effects='A*C')
```

**Verification:**
```python
assert names == ['A', 'B', 'A:B', 'C', 'A:C']
```

### Step 6: Call pytest.raises()

```python
pytest.raises(ValueError, _map_effects, n_factors=2, effects='C')
```

### Step 7: Call pytest.raises()

```python
pytest.raises(ValueError, _map_effects, n_factors=27, effects='all')
```


## Complete Example

```python
# Workflow
'Test ANOVA effects parsing.'
selection, names = _map_effects(n_factors=2, effects='A')
assert names == ['A']
selection, names = _map_effects(n_factors=2, effects=['A', 'A:B'])
assert names == ['A', 'A:B']
selection, names = _map_effects(n_factors=3, effects='A*B')
assert names == ['A', 'B', 'A:B']
selection, names = _map_effects(n_factors=3, effects='A*C')
assert names == ['A', 'B', 'A:B', 'C', 'A:C']
pytest.raises(ValueError, _map_effects, n_factors=2, effects='C')
pytest.raises(ValueError, _map_effects, n_factors=27, effects='all')
```

## Next Steps


---

*Source: test_parametric.py:49 | Complexity: Intermediate | Last updated: 2026-05-18*