# How To: Generate Stc Single Hemi

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test generation of source estimate, single hemi.

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

### Step 1: 'Test generation of source estimate, single hemi.'

```python
'Test generation of source estimate, single hemi.'
```

**Verification:**
```python
assert np.all(stc.data[idx] == 1.0)
```

### Step 2: Assign unknown = _get_fwd_labels

```python
fwd, labels = _get_fwd_labels
```

**Verification:**
```python
assert stc.data[idx].shape[1] == n_times
```

### Step 3: Assign labels_single_hemi = value

```python
labels_single_hemi = labels[1:]
```

**Verification:**
```python
assert_array_almost_equal(stc.data[idx], res)
```

### Step 4: Assign mylabels = value

```python
mylabels = []
```

### Step 5: Assign n_times = 10

```python
n_times = 10
```

### Step 6: Assign tmin = 0

```python
tmin = 0
```

### Step 7: Assign tstep = 0.001

```python
tstep = 0.001
```

### Step 8: Assign stc_data = np.ones(...)

```python
stc_data = np.ones((len(labels_single_hemi), n_times))
```

### Step 9: Assign stc = simulate_stc(...)

```python
stc = simulate_stc(fwd['src'], mylabels, stc_data, tmin, tstep)
```

### Step 10: Assign stc = simulate_stc(...)

```python
stc = simulate_stc(fwd['src'], mylabels, stc_data, tmin, tstep, fun)
```

### Step 11: Assign new_label = Label(...)

```python
new_label = Label(vertices=label.vertices, pos=label.pos, values=2 * i * np.ones(len(label.values)), hemi=label.hemi, comment=label.comment)
```

### Step 12: Call mylabels.append()

```python
mylabels.append(new_label)
```

### Step 13: Assign idx = _get_idx_label_stc(...)

```python
idx = _get_idx_label_stc(label, stc)
```

**Verification:**
```python
assert np.all(stc.data[idx] == 1.0)
```

### Step 14: Assign idx = np.intersect1d(...)

```python
idx = np.intersect1d(stc.vertices[hemi_idx], label.vertices)
```

### Step 15: Assign idx = np.searchsorted(...)

```python
idx = np.searchsorted(stc.vertices[hemi_idx], idx)
```

### Step 16: Assign res = value

```python
res = (2.0 * i) ** 2.0 * np.ones((len(idx), n_times))
```

### Step 17: Call assert_array_almost_equal()

```python
assert_array_almost_equal(stc.data[idx], res)
```

### Step 18: Assign hemi_idx = 0

```python
hemi_idx = 0
```

### Step 19: Assign hemi_idx = 1

```python
hemi_idx = 1
```


## Complete Example

```python
# Setup
# Fixtures: _get_fwd_labels

# Workflow
'Test generation of source estimate, single hemi.'
fwd, labels = _get_fwd_labels
labels_single_hemi = labels[1:]
mylabels = []
for i, label in enumerate(labels_single_hemi):
    new_label = Label(vertices=label.vertices, pos=label.pos, values=2 * i * np.ones(len(label.values)), hemi=label.hemi, comment=label.comment)
    mylabels.append(new_label)
n_times = 10
tmin = 0
tstep = 0.001
stc_data = np.ones((len(labels_single_hemi), n_times))
stc = simulate_stc(fwd['src'], mylabels, stc_data, tmin, tstep)
for label in labels_single_hemi:
    idx = _get_idx_label_stc(label, stc)
    assert np.all(stc.data[idx] == 1.0)
    assert stc.data[idx].shape[1] == n_times

def fun(x):
    return x ** 2
stc = simulate_stc(fwd['src'], mylabels, stc_data, tmin, tstep, fun)
for i, label in enumerate(labels_single_hemi):
    if label.hemi == 'lh':
        hemi_idx = 0
    else:
        hemi_idx = 1
    idx = np.intersect1d(stc.vertices[hemi_idx], label.vertices)
    idx = np.searchsorted(stc.vertices[hemi_idx], idx)
    if hemi_idx == 1:
        idx += len(stc.vertices[0])
    res = (2.0 * i) ** 2.0 * np.ones((len(idx), n_times))
    assert_array_almost_equal(stc.data[idx], res)
```

## Next Steps


---

*Source: test_source.py:227 | Complexity: Advanced | Last updated: 2026-05-18*