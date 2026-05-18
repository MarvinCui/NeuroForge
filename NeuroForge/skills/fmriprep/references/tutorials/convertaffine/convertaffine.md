# How To: Convertaffine

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test ConvertAffine

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `nitransforms`
- `numpy`
- `nibabel.tmpdirs`
- `fmriprep.interfaces`

**Setup Required:**
```python
# Fixtures: tmp_path, data_dir
```

## Step-by-Step Guide

### Step 1: Assign bold = value

```python
bold = data_dir / 'sub-pixar008_task-pixar_desc-coreg_boldref.nii.gz'
```

**Verification:**
```python
assert lta_to_fsl.outputs.out_xfm == str(tmp_path / 'mri_coreg_fwd.mat')
```

### Step 2: Assign anat = value

```python
anat = data_dir / 'sub-pixar008_desc-preproc_T1w.nii.gz'
```

**Verification:**
```python
assert not lta_to_fsl.outputs.out_inv
```

### Step 3: Assign lta_convert_fsl = nt.linear.load(...)

```python
lta_convert_fsl = nt.linear.load(data_dir / 'mri_coreg-lta_convert.mat', moving=bold, reference=anat, fmt='fsl')
```

**Verification:**
```python
assert np.allclose(nitransforms_fsl.matrix, lta_convert_fsl.matrix, atol=0.0001)
```

### Step 4: Assign lta_convert_itk = nt.linear.load(...)

```python
lta_convert_itk = nt.linear.load(data_dir / 'mri_coreg-lta_convert.txt')
```

**Verification:**
```python
assert lta_to_itk.outputs.out_xfm == str(tmp_path / 'mri_coreg_fwd.txt')
```

### Step 5: Assign c3d_itk = nt.linear.load(...)

```python
c3d_itk = nt.linear.load(data_dir / 'mri_coreg-c3d.txt')
```

**Verification:**
```python
assert lta_to_itk.outputs.out_inv == str(tmp_path / 'mri_coreg_inv.txt')
```

### Step 6: Assign lta_convert_itk_inv = nt.linear.load(...)

```python
lta_convert_itk_inv = nt.linear.load(data_dir / 'mri_coreg-lta_convert-invert.txt')
```

**Verification:**
```python
assert np.allclose(nitransforms_itk.matrix, lta_convert_itk.matrix, atol=0.0001)
```

### Step 7: Assign c3d_itk_inv = nt.linear.load(...)

```python
c3d_itk_inv = nt.linear.load(data_dir / 'mri_coreg-c3d-invert.txt')
```

**Verification:**
```python
assert np.allclose(nitransforms_itk.matrix, c3d_itk.matrix, atol=0.0001)
```

### Step 8: Assign lta_to_fsl = fin.ConvertAffine.run(...)

```python
lta_to_fsl = fin.ConvertAffine(in_xfm=data_dir / 'mri_coreg.lta', reference=anat, moving=bold, out_fmt='fsl').run()
```

**Verification:**
```python
assert np.allclose(nitransforms_itk_inv.matrix, lta_convert_itk_inv.matrix, atol=0.0001)
```

### Step 9: Assign nitransforms_fsl = nt.linear.load(...)

```python
nitransforms_fsl = nt.linear.load(lta_to_fsl.outputs.out_xfm, moving=bold, reference=anat, fmt='fsl')
```

**Verification:**
```python
assert np.allclose(nitransforms_itk_inv.matrix, c3d_itk_inv.matrix, atol=0.0001)
```

### Step 10: Assign lta_to_itk = fin.ConvertAffine.run(...)

```python
lta_to_itk = fin.ConvertAffine(in_xfm=data_dir / 'mri_coreg.lta', inverse=True).run()
```

**Verification:**
```python
assert np.allclose(nitransforms_itk.matrix, lta_convert_itk.matrix, atol=0.0001)
```

### Step 11: Assign nitransforms_itk = nt.linear.load(...)

```python
nitransforms_itk = nt.linear.load(lta_to_itk.outputs.out_xfm)
```

**Verification:**
```python
assert np.allclose(nitransforms_itk.matrix, c3d_itk.matrix, atol=0.0001)
```

### Step 12: Assign nitransforms_itk_inv = nt.linear.load(...)

```python
nitransforms_itk_inv = nt.linear.load(lta_to_itk.outputs.out_inv)
```

**Verification:**
```python
assert np.allclose(nitransforms_itk_inv.matrix, lta_convert_itk_inv.matrix, atol=0.0001)
```

