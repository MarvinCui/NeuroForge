# How To: Prox L1 Nonexpansiveness

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test prox l1 nonexpansiveness

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `numpy`
- `pytest`
- `numpy.testing`
- `nilearn.decoding._proximal_operators`

**Setup Required:**
```python
# Fixtures: rng, n_features
```

## Step-by-Step Guide

### Step 1: Assign x = rng.standard_normal(...)

```python
x = rng.standard_normal((n_features, 1))
```

**Verification:**
```python
assert (sa - sb) ** 2 <= (a - b) ** 2 - (pa - pb) ** 2
```

### Step 2: Assign tau = 0.3

```python
tau = 0.3
```

### Step 3: Assign s = prox_l1(...)

```python
s = prox_l1(x.copy(), tau)
```

### Step 4: Assign p = value

```python
p = x - s
```

**Verification:**
```python
assert (sa - sb) ** 2 <= (a - b) ** 2 - (pa - pb) ** 2
```


## Complete Example

```python
# Setup
# Fixtures: rng, n_features

# Workflow
x = rng.standard_normal((n_features, 1))
tau = 0.3
s = prox_l1(x.copy(), tau)
p = x - s
for (a, b), (pa, pb), (sa, sb) in zip(*[itertools.product(z[0], z[0]) for z in [x, p, s]], strict=False):
    assert (sa - sb) ** 2 <= (a - b) ** 2 - (pa - pb) ** 2
```

## Next Steps


---

*Source: test_operators.py:10 | Complexity: Intermediate | Last updated: 2026-05-18*