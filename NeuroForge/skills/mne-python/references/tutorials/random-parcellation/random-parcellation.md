# How To: Random Parcellation

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test generation of random cortical parcellation.

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

### Step 1: 'Test generation of random cortical parcellation.'

```python
'Test generation of random cortical parcellation.'
```

**Verification:**
```python
assert_equal(len(labels), n_parcel)
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert len(label.vertices) > 0
```

### Step 3: Assign hemi = 'both'

```python
hemi = 'both'
```

**Verification:**
```python
assert_equal(len(np.unique(vertices_total)), len(vertices_total))
```

### Step 4: Assign n_parcel = 50

```python
n_parcel = 50
```

**Verification:**
```python
assert_array_equal(np.sort(vertices_total), np.arange(len(vert)))
```

### Step 5: Assign surface = 'sphere.reg'

```python
surface = 'sphere.reg'
```

### Step 6: Assign subject = 'sample_ds'

```python
subject = 'sample_ds'
```

### Step 7: Assign rng = np.random.RandomState(...)

```python
rng = np.random.RandomState(0)
```

### Step 8: Assign labels = random_parcellation(...)

```python
labels = random_parcellation(subject, n_parcel, hemi, subjects_dir, surface=surface, random_state=rng)
```

### Step 9: Call assert_equal()

```python
assert_equal(len(labels), n_parcel)
```

### Step 10: Assign hemis = np.atleast_1d(...)

```python
hemis = np.atleast_1d(hemi)
```

### Step 11: Assign hemi = value

```python
hemi = ['lh', 'rh']
```

### Step 12: Assign vertices_total = value

```python
vertices_total = []
```

### Step 13: Call assert_equal()

```python
assert_equal(len(np.unique(vertices_total)), len(vertices_total))
```

### Step 14: Assign surf_fname = value

```python
surf_fname = subjects_dir / subject / 'surf' / (hemi + '.' + surface)
```

### Step 15: Assign unknown = read_surface(...)

```python
vert, _ = read_surface(surf_fname)
```

### Step 16: Call assert_array_equal()

```python
assert_array_equal(np.sort(vertices_total), np.arange(len(vert)))
```

**Verification:**
```python
assert len(label.vertices) > 0
```

### Step 17: Assign vertices_total = np.append(...)

```python
vertices_total = np.append(vertices_total, label.vertices)
```


## Complete Example

```python
# Workflow
'Test generation of random cortical parcellation.'
pytest.importorskip('nibabel')
hemi = 'both'
n_parcel = 50
surface = 'sphere.reg'
subject = 'sample_ds'
rng = np.random.RandomState(0)
labels = random_parcellation(subject, n_parcel, hemi, subjects_dir, surface=surface, random_state=rng)
assert_equal(len(labels), n_parcel)
if hemi == 'both':
    hemi = ['lh', 'rh']
hemis = np.atleast_1d(hemi)
for hemi in set(hemis):
    vertices_total = []
    for label in labels:
        if label.hemi == hemi:
            assert len(label.vertices) > 0
            vertices_total = np.append(vertices_total, label.vertices)
    assert_equal(len(np.unique(vertices_total)), len(vertices_total))
    surf_fname = subjects_dir / subject / 'surf' / (hemi + '.' + surface)
    vert, _ = read_surface(surf_fname)
    assert_array_equal(np.sort(vertices_total), np.arange(len(vert)))
```

## Next Steps


---

*Source: test_label.py:1024 | Complexity: Advanced | Last updated: 2026-05-18*