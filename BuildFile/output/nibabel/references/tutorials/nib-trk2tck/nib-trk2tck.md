# How To: Nib Trk2Tck

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, unittest, workflow, integration

## Overview

Workflow: test nib trk2tck

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

### Step 1: Assign simple_trk = pjoin(...)

```python
simple_trk = pjoin(DATA_PATH, 'simple.trk')
```

**Verification:**
```python
assert len(stdout) == 0
```

### Step 2: Assign standard_trk = pjoin(...)

```python
standard_trk = pjoin(DATA_PATH, 'standard.trk')
```

**Verification:**
```python
assert os.path.isfile(simple_tck)
```

### Step 3: Call shutil.copy()

```python
shutil.copy(simple_trk, tmpdir)
```

**Verification:**
```python
assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
```

### Step 4: Call shutil.copy()

```python
shutil.copy(standard_trk, tmpdir)
```

**Verification:**
```python
assert isinstance(tck, nib.streamlines.TckFile)
```

### Step 5: Assign simple_trk = pjoin(...)

```python
simple_trk = pjoin(tmpdir, 'simple.trk')
```

**Verification:**
```python
assert 'Skipping non TRK file' in stdout
```

### Step 6: Assign standard_trk = pjoin(...)

```python
standard_trk = pjoin(tmpdir, 'standard.trk')
```

**Verification:**
```python
assert 'Skipping existing file' in stdout
```

### Step 7: Assign simple_tck = pjoin(...)

```python
simple_tck = pjoin(tmpdir, 'simple.tck')
```

**Verification:**
```python
assert len(stdout) == 0
```

### Step 8: Assign standard_tck = pjoin(...)

```python
standard_tck = pjoin(tmpdir, 'standard.tck')
```

**Verification:**
```python
assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
```

### Step 9: Assign cmd = value

```python
cmd = ['nib-trk2tck', simple_trk]
```

### Step 10: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(cmd)
```

**Verification:**
```python
assert len(stdout) == 0
```

### Step 11: Assign trk = nib.streamlines.load(...)

```python
trk = nib.streamlines.load(simple_trk)
```

### Step 12: Assign tck = nib.streamlines.load(...)

```python
tck = nib.streamlines.load(simple_tck)
```

**Verification:**
```python
assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
```

### Step 13: Assign cmd = value

```python
cmd = ['nib-trk2tck', simple_tck]
```

### Step 14: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(cmd)
```

**Verification:**
```python
assert 'Skipping non TRK file' in stdout
```

### Step 15: Assign cmd = value

```python
cmd = ['nib-trk2tck', simple_trk]
```

### Step 16: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(cmd)
```

**Verification:**
```python
assert 'Skipping existing file' in stdout
```

### Step 17: Assign cmd = value

```python
cmd = ['nib-trk2tck', '--force', simple_trk, standard_trk]
```

### Step 18: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(cmd)
```

**Verification:**
```python
assert len(stdout) == 0
```

### Step 19: Assign trk = nib.streamlines.load(...)

```python
trk = nib.streamlines.load(standard_trk)
```

### Step 20: Assign tck = nib.streamlines.load(...)

```python
tck = nib.streamlines.load(standard_tck)
```

**Verification:**
```python
assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
```


## Complete Example

```python
# Workflow
simple_trk = pjoin(DATA_PATH, 'simple.trk')
standard_trk = pjoin(DATA_PATH, 'standard.trk')
with InTemporaryDirectory() as tmpdir:
    shutil.copy(simple_trk, tmpdir)
    shutil.copy(standard_trk, tmpdir)
    simple_trk = pjoin(tmpdir, 'simple.trk')
    standard_trk = pjoin(tmpdir, 'standard.trk')
    simple_tck = pjoin(tmpdir, 'simple.tck')
    standard_tck = pjoin(tmpdir, 'standard.tck')
    cmd = ['nib-trk2tck', simple_trk]
    code, stdout, stderr = run_command(cmd)
    assert len(stdout) == 0
    assert os.path.isfile(simple_tck)
    trk = nib.streamlines.load(simple_trk)
    tck = nib.streamlines.load(simple_tck)
    assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
    assert isinstance(tck, nib.streamlines.TckFile)
    cmd = ['nib-trk2tck', simple_tck]
    code, stdout, stderr = run_command(cmd)
    assert 'Skipping non TRK file' in stdout
    cmd = ['nib-trk2tck', simple_trk]
    code, stdout, stderr = run_command(cmd)
    assert 'Skipping existing file' in stdout
    cmd = ['nib-trk2tck', '--force', simple_trk, standard_trk]
    code, stdout, stderr = run_command(cmd)
    assert len(stdout) == 0
    trk = nib.streamlines.load(standard_trk)
    tck = nib.streamlines.load(standard_tck)
    assert (tck.streamlines.get_data() == trk.streamlines.get_data()).all()
```

## Next Steps


---

*Source: test_scripts.py:441 | Complexity: Advanced | Last updated: 2026-05-18*