# How To: Labels To Stc

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test labels_to_stc.

## Prerequisites

**Required Modules:**
- `glob`
- `os`
- `pickle`
- `shutil`
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.label`
- `mne.source_estimate`
- `mne.source_space`
- `mne.surface`
- `mne.utils`


## Step-by-Step Guide

### Step 1: 'Test labels_to_stc.'

```python
'Test labels_to_stc.'
```

**Verification:**
```python
assert stc.subject == 'sample'
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert (stc_label.data == value).all()
```

### Step 3: Assign labels = read_labels_from_annot(...)

```python
labels = read_labels_from_annot('sample', 'aparc', subjects_dir=subjects_dir)
```

### Step 4: Assign values = np.random.RandomState.randn(...)

```python
values = np.random.RandomState(0).randn(len(labels))
```

### Step 5: Assign stc = labels_to_stc(...)

```python
stc = labels_to_stc(labels, values)
```

**Verification:**
```python
assert stc.subject == 'sample'
```

### Step 6: Assign stc = read_source_estimate(...)

```python
stc = read_source_estimate(stc_fname, 'sample')
```

### Step 7: Call labels_to_stc()

```python
labels_to_stc(labels, values[:, np.newaxis, np.newaxis])
```

### Step 8: Call labels_to_stc()

```python
labels_to_stc(labels, values[np.newaxis])
```

### Step 9: Call labels_to_stc()

```python
labels_to_stc(labels, values, subject='foo')
```

### Step 10: Assign stc_label = stc.in_label(...)

```python
stc_label = stc.in_label(label)
```

**Verification:**
```python
assert (stc_label.data == value).all()
```


## Complete Example

```python
# Workflow
'Test labels_to_stc.'
pytest.importorskip('nibabel')
labels = read_labels_from_annot('sample', 'aparc', subjects_dir=subjects_dir)
values = np.random.RandomState(0).randn(len(labels))
with pytest.raises(ValueError, match='1 or 2 dim'):
    labels_to_stc(labels, values[:, np.newaxis, np.newaxis])
with pytest.raises(ValueError, match='values\\.shape'):
    labels_to_stc(labels, values[np.newaxis])
with pytest.raises(ValueError, match='multiple values of subject'):
    labels_to_stc(labels, values, subject='foo')
stc = labels_to_stc(labels, values)
assert stc.subject == 'sample'
for value, label in zip(values, labels):
    stc_label = stc.in_label(label)
    assert (stc_label.data == value).all()
stc = read_source_estimate(stc_fname, 'sample')
```

## Next Steps


---

*Source: test_label.py:449 | Complexity: Advanced | Last updated: 2026-05-18*