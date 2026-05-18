# How To: Var Replacement

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test var replacement

## Prerequisites

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


## Step-by-Step Guide

### Step 1: Assign X_mean = floatX(...)

```python
X_mean = floatX(np.linspace(0, 10, 10))
```

**Verification:**
```python
assert advi.sample_node(mean).eval().shape == (10,)
```

### Step 2: Assign y = floatX(...)

```python
y = floatX(np.random.normal(X_mean * 4, 0.05))
```

**Verification:**
```python
assert advi.sample_node(mean, more_replacements={inp: x_new}).eval().shape == (11,)
```

### Step 3: Assign inp_size = pytensor.shared(...)

```python
inp_size = pytensor.shared(np.array(10, dtype='int64'), name='inp_size')
```

### Step 4: Assign inp = pm.Normal(...)

```python
inp = pm.Normal('X', X_mean, size=(inp_size,))
```

### Step 5: Assign coef = pm.Normal(...)

```python
coef = pm.Normal('b', 4.0)
```

### Step 6: Assign mean = value

```python
mean = inp * coef
```

### Step 7: Call pm.Normal()

```python
pm.Normal('y', mean, 0.1, shape=inp.shape, observed=y)
```

### Step 8: Assign advi = pm.fit(...)

```python
advi = pm.fit(100)
```

**Verification:**
```python
assert advi.sample_node(mean).eval().shape == (10,)
```

### Step 9: Call inp_size.set_value()

```python
inp_size.set_value(11)
```

### Step 10: Assign x_new = floatX(...)

```python
x_new = floatX(np.linspace(0, 10, 11))
```

**Verification:**
```python
assert advi.sample_node(mean, more_replacements={inp: x_new}).eval().shape == (11,)
```


## Complete Example

```python
# Workflow
X_mean = floatX(np.linspace(0, 10, 10))
y = floatX(np.random.normal(X_mean * 4, 0.05))
inp_size = pytensor.shared(np.array(10, dtype='int64'), name='inp_size')
with pm.Model():
    inp = pm.Normal('X', X_mean, size=(inp_size,))
    coef = pm.Normal('b', 4.0)
    mean = inp * coef
    pm.Normal('y', mean, 0.1, shape=inp.shape, observed=y)
    advi = pm.fit(100)
    assert advi.sample_node(mean).eval().shape == (10,)
    inp_size.set_value(11)
    x_new = floatX(np.linspace(0, 10, 11))
    assert advi.sample_node(mean, more_replacements={inp: x_new}).eval().shape == (11,)
```

## Next Steps


---

*Source: test_inference.py:339 | Complexity: Advanced | Last updated: 2026-05-18*