# How To: Make Morph Maps

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test reading and creating morph maps.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `os`
- `shutil`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne.datasets`
- `mne.fixes`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test reading and creating morph maps.'

```python
'Test reading and creating morph maps.'
```

**Verification:**
```python
assert 'does not exist' in log
```

### Step 2: Call pytest.importorskip()

```python
pytest.importorskip('nibabel')
```

**Verification:**
```python
assert 'Creating' in log
```

### Step 3: Call os.mkdir()

```python
os.mkdir(tmp_path / subject)
```

**Verification:**
```python
assert len(mmap) == len(mmap2)
```

### Step 4: Call os.mkdir()

```python
os.mkdir(tmp_path / subject / 'surf')
```

**Verification:**
```python
assert_allclose(diff, np.zeros_like(diff), atol=0.001, rtol=0)
```

### Step 5: Assign regs = value

```python
regs = ('reg', 'left_right') if subject == 'fsaverage_ds' else ('reg',)
```

**Verification:**
```python
assert (mm - _eye_array(mm.shape[0])).sum() == 0
```

### Step 6: Assign log = log.getvalue(...)

```python
log = log.getvalue()
```

**Verification:**
```python
assert 'does not exist' in log
```

### Step 7: Assign mmap2 = read_morph_map(...)

```python
mmap2 = read_morph_map(subject_from, subject_to, subjects_dir, xhemi=xhemi)
```

**Verification:**
```python
assert len(mmap) == len(mmap2)
```

### Step 8: Assign mmap = read_morph_map(...)

```python
mmap = read_morph_map('sample', 'sample', subjects_dir=tmp_path)
```

**Verification:**
```python
assert (mm - _eye_array(mm.shape[0])).sum() == 0
```

### Step 9: Assign mmap = read_morph_map(...)

```python
mmap = read_morph_map(subject_from, subject_to, tmp_path, xhemi=xhemi, verbose=True)
```

### Step 10: Assign diff = value

```python
diff = (m1 - m2).data
```

### Step 11: Call assert_allclose()

```python
assert_allclose(diff, np.zeros_like(diff), atol=0.001, rtol=0)
```

### Step 12: Call copyfile()

```python
copyfile(subjects_dir / subject / 'surf' / f'{hemi}.sphere.{reg}', tmp_path / subject / 'surf' / f'{hemi}.sphere.{reg}')
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test reading and creating morph maps.'
pytest.importorskip('nibabel')
for subject in ('sample', 'sample_ds', 'fsaverage_ds'):
    os.mkdir(tmp_path / subject)
    os.mkdir(tmp_path / subject / 'surf')
    regs = ('reg', 'left_right') if subject == 'fsaverage_ds' else ('reg',)
    for hemi in ['lh', 'rh']:
        for reg in regs:
            copyfile(subjects_dir / subject / 'surf' / f'{hemi}.sphere.{reg}', tmp_path / subject / 'surf' / f'{hemi}.sphere.{reg}')
for subject_from, subject_to, xhemi in (('fsaverage_ds', 'sample_ds', False), ('fsaverage_ds', 'fsaverage_ds', True)):
    with catch_logging() as log:
        mmap = read_morph_map(subject_from, subject_to, tmp_path, xhemi=xhemi, verbose=True)
    log = log.getvalue()
    assert 'does not exist' in log
    assert 'Creating' in log
    mmap2 = read_morph_map(subject_from, subject_to, subjects_dir, xhemi=xhemi)
    assert len(mmap) == len(mmap2)
    for m1, m2 in zip(mmap, mmap2):
        diff = (m1 - m2).data
        assert_allclose(diff, np.zeros_like(diff), atol=0.001, rtol=0)
with _record_warnings():
    mmap = read_morph_map('sample', 'sample', subjects_dir=tmp_path)
for mm in mmap:
    assert (mm - _eye_array(mm.shape[0])).sum() == 0
```

## Next Steps


---

*Source: test_morph_map.py:23 | Complexity: Advanced | Last updated: 2026-05-18*