### Step 13: Assign fsl_to_itk = fin.ConvertAffine.run(...)

```python
fsl_to_itk = fin.ConvertAffine(in_xfm=data_dir / 'mri_coreg-lta_convert.mat', reference=anat, moving=bold, out_fmt='itk', inverse=True).run()
```

**Verification:**
```python
assert np.allclose(nitransforms_itk_inv.matrix, c3d_itk_inv.matrix, atol=0.0001)
```

### Step 14: Assign nitransforms_itk = nt.linear.load(...)

```python
nitransforms_itk = nt.linear.load(fsl_to_itk.outputs.out_xfm)
```

**Verification:**
```python
assert np.allclose(nitransforms_itk.matrix, lta_convert_itk.matrix, atol=0.0001)
```

### Step 15: Assign nitransforms_itk_inv = nt.linear.load(...)

```python
nitransforms_itk_inv = nt.linear.load(fsl_to_itk.outputs.out_inv)
```

**Verification:**
```python
assert np.allclose(nitransforms_itk_inv.matrix, lta_convert_itk_inv.matrix, atol=0.0001)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path, data_dir

# Workflow
bold = data_dir / 'sub-pixar008_task-pixar_desc-coreg_boldref.nii.gz'
anat = data_dir / 'sub-pixar008_desc-preproc_T1w.nii.gz'
lta_convert_fsl = nt.linear.load(data_dir / 'mri_coreg-lta_convert.mat', moving=bold, reference=anat, fmt='fsl')
lta_convert_itk = nt.linear.load(data_dir / 'mri_coreg-lta_convert.txt')
c3d_itk = nt.linear.load(data_dir / 'mri_coreg-c3d.txt')
lta_convert_itk_inv = nt.linear.load(data_dir / 'mri_coreg-lta_convert-invert.txt')
c3d_itk_inv = nt.linear.load(data_dir / 'mri_coreg-c3d-invert.txt')
with InGivenDirectory(tmp_path):
    lta_to_fsl = fin.ConvertAffine(in_xfm=data_dir / 'mri_coreg.lta', reference=anat, moving=bold, out_fmt='fsl').run()
    assert lta_to_fsl.outputs.out_xfm == str(tmp_path / 'mri_coreg_fwd.mat')
    assert not lta_to_fsl.outputs.out_inv
    nitransforms_fsl = nt.linear.load(lta_to_fsl.outputs.out_xfm, moving=bold, reference=anat, fmt='fsl')
    assert np.allclose(nitransforms_fsl.matrix, lta_convert_fsl.matrix, atol=0.0001)
    lta_to_itk = fin.ConvertAffine(in_xfm=data_dir / 'mri_coreg.lta', inverse=True).run()
    assert lta_to_itk.outputs.out_xfm == str(tmp_path / 'mri_coreg_fwd.txt')
    assert lta_to_itk.outputs.out_inv == str(tmp_path / 'mri_coreg_inv.txt')
    nitransforms_itk = nt.linear.load(lta_to_itk.outputs.out_xfm)
    assert np.allclose(nitransforms_itk.matrix, lta_convert_itk.matrix, atol=0.0001)
    assert np.allclose(nitransforms_itk.matrix, c3d_itk.matrix, atol=0.0001)
    nitransforms_itk_inv = nt.linear.load(lta_to_itk.outputs.out_inv)
    assert np.allclose(nitransforms_itk_inv.matrix, lta_convert_itk_inv.matrix, atol=0.0001)
    assert np.allclose(nitransforms_itk_inv.matrix, c3d_itk_inv.matrix, atol=0.0001)
    fsl_to_itk = fin.ConvertAffine(in_xfm=data_dir / 'mri_coreg-lta_convert.mat', reference=anat, moving=bold, out_fmt='itk', inverse=True).run()
    nitransforms_itk = nt.linear.load(fsl_to_itk.outputs.out_xfm)
    assert np.allclose(nitransforms_itk.matrix, lta_convert_itk.matrix, atol=0.0001)
    assert np.allclose(nitransforms_itk.matrix, c3d_itk.matrix, atol=0.0001)
    nitransforms_itk_inv = nt.linear.load(fsl_to_itk.outputs.out_inv)
    assert np.allclose(nitransforms_itk_inv.matrix, lta_convert_itk_inv.matrix, atol=0.0001)
    assert np.allclose(nitransforms_itk_inv.matrix, c3d_itk_inv.matrix, atol=0.0001)
```

## Next Steps


---

*Source: test_nitransforms.py:8 | Complexity: Advanced | Last updated: 2026-05-18*