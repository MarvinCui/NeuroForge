# How To: External Nuts Sampler

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test external nuts sampler

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `unittest.mock`
- `warnings`
- `contextlib`
- `types`
- `numpy`
- `numpy.testing`
- `pytensor.tensor`
- `pytest`
- `xarray`
- `pymc`
- `pymc.exceptions`
- `pymc.progress_bar`
- `pymc.step_methods.hmc.quadpotential`

**Setup Required:**
```python
# Fixtures: nuts_sampler
```

## Step-by-Step Guide

### Step 1: Call np.testing.assert_array_equal()

```python
np.testing.assert_array_equal(idata1.posterior.x, idata2.posterior.x)
```

**Verification:**
```python
assert 'y' in idata1.constant_data
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip(nuts_sampler)
```

**Verification:**
```python
assert 'z' in idata1.constant_data
```

### Step 3: Assign x = Normal(...)

```python
x = Normal('x', 100, 5)
```

**Verification:**
```python
assert 'L' in idata1.observed_data
```

### Step 4: Assign y = Data(...)

```python
y = Data('y', [1, 2, 3, 4])
```

**Verification:**
```python
assert idata1.posterior.chain.size == 2
```

### Step 5: Call Data()

```python
Data('z', [100, 190, 310, 405])
```

**Verification:**
```python
assert idata1.posterior.draw.size == 500
```

### Step 6: Call Normal()

```python
Normal('L', mu=x, sigma=0.1, observed=y)
```

**Verification:**
```python
assert idata_reference.posterior.attrs.keys() == idata1.posterior.attrs.keys()
```

### Step 7: Assign kwargs = value

```python
kwargs = {'nuts_sampler': nuts_sampler, 'random_seed': 123, 'chains': 2, 'tune': 500, 'draws': 500, 'progressbar': False, 'initvals': {'x': 0.0}}
```

### Step 8: Assign idata1 = sample(...)

```python
idata1 = sample(**kwargs)
```

### Step 9: Assign idata2 = sample(...)

```python
idata2 = sample(**kwargs)
```

### Step 10: Assign reference_kwargs = kwargs.copy(...)

```python
reference_kwargs = kwargs.copy()
```

### Step 11: Assign unknown = 'pymc'

```python
reference_kwargs['nuts_sampler'] = 'pymc'
```

### Step 12: Assign idata_reference = sample(...)

```python
idata_reference = sample(**reference_kwargs)
```


## Complete Example

```python
# Setup
# Fixtures: nuts_sampler

# Workflow
if nuts_sampler != 'pymc':
    pytest.importorskip(nuts_sampler)
with Model():
    x = Normal('x', 100, 5)
    y = Data('y', [1, 2, 3, 4])
    Data('z', [100, 190, 310, 405])
    Normal('L', mu=x, sigma=0.1, observed=y)
    kwargs = {'nuts_sampler': nuts_sampler, 'random_seed': 123, 'chains': 2, 'tune': 500, 'draws': 500, 'progressbar': False, 'initvals': {'x': 0.0}}
    idata1 = sample(**kwargs)
    idata2 = sample(**kwargs)
    reference_kwargs = kwargs.copy()
    reference_kwargs['nuts_sampler'] = 'pymc'
    idata_reference = sample(**reference_kwargs)
assert 'y' in idata1.constant_data
assert 'z' in idata1.constant_data
assert 'L' in idata1.observed_data
assert idata1.posterior.chain.size == 2
assert idata1.posterior.draw.size == 500
np.testing.assert_array_equal(idata1.posterior.x, idata2.posterior.x)
assert idata_reference.posterior.attrs.keys() == idata1.posterior.attrs.keys()
```

## Next Steps


---

*Source: test_mcmc_external.py:50 | Complexity: Advanced | Last updated: 2026-05-18*