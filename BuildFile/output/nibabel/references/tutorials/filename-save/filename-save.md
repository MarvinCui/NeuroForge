# How To: Filename Save

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test filename save

## Prerequisites

**Required Modules:**
- `logging`
- `pathlib`
- `shutil`
- `io`
- `os.path`
- `os.path`
- `tempfile`
- `numpy`
- `pytest`
- `numpy.testing`
- `optpkg`
- `spatialimages`
- `testing`
- `tmpdirs`
- `volumeutils`


## Step-by-Step Guide

### Step 1: Assign inklass_ext_loadklasses = value

```python
inklass_ext_loadklasses = ((Nifti1Image, '.nii', Nifti1Image), (Nifti2Image, '.nii', Nifti2Image), (Nifti1Pair, '.nii', Nifti1Image), (Nifti2Pair, '.nii', Nifti2Image), (Nifti1Image, '.img', Nifti1Pair), (Nifti2Image, '.img', Nifti2Pair), (Nifti1Pair, '.img', Nifti1Pair), (Nifti2Pair, '.img', Nifti2Pair), (Nifti1Image, '.hdr', Nifti1Pair), (Nifti2Image, '.hdr', Nifti2Pair), (Nifti1Pair, '.hdr', Nifti1Pair), (Nifti2Pair, '.hdr', Nifti2Pair), (Minc1Image, '.nii', Nifti1Image), (Minc1Image, '.img', Nifti1Pair), (Spm2AnalyzeImage, '.nii', Nifti1Image), (Spm2AnalyzeImage, '.img', Spm2AnalyzeImage), (Spm99AnalyzeImage, '.nii', Nifti1Image), (Spm99AnalyzeImage, '.img', Spm2AnalyzeImage), (AnalyzeImage, '.nii', Nifti1Image), (AnalyzeImage, '.img', Spm2AnalyzeImage))
```

**Verification:**
```python
assert_array_almost_equal(rt_img.get_fdata(), data)
```

### Step 2: Assign shape = value

```python
shape = (2, 4, 6)
```

**Verification:**
```python
assert type(rt_img) is loadklass
```

### Step 3: Assign affine = np.diag(...)

```python
affine = np.diag([1, 2, 3, 1])
```

### Step 4: Assign data = np.arange.reshape(...)

```python
data = np.arange(np.prod(shape), dtype='f4').reshape(shape)
```

### Step 5: Assign img = inklass(...)

```python
img = inklass(data, affine)
```

### Step 6: Assign pth = mkdtemp(...)

```python
pth = mkdtemp()
```

### Step 7: Assign fname = pjoin(...)

```python
fname = pjoin(pth, 'image' + out_ext)
```

### Step 8: Call shutil.rmtree()

```python
shutil.rmtree(pth)
```

### Step 9: Call nils.save()

```python
nils.save(img, path)
```

### Step 10: Assign rt_img = nils.load(...)

```python
rt_img = nils.load(path)
```

### Step 11: Call assert_array_almost_equal()

```python
assert_array_almost_equal(rt_img.get_fdata(), data)
```

**Verification:**
```python
assert type(rt_img) is loadklass
```


## Complete Example

```python
# Workflow
inklass_ext_loadklasses = ((Nifti1Image, '.nii', Nifti1Image), (Nifti2Image, '.nii', Nifti2Image), (Nifti1Pair, '.nii', Nifti1Image), (Nifti2Pair, '.nii', Nifti2Image), (Nifti1Image, '.img', Nifti1Pair), (Nifti2Image, '.img', Nifti2Pair), (Nifti1Pair, '.img', Nifti1Pair), (Nifti2Pair, '.img', Nifti2Pair), (Nifti1Image, '.hdr', Nifti1Pair), (Nifti2Image, '.hdr', Nifti2Pair), (Nifti1Pair, '.hdr', Nifti1Pair), (Nifti2Pair, '.hdr', Nifti2Pair), (Minc1Image, '.nii', Nifti1Image), (Minc1Image, '.img', Nifti1Pair), (Spm2AnalyzeImage, '.nii', Nifti1Image), (Spm2AnalyzeImage, '.img', Spm2AnalyzeImage), (Spm99AnalyzeImage, '.nii', Nifti1Image), (Spm99AnalyzeImage, '.img', Spm2AnalyzeImage), (AnalyzeImage, '.nii', Nifti1Image), (AnalyzeImage, '.img', Spm2AnalyzeImage))
shape = (2, 4, 6)
affine = np.diag([1, 2, 3, 1])
data = np.arange(np.prod(shape), dtype='f4').reshape(shape)
for inklass, out_ext, loadklass in inklass_ext_loadklasses:
    if not have_scipy:
        if ('mat', '.mat') in loadklass.files_types:
            continue
    img = inklass(data, affine)
    try:
        pth = mkdtemp()
        fname = pjoin(pth, 'image' + out_ext)
        for path in (fname, pathlib.Path(fname)):
            nils.save(img, path)
            rt_img = nils.load(path)
            assert_array_almost_equal(rt_img.get_fdata(), data)
            assert type(rt_img) is loadklass
            del rt_img
    finally:
        shutil.rmtree(pth)
```

## Next Steps


---

*Source: test_image_load_save.py:236 | Complexity: Advanced | Last updated: 2026-05-18*