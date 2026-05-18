# How To: Select Sources

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test the selection of sources for simulation.

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

### Step 1: 'Test the selection of sources for simulation.'

```python
'Test the selection of sources for simulation.'
```

**Verification:**
```python
assert len(label.vertices) == 1
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert set(new_label.vertices) > set(label.vertices)
```

### Step 3: Assign subject = 'sample'

```python
subject = 'sample'
```

**Verification:**
```python
assert new_label.hemi == 'lh'
```

### Step 4: Assign label_file = value

```python
label_file = subjects_dir / subject / 'label' / 'aparc' / 'temporalpole-rh.label'
```

**Verification:**
```python
assert set(label.vertices) == set(tp_label.vertices)
```

### Step 5: Assign tp_label = read_label(...)

```python
tp_label = read_label(label_file)
```

**Verification:**
```python
assert set(label.vertices) > set(tp_label.vertices)
```

### Step 6: Assign unknown = 1

```python
tp_label.values[:] = 1
```

**Verification:**
```python
assert label.name == 'mne'
```

### Step 7: Assign labels = value

```python
labels = ['lh', tp_label]
```

**Verification:**
```python
assert label.hemi == 'rh'
```

### Step 8: Assign locations = value

```python
locations = ['random', 'center']
```

### Step 9: Assign label = select_sources(...)

```python
label = select_sources(subject, 'lh', 0, extent=0, subjects_dir=subjects_dir)
```

### Step 10: Assign label = select_sources(...)

```python
label = select_sources(subject, tp_label, 0, extent=30, grow_outside=False, subjects_dir=subjects_dir)
```

**Verification:**
```python
assert set(label.vertices) == set(tp_label.vertices)
```

### Step 11: Assign label = select_sources(...)

```python
label = select_sources(subject, tp_label, 0, extent=30, grow_outside=True, subjects_dir=subjects_dir)
```

**Verification:**
```python
assert set(label.vertices) > set(tp_label.vertices)
```

### Step 12: Assign label = select_sources(...)

```python
label = select_sources(subject, tp_label, 0, extent=10, grow_outside=False, subjects_dir=subjects_dir, name='mne')
```

**Verification:**
```python
assert label.name == 'mne'
```

### Step 13: Assign label = select_sources(...)

```python
label = select_sources(subject, label, location, extent=0, subjects_dir=subjects_dir)
```

**Verification:**
```python
assert len(label.vertices) == 1
```

### Step 14: Assign new_label = select_sources(...)

```python
new_label = select_sources(subject, 'lh', 0, extent=extent * 2, subjects_dir=subjects_dir)
```

**Verification:**
```python
assert set(new_label.vertices) > set(label.vertices)
```

### Step 15: Assign label = new_label

```python
label = new_label
```


## Complete Example

```python
# Workflow
'Test the selection of sources for simulation.'
pytest.importorskip('nibabel')
subject = 'sample'
label_file = subjects_dir / subject / 'label' / 'aparc' / 'temporalpole-rh.label'
tp_label = read_label(label_file)
tp_label.values[:] = 1
labels = ['lh', tp_label]
locations = ['random', 'center']
for label, location in product(labels, locations):
    label = select_sources(subject, label, location, extent=0, subjects_dir=subjects_dir)
    assert len(label.vertices) == 1
label = select_sources(subject, 'lh', 0, extent=0, subjects_dir=subjects_dir)
for extent in range(1, 3):
    new_label = select_sources(subject, 'lh', 0, extent=extent * 2, subjects_dir=subjects_dir)
    assert set(new_label.vertices) > set(label.vertices)
    assert new_label.hemi == 'lh'
    label = new_label
label = select_sources(subject, tp_label, 0, extent=30, grow_outside=False, subjects_dir=subjects_dir)
assert set(label.vertices) == set(tp_label.vertices)
label = select_sources(subject, tp_label, 0, extent=30, grow_outside=True, subjects_dir=subjects_dir)
assert set(label.vertices) > set(tp_label.vertices)
label = select_sources(subject, tp_label, 0, extent=10, grow_outside=False, subjects_dir=subjects_dir, name='mne')
assert label.name == 'mne'
assert label.hemi == 'rh'
```

## Next Steps


---

*Source: test_label.py:1163 | Complexity: Advanced | Last updated: 2026-05-18*