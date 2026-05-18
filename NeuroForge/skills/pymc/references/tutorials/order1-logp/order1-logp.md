# How To: Order1 Logp

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test order1 logp

## Prerequisites

**Required Modules:**
- `numpy`
- `pytensor`
- `pytest`
- `scipy.stats`
- `pytensor.tensor.random.op`
- `pymc`
- `pymc`
- `pymc.distributions.continuous`
- `pymc.distributions.distribution`
- `pymc.distributions.multivariate`
- `pymc.distributions.shape_utils`
- `pymc.distributions.timeseries`
- `pymc.logprob.basic`
- `pymc.model`
- `pymc.pytensorf`
- `pymc.sampling.forward`
- `pymc.sampling.mcmc`
- `pymc.testing`


## Step-by-Step Guide

### Step 1: Assign data = np.array(...)

```python
data = np.array([0.3, 1, 2, 3, 4])
```

### Step 2: Assign phi = np.array(...)

```python
phi = np.array([0.99])
```

### Step 3: Assign test_dict = value

```python
test_dict = {'y': data, 'z': data[1:]}
```

### Step 4: Assign ar_like = t.compile_logp(...)

```python
ar_like = t.compile_logp(y)(test_dict)
```

### Step 5: Assign reg_like = t.compile_logp(...)

```python
reg_like = t.compile_logp(z)(test_dict)
```

### Step 6: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(ar_like, reg_like)
```

### Step 7: Assign ar_like = t_constant.compile_logp(...)

```python
ar_like = t_constant.compile_logp(y)(test_dict)
```

### Step 8: Assign reg_like = t_constant.compile_logp(...)

```python
reg_like = t_constant.compile_logp(z)(test_dict)
```

### Step 9: Call np.testing.assert_allclose()

```python
np.testing.assert_allclose(ar_like, reg_like)
```

### Step 10: Assign y = AR(...)

```python
y = AR('y', phi, sigma=1, init_dist=Flat.dist(), shape=len(data))
```

### Step 11: Assign z = Normal(...)

```python
z = Normal('z', mu=phi * data[:-1], sigma=1, shape=len(data) - 1)
```

### Step 12: Assign y = AR(...)

```python
y = AR('y', np.hstack((0.3, phi)), sigma=1, init_dist=Flat.dist(), shape=len(data), constant=True)
```

### Step 13: Assign z = Normal(...)

```python
z = Normal('z', mu=0.3 + phi * data[:-1], sigma=1, shape=len(data) - 1)
```


## Complete Example

```python
# Workflow
data = np.array([0.3, 1, 2, 3, 4])
phi = np.array([0.99])
with Model() as t:
    y = AR('y', phi, sigma=1, init_dist=Flat.dist(), shape=len(data))
    z = Normal('z', mu=phi * data[:-1], sigma=1, shape=len(data) - 1)
test_dict = {'y': data, 'z': data[1:]}
ar_like = t.compile_logp(y)(test_dict)
reg_like = t.compile_logp(z)(test_dict)
np.testing.assert_allclose(ar_like, reg_like)
with Model() as t_constant:
    y = AR('y', np.hstack((0.3, phi)), sigma=1, init_dist=Flat.dist(), shape=len(data), constant=True)
    z = Normal('z', mu=0.3 + phi * data[:-1], sigma=1, shape=len(data) - 1)
ar_like = t_constant.compile_logp(y)(test_dict)
reg_like = t_constant.compile_logp(z)(test_dict)
np.testing.assert_allclose(ar_like, reg_like)
```

## Next Steps


---

*Source: test_timeseries.py:468 | Complexity: Advanced | Last updated: 2026-05-18*