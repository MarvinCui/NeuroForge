# How To: Ctps

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test basic ctps functionality.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne.preprocessing.ctps_`
- `mne.time_frequency`


## Step-by-Step Guide

### Step 1: 'Test basic ctps functionality.'

```python
'Test basic ctps functionality.'
```

**Verification:**
```python
assert_array_equal(a, b)
```

### Step 2: Call assert_array_equal()

```python
assert_array_equal(_prob_kuiper(np.array([1.0, 1.0]), 400), _prob_kuiper(np.array([1.0, 1.0]), 400))
```

**Verification:**
```python
assert a.min() >= 0
```

### Step 3: Assign data = get_data(...)

```python
data = get_data(n_trials, j_extent)
```

**Verification:**
```python
assert a.max() <= 1
```

### Step 4: Assign unknown = ctps(...)

```python
ks_dyn, pk_dyn, phase_trial = ctps(data)
```

**Verification:**
```python
assert b.min() >= 0
```

### Step 5: Assign data2 = _compute_normalized_phase(...)

```python
data2 = _compute_normalized_phase(data)
```

**Verification:**
```python
assert b.max() <= 1
```

### Step 6: Assign unknown = ctps(...)

```python
ks_dyn2, pk_dyn2, _ = ctps(data2, is_raw=False)
```

**Verification:**
```python
assert pk_dyn.min() > 0.0 or pk_dyn.max() < 1.0
```

### Step 7: Call assert_array_equal()

```python
assert_array_equal(a, b)
```

**Verification:**
```python
assert phase_trial.shape == data.shape
```

### Step 8: Call pytest.raises()

```python
pytest.raises(ValueError, ctps, data[:, :, :, None])
```

**Verification:**
```python
assert pk_dyn.shape == data.shape[1:]
```


## Complete Example

```python
# Workflow
'Test basic ctps functionality.'
for ii, (n_trials, j_extent, pk_max) in iter_test_ctps:
    data = get_data(n_trials, j_extent)
    ks_dyn, pk_dyn, phase_trial = ctps(data)
    data2 = _compute_normalized_phase(data)
    ks_dyn2, pk_dyn2, _ = ctps(data2, is_raw=False)
    for a, b in zip([ks_dyn, pk_dyn, phase_trial], [ks_dyn2, pk_dyn2, data2]):
        assert_array_equal(a, b)
        assert a.min() >= 0
        assert a.max() <= 1
        assert b.min() >= 0
        assert b.max() <= 1
    assert pk_dyn.min() > 0.0 or pk_dyn.max() < 1.0
    assert phase_trial.shape == data.shape
    assert pk_dyn.shape == data.shape[1:]
    assert pk_dyn[0].max() == 1.0
    assert len(np.unique(pk_dyn[0])) == 1.0
    assert pk_dyn[1].max() < pk_max
    assert pk_dyn[2].max() > 0.3
    if ii < 1:
        pytest.raises(ValueError, ctps, data[:, :, :, None])
assert _prob_kuiper(1.0, 400) == 1.0
assert_array_equal(_prob_kuiper(np.array([1.0, 1.0]), 400), _prob_kuiper(np.array([1.0, 1.0]), 400))
assert _prob_kuiper(0.1, 400) < 0.1
```

## Next Steps


---

*Source: test_ctps.py:56 | Complexity: Advanced | Last updated: 2026-05-18*