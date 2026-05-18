# How To: Metrics

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test simulation metrics.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.simulation`
- `mne.simulation.metrics`


## Step-by-Step Guide

### Step 1: 'Test simulation metrics.'

```python
'Test simulation metrics.'
```

**Verification:**
```python
assert E1_rms == 0.0
```

### Step 2: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(src_fname)
```

**Verification:**
```python
assert E2_rms == 0.0
```

### Step 3: Assign times = value

```python
times = np.arange(600) / 1000.0
```

**Verification:**
```python
assert_allclose(E1_cos, 0.0, atol=1e-08)
```

### Step 4: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(42)
```

**Verification:**
```python
assert_allclose(E2_cos, 0.0, atol=1e-08)
```

### Step 5: Assign stc1 = simulate_sparse_stc(...)

```python
stc1 = simulate_sparse_stc(src, n_dipoles=2, times=times, random_state=rng)
```

### Step 6: Assign stc2 = simulate_sparse_stc(...)

```python
stc2 = simulate_sparse_stc(src, n_dipoles=2, times=times, random_state=rng)
```

### Step 7: Assign E1_rms = source_estimate_quantification(...)

```python
E1_rms = source_estimate_quantification(stc1, stc1, metric='rms')
```

### Step 8: Assign E2_rms = source_estimate_quantification(...)

```python
E2_rms = source_estimate_quantification(stc2, stc2, metric='rms')
```

### Step 9: Assign E1_cos = source_estimate_quantification(...)

```python
E1_cos = source_estimate_quantification(stc1, stc1, metric='cosine')
```

### Step 10: Assign E2_cos = source_estimate_quantification(...)

```python
E2_cos = source_estimate_quantification(stc2, stc2, metric='cosine')
```

**Verification:**
```python
assert E1_rms == 0.0
```

### Step 11: Call assert_allclose()

```python
assert_allclose(E1_cos, 0.0, atol=1e-08)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(E2_cos, 0.0, atol=1e-08)
```

### Step 13: Assign stc_bad = stc2.copy.crop(...)

```python
stc_bad = stc2.copy().crop(0, 0.5)
```

### Step 14: Assign stc_bad = stc2.copy(...)

```python
stc_bad = stc2.copy()
```

### Step 15: Call source_estimate_quantification()

```python
source_estimate_quantification(stc1, stc_bad)
```

### Step 16: Call source_estimate_quantification()

```python
source_estimate_quantification(stc1, stc_bad)
```

### Step 17: Call source_estimate_quantification()

```python
source_estimate_quantification(stc1, stc2, metric='foo')
```


## Complete Example

```python
# Workflow
'Test simulation metrics.'
src = read_source_spaces(src_fname)
times = np.arange(600) / 1000.0
rng = np.random.RandomState(42)
stc1 = simulate_sparse_stc(src, n_dipoles=2, times=times, random_state=rng)
stc2 = simulate_sparse_stc(src, n_dipoles=2, times=times, random_state=rng)
E1_rms = source_estimate_quantification(stc1, stc1, metric='rms')
E2_rms = source_estimate_quantification(stc2, stc2, metric='rms')
E1_cos = source_estimate_quantification(stc1, stc1, metric='cosine')
E2_cos = source_estimate_quantification(stc2, stc2, metric='cosine')
assert E1_rms == 0.0
assert E2_rms == 0.0
assert_allclose(E1_cos, 0.0, atol=1e-08)
assert_allclose(E2_cos, 0.0, atol=1e-08)
stc_bad = stc2.copy().crop(0, 0.5)
with pytest.raises(ValueError, match='must have the same size'):
    source_estimate_quantification(stc1, stc_bad)
stc_bad = stc2.copy()
stc_bad.tmin -= 0.1
with pytest.raises(ValueError, match='Times.*must match'):
    source_estimate_quantification(stc1, stc_bad)
with pytest.raises(ValueError, match="Invalid value for the 'metric'"):
    source_estimate_quantification(stc1, stc2, metric='foo')
```

## Next Steps


---

*Source: test_metrics.py:19 | Complexity: Advanced | Last updated: 2026-05-18*