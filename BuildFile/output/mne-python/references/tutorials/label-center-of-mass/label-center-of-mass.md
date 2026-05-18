# How To: Label Center Of Mass

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test computing the center of mass of a label.

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

### Step 1: 'Test computing the center of mass of a label.'

```python
'Test computing the center of mass of a label.'
```

**Verification:**
```python
assert_equal(vertex_stc, 124791)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert_equal(vertex_label, vertex_stc)
```

### Step 3: Assign stc = read_source_estimate(...)

```python
stc = read_source_estimate(stc_fname)
```

**Verification:**
```python
assert_equal(label.center_of_mass(subjects_dir=subjects_dir), expected)
```

### Step 4: Assign unknown = 0

```python
stc.lh_data[:] = 0
```

**Verification:**
```python
assert_equal(label.center_of_mass(subjects_dir=subjects_dir, restrict_vertices=label.vertices), expected)
```

### Step 5: Assign vertex_stc = value

```python
vertex_stc = stc.center_of_mass('sample', subjects_dir=subjects_dir)[0]
```

**Verification:**
```python
assert_equal(label.center_of_mass(subjects_dir=subjects_dir, restrict_vertices=src_restrict), src_expected)
```

### Step 6: Call assert_equal()

```python
assert_equal(vertex_stc, 124791)
```

**Verification:**
```python
assert_equal(label.center_of_mass(subjects_dir=subjects_dir, restrict_vertices=src), src_expected)
```

### Step 7: Assign label = Label(...)

```python
label = Label(stc.vertices[1], pos=None, values=stc.rh_data.mean(axis=1), hemi='rh', subject='sample')
```

### Step 8: Assign vertex_label = label.center_of_mass(...)

```python
vertex_label = label.center_of_mass(subjects_dir=subjects_dir)
```

### Step 9: Call assert_equal()

```python
assert_equal(vertex_label, vertex_stc)
```

### Step 10: Assign labels = read_labels_from_annot(...)

```python
labels = read_labels_from_annot('sample', parc='aparc.a2009s', subjects_dir=subjects_dir)
```

### Step 11: Assign src = read_source_spaces(...)

```python
src = read_source_spaces(src_fname)
```

### Step 12: Call pytest.raises()

```python
pytest.raises(ValueError, label.center_of_mass, subjects_dir=subjects_dir, restrict_vertices='foo')
```

### Step 13: Call pytest.raises()

```python
pytest.raises(TypeError, label.center_of_mass, subjects_dir=subjects_dir, surf=1)
```

### Step 14: Call pytest.raises()

```python
pytest.raises(OSError, label.center_of_mass, subjects_dir=subjects_dir, surf='foo')
```

### Step 15: Assign unknown = value

```python
label.values[:] = -1
```

### Step 16: Call pytest.raises()

```python
pytest.raises(ValueError, label.center_of_mass, subjects_dir=subjects_dir)
```

### Step 17: Assign unknown = 0

```python
label.values[:] = 0
```

### Step 18: Call pytest.raises()

```python
pytest.raises(ValueError, label.center_of_mass, subjects_dir=subjects_dir)
```

### Step 19: Assign unknown = 1

```python
label.values[:] = 1
```

### Step 20: Call assert_equal()

```python
assert_equal(label.center_of_mass(subjects_dir=subjects_dir), expected)
```

### Step 21: Call assert_equal()

```python
assert_equal(label.center_of_mass(subjects_dir=subjects_dir, restrict_vertices=label.vertices), expected)
```

### Step 22: Assign idx = value

```python
idx = 0 if label.hemi == 'lh' else 1
```

### Step 23: Assign pos = value

```python
pos = label.pos[np.where(label.vertices == expected)[0][0]]
```

### Step 24: Assign pos = value

```python
pos = src[idx]['rr'][src[idx]['vertno']] - pos
```

### Step 25: Assign pos = np.argmin(...)

```python
pos = np.argmin(np.sum(pos * pos, axis=1))
```

### Step 26: Assign src_expected = value

```python
src_expected = src[idx]['vertno'][pos]
```

### Step 27: Assign src_restrict = np.intersect1d(...)

```python
src_restrict = np.intersect1d(label.vertices, src[idx]['vertno'])
```

### Step 28: Call assert_equal()

```python
assert_equal(label.center_of_mass(subjects_dir=subjects_dir, restrict_vertices=src_restrict), src_expected)
```

### Step 29: Call assert_equal()

```python
assert_equal(label.center_of_mass(subjects_dir=subjects_dir, restrict_vertices=src), src_expected)
```


## Complete Example

```python
# Workflow
'Test computing the center of mass of a label.'
pytest.importorskip('nibabel')
stc = read_source_estimate(stc_fname)
stc.lh_data[:] = 0
vertex_stc = stc.center_of_mass('sample', subjects_dir=subjects_dir)[0]
assert_equal(vertex_stc, 124791)
label = Label(stc.vertices[1], pos=None, values=stc.rh_data.mean(axis=1), hemi='rh', subject='sample')
vertex_label = label.center_of_mass(subjects_dir=subjects_dir)
assert_equal(vertex_label, vertex_stc)
labels = read_labels_from_annot('sample', parc='aparc.a2009s', subjects_dir=subjects_dir)
src = read_source_spaces(src_fname)
for label, expected in zip([labels[2], labels[3], labels[-5]], [141162, 145221, 55979]):
    label.values[:] = -1
    pytest.raises(ValueError, label.center_of_mass, subjects_dir=subjects_dir)
    label.values[:] = 0
    pytest.raises(ValueError, label.center_of_mass, subjects_dir=subjects_dir)
    label.values[:] = 1
    assert_equal(label.center_of_mass(subjects_dir=subjects_dir), expected)
    assert_equal(label.center_of_mass(subjects_dir=subjects_dir, restrict_vertices=label.vertices), expected)
    idx = 0 if label.hemi == 'lh' else 1
    pos = label.pos[np.where(label.vertices == expected)[0][0]]
    pos = src[idx]['rr'][src[idx]['vertno']] - pos
    pos = np.argmin(np.sum(pos * pos, axis=1))
    src_expected = src[idx]['vertno'][pos]
    src_restrict = np.intersect1d(label.vertices, src[idx]['vertno'])
    assert_equal(label.center_of_mass(subjects_dir=subjects_dir, restrict_vertices=src_restrict), src_expected)
    assert_equal(label.center_of_mass(subjects_dir=subjects_dir, restrict_vertices=src), src_expected)
pytest.raises(ValueError, label.center_of_mass, subjects_dir=subjects_dir, restrict_vertices='foo')
pytest.raises(TypeError, label.center_of_mass, subjects_dir=subjects_dir, surf=1)
pytest.raises(OSError, label.center_of_mass, subjects_dir=subjects_dir, surf='foo')
```

## Next Steps


---

*Source: test_label.py:1093 | Complexity: Advanced | Last updated: 2026-05-18*