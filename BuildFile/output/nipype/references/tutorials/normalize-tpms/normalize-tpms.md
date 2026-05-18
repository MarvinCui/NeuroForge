# How To: Normalize Tpms

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test normalize tpms

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `nipype.testing`
- `numpy`
- `nibabel`
- `nipype.algorithms.misc`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: Assign in_mask = example_data(...)

```python
in_mask = example_data('tpms_msk.nii.gz')
```

**Verification:**
```python
assert np.all(normdata[mskdata == 0] == 0)
```

### Step 2: Assign mskdata = np.asanyarray(...)

```python
mskdata = np.asanyarray(nb.load(in_mask).dataobj)
```

**Verification:**
```python
assert np.allclose(normdata, mapdata[i])
```

### Step 3: Assign unknown = 1.0

```python
mskdata[mskdata > 0.0] = 1.0
```

**Verification:**
```python
assert np.allclose(sumdata[sumdata > 0.0], 1.0)
```

### Step 4: Assign mapdata = value

```python
mapdata = []
```

### Step 5: Assign in_files = value

```python
in_files = []
```

### Step 6: Assign out_files = value

```python
out_files = []
```

### Step 7: Call normalize_tpms()

```python
normalize_tpms(in_files, in_mask, out_files=out_files)
```

### Step 8: Assign sumdata = np.zeros_like(...)

```python
sumdata = np.zeros_like(mskdata)
```

**Verification:**
```python
assert np.allclose(sumdata[sumdata > 0.0], 1.0)
```

### Step 9: Assign mapname = example_data(...)

```python
mapname = example_data('tpm_%02d.nii.gz' % i)
```

### Step 10: Assign filename = value

```python
filename = tmpdir.join('modtpm_%02d.nii.gz' % i).strpath
```

### Step 11: Call out_files.append()

```python
out_files.append(tmpdir.join('normtpm_%02d.nii.gz' % i).strpath)
```

### Step 12: Assign im = nb.load(...)

```python
im = nb.load(mapname)
```

### Step 13: Assign data = im.get_fdata(...)

```python
data = im.get_fdata()
```

### Step 14: Call mapdata.append()

```python
mapdata.append(data)
```

### Step 15: Call nb.Nifti1Image.to_filename()

```python
nb.Nifti1Image(2.0 * (data * mskdata), im.affine, im.header).to_filename(filename)
```

### Step 16: Call in_files.append()

```python
in_files.append(filename)
```

### Step 17: Assign normdata = nb.load.get_fdata(...)

```python
normdata = nb.load(tstfname).get_fdata()
```

**Verification:**
```python
assert np.all(normdata[mskdata == 0] == 0)
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
in_mask = example_data('tpms_msk.nii.gz')
mskdata = np.asanyarray(nb.load(in_mask).dataobj)
mskdata[mskdata > 0.0] = 1.0
mapdata = []
in_files = []
out_files = []
for i in range(3):
    mapname = example_data('tpm_%02d.nii.gz' % i)
    filename = tmpdir.join('modtpm_%02d.nii.gz' % i).strpath
    out_files.append(tmpdir.join('normtpm_%02d.nii.gz' % i).strpath)
    im = nb.load(mapname)
    data = im.get_fdata()
    mapdata.append(data)
    nb.Nifti1Image(2.0 * (data * mskdata), im.affine, im.header).to_filename(filename)
    in_files.append(filename)
normalize_tpms(in_files, in_mask, out_files=out_files)
sumdata = np.zeros_like(mskdata)
for i, tstfname in enumerate(out_files):
    normdata = nb.load(tstfname).get_fdata()
    sumdata += normdata
    assert np.all(normdata[mskdata == 0] == 0)
    assert np.allclose(normdata, mapdata[i])
assert np.allclose(sumdata[sumdata > 0.0], 1.0)
```

## Next Steps


---

*Source: test_normalize_tpms.py:13 | Complexity: Advanced | Last updated: 2026-05-18*