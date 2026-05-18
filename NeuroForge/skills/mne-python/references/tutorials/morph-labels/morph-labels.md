# How To: Morph Labels

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test morph_labels.

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

### Step 1: 'Test morph_labels.'

```python
'Test morph_labels.'
```

**Verification:**
```python
assert lf.hemi == ls.hemi == lfs.hemi
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert lf.name == ls.name == lfs.name
```

### Step 3: Assign parc_fsaverage = value

```python
parc_fsaverage = read_labels_from_annot('fsaverage', 'aparc', subjects_dir=subjects_dir)[:5]
```

**Verification:**
```python
assert perc_1 > 92
```

### Step 4: Assign parc_sample = value

```python
parc_sample = read_labels_from_annot('sample', 'aparc', subjects_dir=subjects_dir)[:5]
```

**Verification:**
```python
assert perc_2 > 88
```

### Step 5: Assign parc_fssamp = morph_labels(...)

```python
parc_fssamp = morph_labels(parc_fsaverage, 'sample', subjects_dir=subjects_dir)
```

**Verification:**
```python
assert lf.hemi == ls.hemi == lfs.hemi
```

### Step 6: Assign perc_1 = value

```python
perc_1 = np.isin(lfs.vertices, ls.vertices).mean() * 100
```

### Step 7: Assign perc_2 = value

```python
perc_2 = np.isin(ls.vertices, lfs.vertices).mean() * 100
```

**Verification:**
```python
assert perc_1 > 92
```

### Step 8: Call morph_labels()

```python
morph_labels(parc_fsaverage, 'sample', subjects_dir=subjects_dir, subject_from='wrong')
```

### Step 9: Call _load_vert_pos()

```python
_load_vert_pos('sample', subjects_dir, 'white', 'lh', 1)
```

### Step 10: Assign label.subject = None

```python
label.subject = None
```

### Step 11: Call morph_labels()

```python
morph_labels(parc_fsaverage, 'sample', subjects_dir=subjects_dir)
```


## Complete Example

```python
# Workflow
'Test morph_labels.'
pytest.importorskip('nibabel')
parc_fsaverage = read_labels_from_annot('fsaverage', 'aparc', subjects_dir=subjects_dir)[:5]
parc_sample = read_labels_from_annot('sample', 'aparc', subjects_dir=subjects_dir)[:5]
parc_fssamp = morph_labels(parc_fsaverage, 'sample', subjects_dir=subjects_dir)
for lf, ls, lfs in zip(parc_fsaverage, parc_sample, parc_fssamp):
    assert lf.hemi == ls.hemi == lfs.hemi
    assert lf.name == ls.name == lfs.name
    perc_1 = np.isin(lfs.vertices, ls.vertices).mean() * 100
    perc_2 = np.isin(ls.vertices, lfs.vertices).mean() * 100
    assert perc_1 > 92
    assert perc_2 > 88
with pytest.raises(ValueError, match='wrong and fsaverage'):
    morph_labels(parc_fsaverage, 'sample', subjects_dir=subjects_dir, subject_from='wrong')
with pytest.raises(RuntimeError, match='Number of surface vertices'):
    _load_vert_pos('sample', subjects_dir, 'white', 'lh', 1)
for label in parc_fsaverage:
    label.subject = None
with pytest.raises(ValueError, match='subject_from must be provided'):
    morph_labels(parc_fsaverage, 'sample', subjects_dir=subjects_dir)
```

## Next Steps


---

*Source: test_label.py:416 | Complexity: Advanced | Last updated: 2026-05-18*