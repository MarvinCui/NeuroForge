# How To: Volume

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test volume

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `nibabel`
- `nibabel.cmdline.stats`
- `nibabel.loadsave`

**Setup Required:**
```python
# Fixtures: tmpdir, capsys
```

## Step-by-Step Guide

### Step 1: Assign mask_data = np.zeros(...)

```python
mask_data = np.zeros((20, 20, 20), dtype='u1')
```

**Verification:**
```python
assert float(vol_mm3[0]) == 1000.0
```

### Step 2: Assign unknown = 1

```python
mask_data[5:15, 5:15, 5:15] = 1
```

**Verification:**
```python
assert int(vol_vox[0]) == 1000
```

### Step 3: Assign img = Nifti1Image(...)

```python
img = Nifti1Image(mask_data, np.eye(4))
```

### Step 4: Assign infile = value

```python
infile = tmpdir / 'input.nii'
```

### Step 5: Call save()

```python
save(img, infile)
```

### Step 6: Assign args = value

```python
args = f'{infile} --Volume'
```

### Step 7: Call main()

```python
main(args.split())
```

### Step 8: Assign vol_mm3 = capsys.readouterr(...)

```python
vol_mm3 = capsys.readouterr()
```

### Step 9: Assign args = value

```python
args = f'{infile} --Volume --units vox'
```

### Step 10: Call main()

```python
main(args.split())
```

### Step 11: Assign vol_vox = capsys.readouterr(...)

```python
vol_vox = capsys.readouterr()
```

**Verification:**
```python
assert float(vol_mm3[0]) == 1000.0
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir, capsys

# Workflow
mask_data = np.zeros((20, 20, 20), dtype='u1')
mask_data[5:15, 5:15, 5:15] = 1
img = Nifti1Image(mask_data, np.eye(4))
infile = tmpdir / 'input.nii'
save(img, infile)
args = f'{infile} --Volume'
main(args.split())
vol_mm3 = capsys.readouterr()
args = f'{infile} --Volume --units vox'
main(args.split())
vol_vox = capsys.readouterr()
assert float(vol_mm3[0]) == 1000.0
assert int(vol_vox[0]) == 1000
```

## Next Steps


---

*Source: test_stats.py:18 | Complexity: Advanced | Last updated: 2026-05-18*