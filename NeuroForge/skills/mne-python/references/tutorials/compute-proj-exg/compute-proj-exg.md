# How To: Compute Proj Exg

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test mne compute_proj_ecg/eog.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `glob`
- `os`
- `platform`
- `shutil`
- `os`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne`
- `mne.bem`
- `mne.commands`
- `mne.datasets`
- `mne.io`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path, fun
```

## Step-by-Step Guide

### Step 1: 'Test mne compute_proj_ecg/eog.'

```python
'Test mne compute_proj_ecg/eog.'
```

**Verification:**
```python
assert len(fnames) == 1
```

### Step 2: Call check_usage()

```python
check_usage(fun)
```

**Verification:**
```python
assert len(fnames) == 1
```

### Step 3: Assign tempdir = str(...)

```python
tempdir = str(tmp_path)
```

### Step 4: Assign use_fname = op.join(...)

```python
use_fname = op.join(tempdir, op.basename(raw_fname))
```

### Step 5: Assign bad_fname = op.join(...)

```python
bad_fname = op.join(tempdir, 'bads.txt')
```

### Step 6: Call shutil.copyfile()

```python
shutil.copyfile(raw_fname, use_fname)
```

### Step 7: Assign fnames = glob.glob(...)

```python
fnames = glob.glob(op.join(tempdir, '*proj.fif'))
```

**Verification:**
```python
assert len(fnames) == 1
```

### Step 8: Assign fnames = glob.glob(...)

```python
fnames = glob.glob(op.join(tempdir, '*-eve.fif'))
```

**Verification:**
```python
assert len(fnames) == 1
```

### Step 9: Call fid.write()

```python
fid.write('MEG 2443\n')
```

### Step 10: Call fun.run()

```python
fun.run()
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, fun

# Workflow
'Test mne compute_proj_ecg/eog.'
check_usage(fun)
tempdir = str(tmp_path)
use_fname = op.join(tempdir, op.basename(raw_fname))
bad_fname = op.join(tempdir, 'bads.txt')
with open(bad_fname, 'w') as fid:
    fid.write('MEG 2443\n')
shutil.copyfile(raw_fname, use_fname)
with ArgvSetter(('-i', use_fname, '--bad=' + bad_fname, '--rej-eeg', '150')):
    with _record_warnings():
        fun.run()
fnames = glob.glob(op.join(tempdir, '*proj.fif'))
assert len(fnames) == 1
fnames = glob.glob(op.join(tempdir, '*-eve.fif'))
assert len(fnames) == 1
```

## Next Steps


---

*Source: test_commands.py:145 | Complexity: Advanced | Last updated: 2026-05-18*