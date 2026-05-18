# How To: Extract Label Time Course Equiv

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test extraction of label time courses from stc equivalences.

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

### Step 1: 'Test extraction of label time courses from stc equivalences.'

```python
'Test extraction of label time courses from stc equivalences.'
```

**Verification:**
```python
assert len(label) == 1
```

### Step 2: Assign label = read_labels_from_annot(...)

```python
label = read_labels_from_annot('sample', 'aparc', 'lh', regexp='transv', subjects_dir=subjects_dir)
```

**Verification:**
```python
assert_allclose(mean, mean_2)
```

### Step 3: Assign label = value

```python
label = label[0]
```

**Verification:**
```python
assert len(stc_in_label.vertices[0]) == 22
```

### Step 4: Assign inv = read_inverse_operator(...)

```python
inv = read_inverse_operator(fname_inv)
```

### Step 5: Assign evoked = unknown.crop(...)

```python
evoked = read_evokeds(fname_evoked, baseline=(None, 0))[0].crop(0, 0.01)
```

### Step 6: Assign stc = apply_inverse(...)

```python
stc = apply_inverse(evoked, inv, pick_ori='normal', label=label)
```

### Step 7: Assign stc_full = apply_inverse(...)

```python
stc_full = apply_inverse(evoked, inv, pick_ori='normal')
```

### Step 8: Assign stc_in_label = stc_full.in_label(...)

```python
stc_in_label = stc_full.in_label(label)
```

### Step 9: Assign mean = stc.extract_label_time_course(...)

```python
mean = stc.extract_label_time_course(label, inv['src'])
```

### Step 10: Assign mean_2 = stc_in_label.extract_label_time_course(...)

```python
mean_2 = stc_in_label.extract_label_time_course(label, inv['src'])
```

### Step 11: Call assert_allclose()

```python
assert_allclose(mean, mean_2)
```

### Step 12: Assign unknown = np.array(...)

```python
inv['src'][0]['vertno'] = np.array([], int)
```

**Verification:**
```python
assert len(stc_in_label.vertices[0]) == 22
```

### Step 13: Call stc_in_label.extract_label_time_course()

```python
stc_in_label.extract_label_time_course(label, inv['src'])
```


## Complete Example

```python
# Workflow
'Test extraction of label time courses from stc equivalences.'
label = read_labels_from_annot('sample', 'aparc', 'lh', regexp='transv', subjects_dir=subjects_dir)
assert len(label) == 1
label = label[0]
inv = read_inverse_operator(fname_inv)
evoked = read_evokeds(fname_evoked, baseline=(None, 0))[0].crop(0, 0.01)
stc = apply_inverse(evoked, inv, pick_ori='normal', label=label)
stc_full = apply_inverse(evoked, inv, pick_ori='normal')
stc_in_label = stc_full.in_label(label)
mean = stc.extract_label_time_course(label, inv['src'])
mean_2 = stc_in_label.extract_label_time_course(label, inv['src'])
assert_allclose(mean, mean_2)
inv['src'][0]['vertno'] = np.array([], int)
assert len(stc_in_label.vertices[0]) == 22
with pytest.raises(ValueError, match='22/22 left hemisphere.*missing'):
    stc_in_label.extract_label_time_course(label, inv['src'])
```

## Next Steps


---

*Source: test_source_estimate.py:1044 | Complexity: Advanced | Last updated: 2026-05-18*