# How To: Morph

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test inter-subject label morphing.

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

### Step 1: 'Test inter-subject label morphing.'

```python
'Test inter-subject label morphing.'
```

**Verification:**
```python
assert np.isin(label_orig.vertices, label.vertices).all()
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert len(label.vertices) < 3 * len(label_orig.vertices)
```

### Step 3: Assign label_orig = read_label(...)

```python
label_orig = read_label(real_label_fname)
```

**Verification:**
```python
assert_array_equal(vals[0], vals[1])
```

### Step 4: Assign label_orig.subject = 'sample'

```python
label_orig.subject = 'sample'
```

**Verification:**
```python
assert_equal(label.subject, 'sample')
```

### Step 5: Assign vals = list(...)

```python
vals = list()
```

### Step 6: Call assert_array_equal()

```python
assert_array_equal(vals[0], vals[1])
```

### Step 7: Call assert_equal()

```python
assert_equal(label.subject, 'sample')
```

### Step 8: Assign verts = value

```python
verts = [np.arange(10242), np.arange(10242)]
```

### Step 9: Call pytest.raises()

```python
pytest.raises(TypeError, label.morph, None, 1, 5, verts, subjects_dir, 2)
```

### Step 10: Call pytest.raises()

```python
pytest.raises(TypeError, label.morph, None, 'fsaverage', 5.5, verts, subjects_dir, 2)
```

### Step 11: Assign label = label_orig.copy(...)

```python
label = label_orig.copy()
```

### Step 12: Call pytest.raises()

```python
pytest.raises(ValueError, label.morph, 'sample', 'fsaverage')
```

### Step 13: Call label.values.fill()

```python
label.values.fill(1)
```

### Step 14: Assign label = label.morph(...)

```python
label = label.morph(None, 'fsaverage', 5, grade, subjects_dir, 1)
```

### Step 15: Assign label = label.morph(...)

```python
label = label.morph('fsaverage', 'sample', 5, None, subjects_dir, 2)
```

**Verification:**
```python
assert np.isin(label_orig.vertices, label.vertices).all()
```

### Step 16: Call vals.append()

```python
vals.append(label.vertices)
```

### Step 17: Assign label.hemi = hemi

```python
label.hemi = hemi
```

### Step 18: Call label.smooth()

```python
label.smooth(subjects_dir=subjects_dir)
```

### Step 19: Call label.morph()

```python
label.morph(None, 'fsaverage', 5, verts, subjects_dir, 2)
```


## Complete Example

```python
# Workflow
'Test inter-subject label morphing.'
pytest.importorskip('nibabel')
label_orig = read_label(real_label_fname)
label_orig.subject = 'sample'
vals = list()
for grade in [5, [np.arange(10242), np.arange(10242)], np.arange(10242)]:
    label = label_orig.copy()
    pytest.raises(ValueError, label.morph, 'sample', 'fsaverage')
    label.values.fill(1)
    label = label.morph(None, 'fsaverage', 5, grade, subjects_dir, 1)
    label = label.morph('fsaverage', 'sample', 5, None, subjects_dir, 2)
    assert np.isin(label_orig.vertices, label.vertices).all()
    assert len(label.vertices) < 3 * len(label_orig.vertices)
    vals.append(label.vertices)
assert_array_equal(vals[0], vals[1])
assert_equal(label.subject, 'sample')
verts = [np.arange(10242), np.arange(10242)]
for hemi in ['lh', 'rh']:
    label.hemi = hemi
    with _record_warnings():
        label.morph(None, 'fsaverage', 5, verts, subjects_dir, 2)
pytest.raises(TypeError, label.morph, None, 1, 5, verts, subjects_dir, 2)
pytest.raises(TypeError, label.morph, None, 'fsaverage', 5.5, verts, subjects_dir, 2)
with _record_warnings():
    label.smooth(subjects_dir=subjects_dir)
```

## Next Steps


---

*Source: test_label.py:921 | Complexity: Advanced | Last updated: 2026-05-18*