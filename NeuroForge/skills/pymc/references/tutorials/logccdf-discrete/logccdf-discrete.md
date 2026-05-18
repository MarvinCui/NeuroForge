# How To: Logccdf Discrete

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test logccdf discrete

## Prerequisites

**Required Modules:**
- `re`
- `numpy`
- `pytensor.tensor`
- `pytest`
- `scipy.stats.distributions`
- `pytensor.scalar`
- `pymc`
- `pymc.logprob.abstract`
- `pymc.logprob.basic`
- `pytensor.graph.traversal`
- `pytensor.scalar.math`
- `pytensor.tensor.elemwise`


## Step-by-Step Guide

### Step 1: Assign mu = 3.0

```python
mu = 3.0
```

### Step 2: Assign x = pm.Poisson.dist(...)

```python
x = pm.Poisson.dist(mu=mu)
```

### Step 3: Assign test_values = np.array(...)

```python
test_values = np.array([0, 1, 2, 3, 5, 10])
```

### Step 4: Assign result = logccdf.eval(...)

```python
result = logccdf(x, test_values).eval()
```

### Step 5: Assign expected = sp.poisson.logsf(...)

```python
expected = sp.poisson(mu).logsf(test_values)
```

### Step 6: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(result, expected, rtol=1e-06)
```


## Complete Example

```python
# Workflow
mu = 3.0
x = pm.Poisson.dist(mu=mu)
test_values = np.array([0, 1, 2, 3, 5, 10])
result = logccdf(x, test_values).eval()
expected = sp.poisson(mu).logsf(test_values)
np.testing.assert_allclose(result, expected, rtol=1e-06)
```

## Next Steps


---

*Source: test_abstract.py:153 | Complexity: Intermediate | Last updated: 2026-05-18*