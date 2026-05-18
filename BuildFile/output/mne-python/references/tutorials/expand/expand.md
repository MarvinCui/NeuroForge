# How To: Expand

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test stc expansion.

## Prerequisites

**Required Modules:**
- `os`
- `re`
- `contextlib`
- `copy`
- `pathlib`
- `shutil`
- `numpy`
- `pytest`
- `numpy.fft`
- `numpy.testing`
- `scipy`
- `scipy.optimize`
- `scipy.spatial.distance`
- `mne`
- `mne`
- `mne._fiff.constants`
- `mne.datasets`
- `mne.fixes`
- `mne.io`
- `mne.label`
- `mne.minimum_norm`
- `mne.morph_map`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.transforms`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test stc expansion.'

```python
'Test stc expansion.'
```

**Verification:**
```python
assert 'sample' in repr(stc)
```

### Step 2: Assign stc_ = read_source_estimate(...)

```python
stc_ = read_source_estimate(fname_stc, 'sample')
```

### Step 3: Assign vec_stc_ = VectorSourceEstimate(...)

```python
vec_stc_ = VectorSourceEstimate(np.zeros((stc_.data.shape[0], 3, stc_.data.shape[1])), stc_.vertices, stc_.tmin, stc_.tstep, stc_.subject)
```

**Verification:**
```python
assert 'sample' in repr(stc)
```

### Step 4: Assign labels_lh = read_labels_from_annot(...)

```python
labels_lh = read_labels_from_annot('sample', 'aparc', 'lh', subjects_dir=subjects_dir)
```

### Step 5: Assign new_label = value

```python
new_label = labels_lh[0] + labels_lh[1]
```

### Step 6: Assign stc_limited = stc.in_label(...)

```python
stc_limited = stc.in_label(new_label)
```

### Step 7: Assign stc_new = stc_limited.copy(...)

```python
stc_new = stc_limited.copy()
```

### Step 8: Call stc_new.data.fill()

```python
stc_new.data.fill(0)
```

### Step 9: Call pytest.raises()

```python
pytest.raises(TypeError, stc_new.expand, stc_limited.vertices[0])
```

### Step 10: Call pytest.raises()

```python
pytest.raises(ValueError, stc_new.expand, [stc_limited.vertices[0]])
```

### Step 11: Call pytest.raises()

```python
pytest.raises(ValueError, stc.__add__, stc.in_label(labels_lh[0]))
```


## Complete Example

```python
# Workflow
'Test stc expansion.'
stc_ = read_source_estimate(fname_stc, 'sample')
vec_stc_ = VectorSourceEstimate(np.zeros((stc_.data.shape[0], 3, stc_.data.shape[1])), stc_.vertices, stc_.tmin, stc_.tstep, stc_.subject)
for stc in [stc_, vec_stc_]:
    assert 'sample' in repr(stc)
    labels_lh = read_labels_from_annot('sample', 'aparc', 'lh', subjects_dir=subjects_dir)
    new_label = labels_lh[0] + labels_lh[1]
    stc_limited = stc.in_label(new_label)
    stc_new = stc_limited.copy()
    stc_new.data.fill(0)
    for label in labels_lh[:2]:
        stc_new += stc.in_label(label).expand(stc_limited.vertices)
    pytest.raises(TypeError, stc_new.expand, stc_limited.vertices[0])
    pytest.raises(ValueError, stc_new.expand, [stc_limited.vertices[0]])
    pytest.raises(ValueError, stc.__add__, stc.in_label(labels_lh[0]))
```

## Next Steps


---

*Source: test_source_estimate.py:346 | Complexity: Advanced | Last updated: 2026-05-18*