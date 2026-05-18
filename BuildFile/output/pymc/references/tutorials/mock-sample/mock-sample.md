# How To: Mock Sample

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, mock, workflow, integration

## Overview

Workflow: test mock sample

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `contextlib`
- `numpy`
- `pytest`
- `pymc`
- `pymc.testing`
- `tests.models`

**Setup Required:**
```python
# Fixtures: args, kwargs, expected_size, sample_stats
```

## Step-by-Step Guide

### Step 1: Assign unknown = expected_size

```python
expected_chains, expected_draws = expected_size
```

**Verification:**
```python
assert 'posterior' in idata
```

### Step 2: Assign unknown = simple_normal(...)

```python
_, model, _ = simple_normal(bounded_prior=True)
```

**Verification:**
```python
assert 'observed_data' in idata
```

### Step 3: Assign expected_sizes = value

```python
expected_sizes = {'chain': expected_chains, 'draw': expected_draws}
```

**Verification:**
```python
assert 'prior' not in idata
```

### Step 4: Assign idata = mock_sample(...)

```python
idata = mock_sample(*args, **kwargs, sample_stats=sample_stats)
```

**Verification:**
```python
assert 'posterior_predictive' not in idata
```

### Step 5: Assign sample_stats_ds = value

```python
sample_stats_ds = idata['sample_stats']
```

**Verification:**
```python
assert sample_stats_ds[name].sizes == expected_sizes
```


## Complete Example

```python
# Setup
# Fixtures: args, kwargs, expected_size, sample_stats

# Workflow
expected_chains, expected_draws = expected_size
_, model, _ = simple_normal(bounded_prior=True)
with model:
    idata = mock_sample(*args, **kwargs, sample_stats=sample_stats)
assert 'posterior' in idata
assert 'observed_data' in idata
assert 'prior' not in idata
assert 'posterior_predictive' not in idata
expected_sizes = {'chain': expected_chains, 'draw': expected_draws}
if sample_stats:
    sample_stats_ds = idata['sample_stats']
    for name in sample_stats.keys():
        assert sample_stats_ds[name].sizes == expected_sizes
else:
    assert 'sample_stats' not in idata
assert idata.posterior.sizes == expected_sizes
```

## Next Steps


---

*Source: test_testing.py:60 | Complexity: Intermediate | Last updated: 2026-05-18*