# How To: Shared Data As Index

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Allow pm.Data to be used for index variables, i.e with integers as well as floats.
See https://github.com/pymc-devs/pymc/issues/3813

## Prerequisites

**Required Modules:**
- `io`
- `os`
- `numpy`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `pytensor`
- `pytensor.tensor.variable`
- `pymc`
- `pymc.data`
- `pymc.pytensorf`


## Step-by-Step Guide

### Step 1: '\n        Allow pm.Data to be used for index variables, i.e with integers as well as floats.\n        See https://github.com/pymc-devs/pymc/issues/3813\n        '

```python
'\n        Allow pm.Data to be used for index variables, i.e with integers as well as floats.\n        See https://github.com/pymc-devs/pymc/issues/3813\n        '
```

**Verification:**
```python
assert prior_trace.prior['alpha'].shape == (1, 1000, 3)
```

### Step 2: Assign new_index = np.array(...)

```python
new_index = np.array([0, 1, 2])
```

**Verification:**
```python
assert idata.posterior['alpha'].shape == (1, 1000, 3)
```

### Step 3: Assign new_y = value

```python
new_y = [5.0, 6.0, 9.0]
```

**Verification:**
```python
assert pp_trace.posterior_predictive['alpha'].shape == (1, 1000, 3)
```

### Step 4: Assign index = pm.Data(...)

```python
index = pm.Data('index', [2, 0, 1, 0, 2])
```

**Verification:**
```python
assert pp_trace.posterior_predictive['obs'].shape == (1, 1000, 3)
```

### Step 5: Assign y = pm.Data(...)

```python
y = pm.Data('y', [1.0, 2.0, 3.0, 2.0, 1.0])
```

### Step 6: Assign alpha = pm.Normal(...)

```python
alpha = pm.Normal('alpha', 0, 1.5, size=3)
```

### Step 7: Call pm.Normal()

```python
pm.Normal('obs', alpha[index], np.sqrt(0.01), observed=y)
```

### Step 8: Assign prior_trace = pm.sample_prior_predictive(...)

```python
prior_trace = pm.sample_prior_predictive(1000)
```

### Step 9: Assign idata = pm.sample(...)

```python
idata = pm.sample(1000, tune=1000, chains=1, compute_convergence_checks=False)
```

### Step 10: Call pm.set_data()

```python
pm.set_data(new_data={'index': new_index, 'y': new_y})
```

### Step 11: Assign pp_trace = pm.sample_posterior_predictive(...)

```python
pp_trace = pm.sample_posterior_predictive(idata, var_names=['alpha', 'obs'])
```


## Complete Example

```python
# Workflow
'\n        Allow pm.Data to be used for index variables, i.e with integers as well as floats.\n        See https://github.com/pymc-devs/pymc/issues/3813\n        '
with pm.Model() as model:
    index = pm.Data('index', [2, 0, 1, 0, 2])
    y = pm.Data('y', [1.0, 2.0, 3.0, 2.0, 1.0])
    alpha = pm.Normal('alpha', 0, 1.5, size=3)
    pm.Normal('obs', alpha[index], np.sqrt(0.01), observed=y)
    prior_trace = pm.sample_prior_predictive(1000)
    idata = pm.sample(1000, tune=1000, chains=1, compute_convergence_checks=False)
new_index = np.array([0, 1, 2])
new_y = [5.0, 6.0, 9.0]
with model:
    pm.set_data(new_data={'index': new_index, 'y': new_y})
    pp_trace = pm.sample_posterior_predictive(idata, var_names=['alpha', 'obs'])
assert prior_trace.prior['alpha'].shape == (1, 1000, 3)
assert idata.posterior['alpha'].shape == (1, 1000, 3)
assert pp_trace.posterior_predictive['alpha'].shape == (1, 1000, 3)
assert pp_trace.posterior_predictive['obs'].shape == (1, 1000, 3)
```

## Next Steps


---

*Source: test_data.py:153 | Complexity: Advanced | Last updated: 2026-05-18*