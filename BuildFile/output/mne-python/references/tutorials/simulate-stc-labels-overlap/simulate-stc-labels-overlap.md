# How To: Simulate Stc Labels Overlap

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test generation of source estimate, overlapping labels.

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

### Step 1: 'Test generation of source estimate, overlapping labels.'

```python
'Test generation of source estimate, overlapping labels.'
```

**Verification:**
```python
assert_equal(stc.subject, 'sample')
```

### Step 2: Assign unknown = _get_fwd_labels

```python
fwd, labels = _get_fwd_labels
```

**Verification:**
```python
assert stc.data.shape[1] == n_times
```

### Step 3: Assign mylabels = value

```python
mylabels = []
```

**Verification:**
```python
assert 2 in stc.data
```

### Step 4: Call mylabels.append()

```python
mylabels.append(new_label)
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
stc_data = np.ones((len(mylabels), n_times))
```

### Step 9: Assign stc = simulate_stc(...)

```python
stc = simulate_stc(fwd['src'], mylabels, stc_data, tmin, tstep, allow_overlap=True)
```

### Step 10: Call assert_equal()

```python
assert_equal(stc.subject, 'sample')
```

**Verification:**
```python
assert stc.data.shape[1] == n_times
```

### Step 11: Assign new_label = Label(...)

```python
new_label = Label(vertices=label.vertices, pos=label.pos, values=2 * i * np.ones(len(label.values)), hemi=label.hemi, comment=label.comment)
```

### Step 12: Call mylabels.append()

```python
mylabels.append(new_label)
```

### Step 13: Call simulate_stc()

```python
simulate_stc(fwd['src'], mylabels, stc_data, tmin, tstep, allow_overlap=False)
```


## Complete Example

```python
# Setup
# Fixtures: _get_fwd_labels

# Workflow
'Test generation of source estimate, overlapping labels.'
fwd, labels = _get_fwd_labels
mylabels = []
for i, label in enumerate(labels):
    new_label = Label(vertices=label.vertices, pos=label.pos, values=2 * i * np.ones(len(label.values)), hemi=label.hemi, comment=label.comment)
    mylabels.append(new_label)
mylabels.append(new_label)
n_times = 10
tmin = 0
tstep = 0.001
stc_data = np.ones((len(mylabels), n_times))
with pytest.raises(RuntimeError, match='must be non-overlapping'):
    simulate_stc(fwd['src'], mylabels, stc_data, tmin, tstep, allow_overlap=False)
stc = simulate_stc(fwd['src'], mylabels, stc_data, tmin, tstep, allow_overlap=True)
assert_equal(stc.subject, 'sample')
assert stc.data.shape[1] == n_times
assert 2 in stc.data
```

## Next Steps


---

*Source: test_source.py:314 | Complexity: Advanced | Last updated: 2026-05-18*