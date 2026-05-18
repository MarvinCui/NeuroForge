# How To: Keep Warning Stat Setting

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: The ``keep_warning_stat`` stat (aka "Adrian's kwarg) enables users
to keep the ``SamplerWarning`` objects from the ``sample_stats.warning`` group.
This breaks ``idata.to_netcdf()`` which is why it defaults to ``False``.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `unittest.mock`
- `warnings`
- `contextlib`
- `numpy`
- `numpy.testing`
- `pytensor`
- `pytensor.tensor`
- `pytest`
- `scipy.special`
- `pytensor`
- `pytensor.compile.ops`
- `xarray`
- `pymc`
- `pymc.backends.ndarray`
- `pymc.distributions`
- `pymc.exceptions`
- `pymc.sampling.mcmc`
- `pymc.stats.convergence`
- `pymc.step_methods`
- `pymc.testing`
- `tests.models`

**Setup Required:**
```python
# Fixtures: keep_warning_stat
```

## Step-by-Step Guide

### Step 1: 'The ``keep_warning_stat`` stat (aka "Adrian\'s kwarg) enables users\n        to keep the ``SamplerWarning`` objects from the ``sample_stats.warning`` group.\n        This breaks ``idata.to_netcdf()`` which is why it defaults to ``False``.\n        '

```python
'The ``keep_warning_stat`` stat (aka "Adrian\'s kwarg) enables users\n        to keep the ``SamplerWarning`` objects from the ``sample_stats.warning`` group.\n        This breaks ``idata.to_netcdf()`` which is why it defaults to ``False``.\n        '
```

**Verification:**
```python
assert 'warning' in idata.warmup_sample_stats
```

### Step 2: Assign sample_kwargs = value

```python
sample_kwargs = {'tune': 2, 'draws': 3, 'chains': 1, 'compute_convergence_checks': False, 'discard_tuned_samples': False, 'keep_warning_stat': keep_warning_stat}
```

**Verification:**
```python
assert 'warning' in idata.sample_stats
```

### Step 3: Assign unknown = True

```python
sample_kwargs['keep_warning_stat'] = True
```

**Verification:**
```python
assert 'warning' in idata.sample_stats
```

### Step 4: Call pm.Normal()

```python
pm.Normal('n')
```

**Verification:**
```python
assert warn_objs
```

### Step 5: Assign idata = pm.sample(...)

```python
idata = pm.sample(step=ApocalypticMetropolis(), **sample_kwargs)
```

**Verification:**
```python
assert any((isinstance(w, SamplerWarning) for w in warn_objs))
```

### Step 6: Assign warn_objs = list(...)

```python
warn_objs = list(idata.sample_stats.warning.sel(chain=0).values.flatten())
```

**Verification:**
```python
assert any(('Asteroid' in w.message for w in warn_objs))
```

### Step 7: Assign warn_objs = value

```python
warn_objs = [a.tolist() for a in warn_objs]
```

**Verification:**
```python
assert 'warning' not in idata.warmup_sample_stats
```


## Complete Example

```python
# Setup
# Fixtures: keep_warning_stat

# Workflow
'The ``keep_warning_stat`` stat (aka "Adrian\'s kwarg) enables users\n        to keep the ``SamplerWarning`` objects from the ``sample_stats.warning`` group.\n        This breaks ``idata.to_netcdf()`` which is why it defaults to ``False``.\n        '
sample_kwargs = {'tune': 2, 'draws': 3, 'chains': 1, 'compute_convergence_checks': False, 'discard_tuned_samples': False, 'keep_warning_stat': keep_warning_stat}
if keep_warning_stat:
    sample_kwargs['keep_warning_stat'] = True
with pm.Model():
    pm.Normal('n')
    idata = pm.sample(step=ApocalypticMetropolis(), **sample_kwargs)
if keep_warning_stat:
    assert 'warning' in idata.warmup_sample_stats
    assert 'warning' in idata.sample_stats
    assert 'warning' in idata.sample_stats
    warn_objs = list(idata.sample_stats.warning.sel(chain=0).values.flatten())
    assert warn_objs
    if isinstance(warn_objs[0], np.ndarray):
        warn_objs = [a.tolist() for a in warn_objs]
    assert any((isinstance(w, SamplerWarning) for w in warn_objs))
    assert any(('Asteroid' in w.message for w in warn_objs))
else:
    assert 'warning' not in idata.warmup_sample_stats
    assert 'warning' not in idata.sample_stats
    assert 'warning_dim_0' not in idata.warmup_sample_stats
    assert 'warning_dim_0' not in idata.sample_stats
```

## Next Steps


---

*Source: test_mcmc.py:480 | Complexity: Intermediate | Last updated: 2026-05-18*