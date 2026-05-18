# How To: Nib Ls Multiple

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test nib ls multiple

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

### Step 1: Assign fnames = value

```python
fnames = [pjoin(DATA_PATH, f) for f in ('example4d.nii.gz', 'example_nifti2.nii.gz', 'small.mnc', 'nifti2.hdr')]
```

**Verification:**
```python
assert len(stdout_lines) == 4
```

### Step 2: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(['nib-ls'] + fnames)
```

**Verification:**
```python
assert [l[ln:ln + len(i_str)] for l in stdout_lines] == [i_str] * 4, f"Type sub-string didn't start with '{i_str}'. Full output was: {stdout_lines}"
```

### Step 3: Assign stdout_lines = stdout.split(...)

```python
stdout_lines = stdout.split('\n')
```

**Verification:**
```python
assert [l[l.index('['):] for l in stdout_lines] == ['[128,  96,  24,   2] 2.00x2.00x2.20x2000.00  #exts: 2 sform', '[ 32,  20,  12,   2] 2.00x2.00x2.20x2000.00  #exts: 2 sform', '[ 18,  28,  29]      9.00x8.00x7.00', '[ 91, 109,  91]      2.00x2.00x2.00']
```

### Step 4: Assign ln = max(...)

```python
ln = max((len(f) for f in fnames))
```

**Verification:**
```python
assert len(stdout_lines) == 4
```

### Step 5: Assign i_str = value

```python
i_str = ' i' if sys.byteorder == 'little' else ' <i'
```

**Verification:**
```python
assert [l[l.index('['):] for l in stdout_lines] == ['[128,  96,  24,   2] 2.00x2.00x2.20x2000.00  #exts: 2 sform [229725] [2, 1.2e+03]', '[ 32,  20,  12,   2] 2.00x2.00x2.20x2000.00  #exts: 2 sform [15360]  [46, 7.6e+02]', '[ 18,  28,  29]      9.00x8.00x7.00                         [14616]  [0.12, 93]', '[ 91, 109,  91]      2.00x2.00x2.00                          !error']
```

### Step 6: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(['nib-ls', '-s'] + fnames)
```

### Step 7: Assign stdout_lines = stdout.split(...)

```python
stdout_lines = stdout.split('\n')
```

**Verification:**
```python
assert len(stdout_lines) == 4
```


## Complete Example

```python
# Workflow
fnames = [pjoin(DATA_PATH, f) for f in ('example4d.nii.gz', 'example_nifti2.nii.gz', 'small.mnc', 'nifti2.hdr')]
code, stdout, stderr = run_command(['nib-ls'] + fnames)
stdout_lines = stdout.split('\n')
assert len(stdout_lines) == 4
ln = max((len(f) for f in fnames))
i_str = ' i' if sys.byteorder == 'little' else ' <i'
assert [l[ln:ln + len(i_str)] for l in stdout_lines] == [i_str] * 4, f"Type sub-string didn't start with '{i_str}'. Full output was: {stdout_lines}"
assert [l[l.index('['):] for l in stdout_lines] == ['[128,  96,  24,   2] 2.00x2.00x2.20x2000.00  #exts: 2 sform', '[ 32,  20,  12,   2] 2.00x2.00x2.20x2000.00  #exts: 2 sform', '[ 18,  28,  29]      9.00x8.00x7.00', '[ 91, 109,  91]      2.00x2.00x2.00']
code, stdout, stderr = run_command(['nib-ls', '-s'] + fnames)
stdout_lines = stdout.split('\n')
assert len(stdout_lines) == 4
assert [l[l.index('['):] for l in stdout_lines] == ['[128,  96,  24,   2] 2.00x2.00x2.20x2000.00  #exts: 2 sform [229725] [2, 1.2e+03]', '[ 32,  20,  12,   2] 2.00x2.00x2.20x2000.00  #exts: 2 sform [15360]  [46, 7.6e+02]', '[ 18,  28,  29]      9.00x8.00x7.00                         [14616]  [0.12, 93]', '[ 91, 109,  91]      2.00x2.00x2.00                          !error']
```

## Next Steps


---

*Source: test_scripts.py:156 | Complexity: Intermediate | Last updated: 2026-05-18*