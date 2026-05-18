# How To: Simulate Sparse Stc Single Hemi

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
assert stc_1.data.shape[0] == len(labels_single_hemi)
```

### Step 2: Assign unknown = _get_fwd_labels

```python
fwd, labels = _get_fwd_labels
```

**Verification:**
```python
assert stc_1.data.shape[1] == n_times
```

### Step 3: Assign labels_single_hemi = value

```python
labels_single_hemi = labels[1:]
```

**Verification:**
```python
assert_array_equal(stc_1.lh_vertno, stc_2.lh_vertno)
```

### Step 4: Assign n_times = 10

```python
n_times = 10
```

**Verification:**
```python
assert_array_equal(stc_1.rh_vertno, stc_2.rh_vertno)
```

### Step 5: Assign tmin = 0

```python
tmin = 0
```

### Step 6: Assign tstep = 0.001

```python
tstep = 0.001
```

### Step 7: Assign times = value

```python
times = np.arange(n_times, dtype=np.float64) * tstep + tmin
```

### Step 8: Assign stc_1 = simulate_sparse_stc(...)

```python
stc_1 = simulate_sparse_stc(fwd['src'], len(labels_single_hemi), times, labels=labels_single_hemi, random_state=0)
```

**Verification:**
```python
assert stc_1.data.shape[0] == len(labels_single_hemi)
```

### Step 9: Assign stc_2 = simulate_sparse_stc(...)

```python
stc_2 = simulate_sparse_stc(fwd['src'], len(labels_single_hemi), times, labels=labels_single_hemi, random_state=0)
```

### Step 10: Call assert_array_equal()

```python
assert_array_equal(stc_1.lh_vertno, stc_2.lh_vertno)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(stc_1.rh_vertno, stc_2.rh_vertno)
```


## Complete Example

```python
# Setup
# Fixtures: _get_fwd_labels

# Workflow
'Test generation of sparse source estimate.'
fwd, labels = _get_fwd_labels
labels_single_hemi = labels[1:]
n_times = 10
tmin = 0
tstep = 0.001
times = np.arange(n_times, dtype=np.float64) * tstep + tmin
stc_1 = simulate_sparse_stc(fwd['src'], len(labels_single_hemi), times, labels=labels_single_hemi, random_state=0)
assert stc_1.data.shape[0] == len(labels_single_hemi)
assert stc_1.data.shape[1] == n_times
stc_2 = simulate_sparse_stc(fwd['src'], len(labels_single_hemi), times, labels=labels_single_hemi, random_state=0)
assert_array_equal(stc_1.lh_vertno, stc_2.lh_vertno)
assert_array_equal(stc_1.rh_vertno, stc_2.rh_vertno)
```

## Next Steps


---

*Source: test_source.py:279 | Complexity: Advanced | Last updated: 2026-05-18*