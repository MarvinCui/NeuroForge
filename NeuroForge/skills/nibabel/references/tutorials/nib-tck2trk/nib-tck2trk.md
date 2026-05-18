# How To: Nib Tck2Trk

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test nib tck2trk

## Prerequisites

**Required Modules:**
- `csv`
- `os`
- `shutil`
- `sys`
- `unittest`
- `glob`
- `os.path`
- `os.path`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel`
- `loadsave`
- `orientations`
- `testing`
- `tmpdirs`
- `nibabel_data`
- `scriptrunner`
- `test_parrec`
- `test_parrec`
- `test_parrec_data`
- `fuse`


## Step-by-Step Guide

### Step 1: Assign anat = pjoin(...)

```python
anat = pjoin(DATA_PATH, 'standard.nii.gz')
```

**Verification:**
```python
assert code == 2
```

### Step 2: Assign standard_tck = pjoin(...)

```python
standard_tck = pjoin(DATA_PATH, 'standard.tck')
```

**Verification:**
```python
assert 'Expecting anatomical image as first argument' in stderr
```

### Step 3: Call shutil.copy()

```python
shutil.copy(standard_tck, tmpdir)
```

**Verification:**
```python
assert len(stdout) == 0
```

### Step 4: Assign standard_trk = pjoin(...)

```python
standard_trk = pjoin(tmpdir, 'standard.trk')
```

**Verification:**
```python
assert os.path.isfile(standard_trk)
```

### Step 5: Assign standard_tck = pjoin(...)

```python
standard_tck = pjoin(tmpdir, 'standard.tck')
```

**Verification:**
```python
assert (trk.streamlines.get_data() == tck.streamlines.get_data()).all()
```

### Step 6: Assign cmd = value

```python
cmd = ['nib-tck2trk', standard_tck, anat]
```

**Verification:**
```python
assert isinstance(trk, nib.streamlines.TrkFile)
```

### Step 7: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(cmd, check_code=False)
```

**Verification:**
```python
assert 'Skipping non TCK file' in stdout
```

### Step 8: Assign cmd = value

```python
cmd = ['nib-tck2trk', anat, standard_tck]
```

**Verification:**
```python
assert 'Skipping existing file' in stdout
```

### Step 9: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(cmd)
```

**Verification:**
```python
assert len(stdout) == 0
```

### Step 10: Assign tck = nib.streamlines.load(...)

```python
tck = nib.streamlines.load(standard_tck)
```

**Verification:**
```python
assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
```

### Step 11: Assign trk = nib.streamlines.load(...)

```python
trk = nib.streamlines.load(standard_trk)
```

**Verification:**
```python
assert (trk.streamlines.get_data() == tck.streamlines.get_data()).all()
```

### Step 12: Assign cmd = value

```python
cmd = ['nib-tck2trk', anat, standard_trk]
```

### Step 13: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(cmd)
```

**Verification:**
```python
assert 'Skipping non TCK file' in stdout
```

### Step 14: Assign cmd = value

```python
cmd = ['nib-tck2trk', anat, standard_tck]
```

### Step 15: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(cmd)
```

**Verification:**
```python
assert 'Skipping existing file' in stdout
```

### Step 16: Assign cmd = value

```python
cmd = ['nib-tck2trk', '--force', anat, standard_tck, standard_tck]
```

### Step 17: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(cmd)
```

**Verification:**
```python
assert len(stdout) == 0
```

### Step 18: Assign tck = nib.streamlines.load(...)

```python
tck = nib.streamlines.load(standard_tck)
```

### Step 19: Assign trk = nib.streamlines.load(...)

```python
trk = nib.streamlines.load(standard_trk)
```

**Verification:**
```python
assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
```


## Complete Example

```python
# Workflow
anat = pjoin(DATA_PATH, 'standard.nii.gz')
standard_tck = pjoin(DATA_PATH, 'standard.tck')
with InTemporaryDirectory() as tmpdir:
    shutil.copy(standard_tck, tmpdir)
    standard_trk = pjoin(tmpdir, 'standard.trk')
    standard_tck = pjoin(tmpdir, 'standard.tck')
    cmd = ['nib-tck2trk', standard_tck, anat]
    code, stdout, stderr = run_command(cmd, check_code=False)
    assert code == 2
    assert 'Expecting anatomical image as first argument' in stderr
    cmd = ['nib-tck2trk', anat, standard_tck]
    code, stdout, stderr = run_command(cmd)
    assert len(stdout) == 0
    assert os.path.isfile(standard_trk)
    tck = nib.streamlines.load(standard_tck)
    trk = nib.streamlines.load(standard_trk)
    assert (trk.streamlines.get_data() == tck.streamlines.get_data()).all()
    assert isinstance(trk, nib.streamlines.TrkFile)
    cmd = ['nib-tck2trk', anat, standard_trk]
    code, stdout, stderr = run_command(cmd)
    assert 'Skipping non TCK file' in stdout
    cmd = ['nib-tck2trk', anat, standard_tck]
    code, stdout, stderr = run_command(cmd)
    assert 'Skipping existing file' in stdout
    cmd = ['nib-tck2trk', '--force', anat, standard_tck, standard_tck]
    code, stdout, stderr = run_command(cmd)
    assert len(stdout) == 0
    tck = nib.streamlines.load(standard_tck)
    trk = nib.streamlines.load(standard_trk)
    assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
```

## Next Steps


---

*Source: test_scripts.py:485 | Complexity: Advanced | Last updated: 2026-05-18*