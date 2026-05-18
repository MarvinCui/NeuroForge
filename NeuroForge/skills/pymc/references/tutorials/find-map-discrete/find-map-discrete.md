# How To: Find Map Discrete

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test find MAP discrete

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign tol1 = value

```python
tol1 = 2.0 ** (-11)
```

**Verification:**
```python
assert_allclose(map_est1['p'], 0.6086956533498806, atol=tol1, rtol=0)
```

### Step 2: Assign tol2 = value

```python
tol2 = 2.0 ** (-6)
```

**Verification:**
```python
assert_allclose(map_est2['p'], 0.695642178810167, atol=tol2, rtol=0)
```

### Step 3: Assign alpha = 4

```python
alpha = 4
```

**Verification:**
```python
assert map_est2['ss'] == 14
```

### Step 4: Assign beta = 4

```python
beta = 4
```

### Step 5: Assign n = 20

```python
n = 20
```

### Step 6: Assign yes = 15

```python
yes = 15
```

### Step 7: Call assert_allclose()

```python
assert_allclose(map_est1['p'], 0.6086956533498806, atol=tol1, rtol=0)
```

### Step 8: Call assert_allclose()

```python
assert_allclose(map_est2['p'], 0.695642178810167, atol=tol2, rtol=0)
```

**Verification:**
```python
assert map_est2['ss'] == 14
```

### Step 9: Assign p = pm.Beta(...)

```python
p = pm.Beta('p', alpha, beta)
```

### Step 10: Call pm.Binomial()

```python
pm.Binomial('ss', n=n, p=p)
```

### Step 11: Call pm.Binomial()

```python
pm.Binomial('s', n=n, p=p, observed=yes)
```

### Step 12: Assign map_est1 = find_MAP(...)

```python
map_est1 = find_MAP()
```

### Step 13: Assign map_est2 = find_MAP(...)

```python
map_est2 = find_MAP(vars=model.value_vars)
```


## Complete Example

```python
# Workflow
tol1 = 2.0 ** (-11)
tol2 = 2.0 ** (-6)
alpha = 4
beta = 4
n = 20
yes = 15
with pm.Model() as model:
    p = pm.Beta('p', alpha, beta)
    pm.Binomial('ss', n=n, p=p)
    pm.Binomial('s', n=n, p=p, observed=yes)
    map_est1 = find_MAP()
    map_est2 = find_MAP(vars=model.value_vars)
assert_allclose(map_est1['p'], 0.6086956533498806, atol=tol1, rtol=0)
assert_allclose(map_est2['p'], 0.695642178810167, atol=tol2, rtol=0)
assert map_est2['ss'] == 14
```

## Next Steps


---

*Source: test_starting.py:66 | Complexity: Advanced | Last updated: 2026-05-18*