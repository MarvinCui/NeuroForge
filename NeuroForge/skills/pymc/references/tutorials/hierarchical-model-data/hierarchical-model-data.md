# How To: Hierarchical Model Data

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: hierarchical model data

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

### Step 1: Assign group_coords = value

```python
group_coords = {'group_d1': np.arange(3), 'group_d2': np.arange(7)}
```

### Step 2: Assign group_shape = tuple(...)

```python
group_shape = tuple((len(d) for d in group_coords.values()))
```

### Step 3: Assign data_coords = value

```python
data_coords = {'data_d': np.arange(11), **group_coords}
```

### Step 4: Assign data_shape = tuple(...)

```python
data_shape = tuple((len(d) for d in data_coords.values()))
```

### Step 5: Assign mu = value

```python
mu = -5.0
```

### Step 6: Assign sigma_group_mu = 3

```python
sigma_group_mu = 3
```

### Step 7: Assign group_mu = value

```python
group_mu = sigma_group_mu * np.random.randn(*group_shape)
```

### Step 8: Assign sigma = 3.0

```python
sigma = 3.0
```

### Step 9: Assign data = value

```python
data = sigma * np.random.randn(*data_shape) + group_mu + mu
```


## Complete Example

```python
# Workflow
group_coords = {'group_d1': np.arange(3), 'group_d2': np.arange(7)}
group_shape = tuple((len(d) for d in group_coords.values()))
data_coords = {'data_d': np.arange(11), **group_coords}
data_shape = tuple((len(d) for d in data_coords.values()))
mu = -5.0
sigma_group_mu = 3
group_mu = sigma_group_mu * np.random.randn(*group_shape)
sigma = 3.0
data = sigma * np.random.randn(*data_shape) + group_mu + mu
return {'group_coords': group_coords, 'group_shape': group_shape, 'data_coords': data_coords, 'data_shape': data_shape, 'mu': mu, 'sigma_group_mu': sigma_group_mu, 'sigma': sigma, 'group_mu': group_mu, 'data': data}
```

## Next Steps


---

*Source: test_inference.py:383 | Complexity: Advanced | Last updated: 2026-05-18*