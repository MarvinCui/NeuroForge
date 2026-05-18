# How To: Infer Steps

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test infer steps

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: init_dist, innovation_dist, shape, steps, steps_source
```

## Step-by-Step Guide

### Step 1: Assign shape_source_kwargs = value

```python
shape_source_kwargs = {'shape': None, 'dims': None, 'observed': None}
```

**Verification:**
```python
assert inferred_steps.eval().item() == steps
```

### Step 2: Assign coords = value

```python
coords = {f'dim{i}': range(s) for i, s in enumerate(shape)}
```

### Step 3: Assign inferred_steps = value

```python
inferred_steps = x.owner.inputs[-1]
```

**Verification:**
```python
assert inferred_steps.eval().item() == steps
```

### Step 4: Assign unknown = shape

```python
shape_source_kwargs['shape'] = shape
```

### Step 5: Assign x = RandomWalk(...)

```python
x = RandomWalk('x', init_dist=init_dist, innovation_dist=innovation_dist, **shape_source_kwargs)
```

### Step 6: Assign unknown = value

```python
shape_source_kwargs['dims'] = [f'dim{i}' for i in range(len(shape))]
```

### Step 7: Assign unknown = np.zeros(...)

```python
shape_source_kwargs['observed'] = np.zeros(shape)
```


## Complete Example

```python
# Setup
# Fixtures: init_dist, innovation_dist, shape, steps, steps_source

# Workflow
shape_source_kwargs = {'shape': None, 'dims': None, 'observed': None}
if steps_source == 'shape':
    shape_source_kwargs['shape'] = shape
elif steps_source == 'dims':
    shape_source_kwargs['dims'] = [f'dim{i}' for i in range(len(shape))]
elif steps_source == 'observed':
    shape_source_kwargs['observed'] = np.zeros(shape)
else:
    raise ValueError
coords = {f'dim{i}': range(s) for i, s in enumerate(shape)}
with Model(coords=coords):
    x = RandomWalk('x', init_dist=init_dist, innovation_dist=innovation_dist, **shape_source_kwargs)
inferred_steps = x.owner.inputs[-1]
assert inferred_steps.eval().item() == steps
```

## Next Steps


---

*Source: test_timeseries.py:238 | Complexity: Intermediate | Last updated: 2026-05-18*