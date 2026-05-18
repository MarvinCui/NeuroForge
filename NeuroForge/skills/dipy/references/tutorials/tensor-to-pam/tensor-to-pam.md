# How To: Tensor To Pam

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test tensor to pam

## Prerequisites

**Required Modules:**
- `pathlib`
- `tempfile`
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.io.image`
- `dipy.io.peaks`
- `dipy.reconst.dti`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Assign unknown = get_fnames(...)

```python
fdata, fbval, fbvec = get_fnames(name='small_25')
```

### Step 2: Assign gtab = gradient_table(...)

```python
gtab = gradient_table(fbval, bvecs=fbvec)
```

### Step 3: Assign unknown = load_nifti(...)

```python
data, affine = load_nifti(fdata)
```

### Step 4: Assign dm = dti.TensorModel(...)

```python
dm = dti.TensorModel(gtab)
```

### Step 5: Assign df = dm.fit(...)

```python
df = dm.fit(data)
```

### Step 6: Assign unknown = np.array(...)

```python
df.evals[0, 0, 0] = np.array([0, 0, 0])
```

### Step 7: Assign sphere = create_unit_sphere(...)

```python
sphere = create_unit_sphere(recursion_level=4)
```

### Step 8: Assign odf = df.odf(...)

```python
odf = df.odf(sphere)
```

### Step 9: Assign fname = 'test_tt.pam5'

```python
fname = 'test_tt.pam5'
```

### Step 10: Assign pam = tensor_to_pam(...)

```python
pam = tensor_to_pam(evals=df.evals, evecs=df.evecs, affine=affine, sphere=sphere, odf=odf, pam_file=Path(tmpdir) / fname)
```

### Step 11: Call npt.assert_()

```python
npt.assert_(Path(Path(tmpdir) / fname).is_file())
```

### Step 12: Call save_pam()

```python
save_pam(Path(tmpdir) / 'test_tt_2.pam5', pam)
```

### Step 13: Assign pam2 = load_pam(...)

```python
pam2 = load_pam(Path(tmpdir) / 'test_tt_2.pam5')
```

### Step 14: Call npt.assert_array_equal()

```python
npt.assert_array_equal(pam.peak_values, pam2.peak_values)
```

### Step 15: Call npt.assert_array_equal()

```python
npt.assert_array_equal(pam.peak_dirs, pam2.peak_dirs)
```

### Step 16: Call npt.assert_array_almost_equal()

```python
npt.assert_array_almost_equal(pam.peak_indices, pam2.peak_indices)
```


## Complete Example

```python
# Workflow
fdata, fbval, fbvec = get_fnames(name='small_25')
gtab = gradient_table(fbval, bvecs=fbvec)
data, affine = load_nifti(fdata)
dm = dti.TensorModel(gtab)
df = dm.fit(data)
df.evals[0, 0, 0] = np.array([0, 0, 0])
sphere = create_unit_sphere(recursion_level=4)
odf = df.odf(sphere)
with TemporaryDirectory() as tmpdir:
    fname = 'test_tt.pam5'
    pam = tensor_to_pam(evals=df.evals, evecs=df.evecs, affine=affine, sphere=sphere, odf=odf, pam_file=Path(tmpdir) / fname)
    npt.assert_(Path(Path(tmpdir) / fname).is_file())
    save_pam(Path(tmpdir) / 'test_tt_2.pam5', pam)
    pam2 = load_pam(Path(tmpdir) / 'test_tt_2.pam5')
    npt.assert_array_equal(pam.peak_values, pam2.peak_values)
    npt.assert_array_equal(pam.peak_dirs, pam2.peak_dirs)
    npt.assert_array_almost_equal(pam.peak_indices, pam2.peak_indices)
    del pam
```

## Next Steps


---

*Source: test_io_peaks.py:190 | Complexity: Advanced | Last updated: 2026-05-18*