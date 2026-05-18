# How To: Nib Nifti Dx

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: unittest, workflow, integration

## Overview

Workflow: test nib nifti dx

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

### Step 1: Assign clean_hdr = pjoin(...)

```python
clean_hdr = pjoin(DATA_PATH, 'nifti1.hdr')
```

**Verification:**
```python
assert stdout.strip() == f'Header for "{clean_hdr}" is clean'
```

### Step 2: Assign cmd = value

```python
cmd = ['nib-nifti-dx', clean_hdr]
```

**Verification:**
```python
assert stdout == expected
```

### Step 3: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(cmd)
```

**Verification:**
```python
assert stdout.strip() == f'Header for "{clean_hdr}" is clean'
```

### Step 4: Assign dirty_hdr = pjoin(...)

```python
dirty_hdr = pjoin(DATA_PATH, 'analyze.hdr')
```

### Step 5: Assign cmd = value

```python
cmd = ['nib-nifti-dx', dirty_hdr]
```

### Step 6: Assign unknown = run_command(...)

```python
code, stdout, stderr = run_command(cmd)
```

### Step 7: Assign expected = value

```python
expected = f'''Picky header check output for "{dirty_hdr}"\n\npixdim[0] (qfac) should be 1 (default) or -1\nmagic string '' is not valid\nsform_code 11776 not valid'''
```

**Verification:**
```python
assert stdout == expected
```


## Complete Example

```python
# Workflow
clean_hdr = pjoin(DATA_PATH, 'nifti1.hdr')
cmd = ['nib-nifti-dx', clean_hdr]
code, stdout, stderr = run_command(cmd)
assert stdout.strip() == f'Header for "{clean_hdr}" is clean'
dirty_hdr = pjoin(DATA_PATH, 'analyze.hdr')
cmd = ['nib-nifti-dx', dirty_hdr]
code, stdout, stderr = run_command(cmd)
expected = f'''Picky header check output for "{dirty_hdr}"\n\npixdim[0] (qfac) should be 1 (default) or -1\nmagic string '' is not valid\nsform_code 11776 not valid'''
assert stdout == expected
```

## Next Steps


---

*Source: test_scripts.py:218 | Complexity: Intermediate | Last updated: 2026-05-18*