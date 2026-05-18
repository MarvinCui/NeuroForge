# How To: Fit With Nans

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test fit with nans

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `io`
- `operator`
- `warnings`
- `cloudpickle`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pymc`
- `pymc.variational.opvi`
- `pymc.model.transform.basic`
- `pymc.pytensorf`
- `pymc.variational.inference`
- `pymc.variational.opvi`
- `tests`

**Setup Required:**
```python
# Fixtures: score
```

## Step-by-Step Guide

### Step 1: Assign X_mean = floatX(...)

```python
X_mean = floatX(np.linspace(0, 10, 10))
```

### Step 2: Assign y = floatX(...)

```python
y = floatX(np.random.normal(X_mean * 4, 0.05))
```

### Step 3: Assign inp = pm.Normal(...)

```python
inp = pm.Normal('X', X_mean, size=X_mean.shape)
```

### Step 4: Assign coef = pm.Normal(...)

```python
coef = pm.Normal('b', 4.0)
```

### Step 5: Assign mean = value

```python
mean = inp * coef
```

### Step 6: Call pm.Normal()

```python
pm.Normal('y', mean, 0.1, observed=y)
```

### Step 7: Assign advi = pm.fit(...)

```python
advi = pm.fit(100, score=score, obj_optimizer=pm.adam(learning_rate=float('nan')))
```


## Complete Example

```python
# Setup
# Fixtures: score

# Workflow
X_mean = floatX(np.linspace(0, 10, 10))
y = floatX(np.random.normal(X_mean * 4, 0.05))
with pm.Model():
    inp = pm.Normal('X', X_mean, size=X_mean.shape)
    coef = pm.Normal('b', 4.0)
    mean = inp * coef
    pm.Normal('y', mean, 0.1, observed=y)
    with pytest.raises(FloatingPointError) as e:
        advi = pm.fit(100, score=score, obj_optimizer=pm.adam(learning_rate=float('nan')))
```

## Next Steps


---

*Source: test_inference.py:38 | Complexity: Intermediate | Last updated: 2026-05-18*