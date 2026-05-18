# How To: Multinomial Check Parameters

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multinomial check parameters

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `pytensor`
- `pytensor.tensor.random.basic`
- `scipy`
- `pymc`
- `pymc.distributions`
- `pymc.distributions.dist_math`
- `pymc.logprob.utils`
- `pymc.pytensorf`
- `tests.helpers`


## Step-by-Step Guide

### Step 1: Assign x = np.array(...)

```python
x = np.array([1, 5])
```

**Verification:**
```python
assert np.isclose(modelA.compile_logp()({'p_simplex__': [0]}), modelB.compile_logp()({'p_simplex__': [0]}))
```

### Step 2: Assign n = x.sum(...)

```python
n = x.sum()
```

**Verification:**
```python
assert np.isclose(modelA.compile_logp()({'p_simplex__': [0]}), modelB.compile_logp()({'p_simplex__': [0]}))
```

### Step 3: Assign p_a = pm.Dirichlet(...)

```python
p_a = pm.Dirichlet('p', floatX(np.ones(2)))
```

### Step 4: Call MultinomialA()

```python
MultinomialA('x', n, p_a, observed=x)
```

### Step 5: Assign p_b = pm.Dirichlet(...)

```python
p_b = pm.Dirichlet('p', floatX(np.ones(2)))
```

### Step 6: Call MultinomialB()

```python
MultinomialB('x', n, p_b, observed=x)
```


## Complete Example

```python
# Workflow
x = np.array([1, 5])
n = x.sum()
with pm.Model() as modelA:
    p_a = pm.Dirichlet('p', floatX(np.ones(2)))
    MultinomialA('x', n, p_a, observed=x)
with pm.Model() as modelB:
    p_b = pm.Dirichlet('p', floatX(np.ones(2)))
    MultinomialB('x', n, p_b, observed=x)
assert np.isclose(modelA.compile_logp()({'p_simplex__': [0]}), modelB.compile_logp()({'p_simplex__': [0]}))
```

## Next Steps


---

*Source: test_dist_math.py:104 | Complexity: Intermediate | Last updated: 2026-05-18*