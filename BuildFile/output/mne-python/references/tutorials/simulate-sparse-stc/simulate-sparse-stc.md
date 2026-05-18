# How To: Simulate Sparse Stc

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test generation of sparse source estimate.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.label`
- `mne.simulation`

**Setup Required:**
```python
# Fixtures: _get_fwd_labels
```

## Step-by-Step Guide

### Step 1: 'Test generation of sparse source estimate.'

```python
'Test generation of sparse source estimate.'
```

**Verification:**
```python
assert_equal(stc_1.subject, 'sample')
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert stc_1.data.shape[0] == len(mylabels)
```

### Step 3: Assign unknown = _get_fwd_labels

```python
fwd, labels = _get_fwd_labels
```

**Verification:**
```python
assert stc_1.data.shape[1] == n_times
```

### Step 4: Assign n_times = 10

```python
n_times = 10
```

**Verification:**
```python
assert_array_equal(stc_1.lh_vertno, stc_2.lh_vertno)
```

### Step 5: Assign tmin = 0

```python
tmin = 0
```

**Verification:**
```python
assert_array_equal(stc_1.rh_vertno, stc_2.rh_vertno)
```

### Step 6: Assign tstep = 0.001

```python
tstep = 0.001
```

### Step 7: Assign times = value

```python
times = np.arange(n_times, dtype=np.float64) * tstep + tmin
```

### Step 8: Call pytest.raises()

```python
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(labels), times, labels=labels, location='center', subject='sample', subjects_dir=subjects_dir)
```

### Step 9: Assign mylabels = value

```python
mylabels = []
```

### Step 10: Call pytest.raises()

```python
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(mylabels), times, labels=mylabels, location='center', subject='foo', subjects_dir=subjects_dir)
```

### Step 11: Call pytest.raises()

```python
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(mylabels), times, labels=mylabels, location='center', subjects_dir=subjects_dir)
```

### Step 12: Assign unknown = 'sample'

```python
fwd['src'][0]['subject_his_id'] = 'sample'
```

### Step 13: Call pytest.raises()

```python
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(mylabels), times, labels=mylabels, location='foo')
```

### Step 14: Assign err_str = 'Number of labels'

```python
err_str = 'Number of labels'
```

### Step 15: Assign this_label = label.copy(...)

```python
this_label = label.copy()
```

### Step 16: Call this_label.values.fill()

```python
this_label.values.fill(1.0)
```

### Step 17: Call mylabels.append()

```python
mylabels.append(this_label)
```

### Step 18: Assign random_state = value

```python
random_state = 0 if location == 'random' else None
```

### Step 19: Assign stc_1 = simulate_sparse_stc(...)

```python
stc_1 = simulate_sparse_stc(fwd['src'], len(mylabels), times, labels=mylabels, random_state=random_state, location=location, subjects_dir=subjects_dir)
```

### Step 20: Call assert_equal()

```python
assert_equal(stc_1.subject, 'sample')
```

**Verification:**
```python
assert stc_1.data.shape[0] == len(mylabels)
```

### Step 21: Assign stc_2 = simulate_sparse_stc(...)

```python
stc_2 = simulate_sparse_stc(fwd['src'], len(mylabels), times, labels=mylabels, random_state=random_state, location=location, subjects_dir=subjects_dir)
```

### Step 22: Call assert_array_equal()

```python
assert_array_equal(stc_1.lh_vertno, stc_2.lh_vertno)
```

### Step 23: Call assert_array_equal()

```python
assert_array_equal(stc_1.rh_vertno, stc_2.rh_vertno)
```

### Step 24: Call simulate_sparse_stc()

```python
simulate_sparse_stc(fwd['src'], len(mylabels) + 1, times, labels=mylabels, random_state=random_state, location=location, subjects_dir=subjects_dir)
```


## Complete Example

```python
# Setup
# Fixtures: _get_fwd_labels

# Workflow
'Test generation of sparse source estimate.'
pytest.importorskip('nibabel')
fwd, labels = _get_fwd_labels
n_times = 10
tmin = 0
tstep = 0.001
times = np.arange(n_times, dtype=np.float64) * tstep + tmin
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(labels), times, labels=labels, location='center', subject='sample', subjects_dir=subjects_dir)
mylabels = []
for label in labels:
    this_label = label.copy()
    this_label.values.fill(1.0)
    mylabels.append(this_label)
for location in ('random', 'center'):
    random_state = 0 if location == 'random' else None
    stc_1 = simulate_sparse_stc(fwd['src'], len(mylabels), times, labels=mylabels, random_state=random_state, location=location, subjects_dir=subjects_dir)
    assert_equal(stc_1.subject, 'sample')
    assert stc_1.data.shape[0] == len(mylabels)
    assert stc_1.data.shape[1] == n_times
    stc_2 = simulate_sparse_stc(fwd['src'], len(mylabels), times, labels=mylabels, random_state=random_state, location=location, subjects_dir=subjects_dir)
    assert_array_equal(stc_1.lh_vertno, stc_2.lh_vertno)
    assert_array_equal(stc_1.rh_vertno, stc_2.rh_vertno)
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(mylabels), times, labels=mylabels, location='center', subject='foo', subjects_dir=subjects_dir)
del fwd['src'][0]['subject_his_id']
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(mylabels), times, labels=mylabels, location='center', subjects_dir=subjects_dir)
fwd['src'][0]['subject_his_id'] = 'sample'
pytest.raises(ValueError, simulate_sparse_stc, fwd['src'], len(mylabels), times, labels=mylabels, location='foo')
err_str = 'Number of labels'
with pytest.raises(ValueError, match=err_str):
    simulate_sparse_stc(fwd['src'], len(mylabels) + 1, times, labels=mylabels, random_state=random_state, location=location, subjects_dir=subjects_dir)
```

## Next Steps


---

*Source: test_source.py:124 | Complexity: Advanced | Last updated: 2026-05-18*