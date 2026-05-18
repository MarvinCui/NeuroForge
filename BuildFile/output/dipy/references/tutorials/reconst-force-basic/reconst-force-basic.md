# How To: Reconst Force Basic

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: ReconstForceFlow runs and produces expected output files.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `os`
- `pathlib`
- `tempfile`
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.io.gradients`
- `dipy.io.image`
- `dipy.io.peaks`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.utils.optpkg`
- `dipy.workflows.reconst`

**Setup Required:**
```python
# Fixtures: monkeypatch, tmp_path
```

## Step-by-Step Guide

### Step 1: 'ReconstForceFlow runs and produces expected output files.'

```python
'ReconstForceFlow runs and produces expected output files.'
```

**Verification:**
```python
assert os.path.exists(out_path), f'Missing output: {metric}'
```

### Step 2: Assign unknown = get_fnames(...)

```python
data_path, bval_path, bvec_path = get_fnames(name='small_64D')
```

**Verification:**
```python
assert np.isfinite(data_arr).all(), f'Non-finite values in {metric}'
```

### Step 3: Assign unknown = load_nifti(...)

```python
volume, affine = load_nifti(data_path)
```

### Step 4: Assign mask = np.ones(...)

```python
mask = np.ones(volume.shape[:3], dtype=np.uint8)
```

### Step 5: Assign mask_path = value

```python
mask_path = tmp_path / 'mask.nii.gz'
```

### Step 6: Call save_nifti()

```python
save_nifti(mask_path, mask, affine)
```

### Step 7: Assign unknown = read_bvals_bvecs(...)

```python
bvals, _ = read_bvals_bvecs(bval_path, bvec_path)
```

### Step 8: Assign n_gradients = len(...)

```python
n_gradients = len(bvals)
```

### Step 9: Call _patch_generate()

```python
_patch_generate(monkeypatch, _make_fake_simulations(n_gradients))
```

### Step 10: Assign flow = ReconstForceFlow(...)

```python
flow = ReconstForceFlow()
```

### Step 11: Call flow.run()

```python
flow.run(str(data_path), str(bval_path), str(bvec_path), str(mask_path), n_neighbors=5, engine='serial', out_dir=str(tmp_path))
```

### Step 12: Assign out_path = value

```python
out_path = flow.last_generated_outputs[f'out_{metric}']
```

**Verification:**
```python
assert os.path.exists(out_path), f'Missing output: {metric}'
```

### Step 13: Assign data_arr = load_nifti_data(...)

```python
data_arr = load_nifti_data(out_path)
```

### Step 14: Call npt.assert_equal()

```python
npt.assert_equal(data_arr.shape, volume.shape[:3])
```

**Verification:**
```python
assert np.isfinite(data_arr).all(), f'Non-finite values in {metric}'
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch, tmp_path

# Workflow
'ReconstForceFlow runs and produces expected output files.'
data_path, bval_path, bvec_path = get_fnames(name='small_64D')
volume, affine = load_nifti(data_path)
mask = np.ones(volume.shape[:3], dtype=np.uint8)
mask_path = tmp_path / 'mask.nii.gz'
save_nifti(mask_path, mask, affine)
bvals, _ = read_bvals_bvecs(bval_path, bvec_path)
n_gradients = len(bvals)
_patch_generate(monkeypatch, _make_fake_simulations(n_gradients))
flow = ReconstForceFlow()
flow.run(str(data_path), str(bval_path), str(bvec_path), str(mask_path), n_neighbors=5, engine='serial', out_dir=str(tmp_path))
for metric in ['fa', 'md', 'rd', 'wm_fraction', 'gm_fraction', 'csf_fraction', 'num_fibers', 'dispersion', 'nd', 'uncertainty', 'ambiguity']:
    out_path = flow.last_generated_outputs[f'out_{metric}']
    assert os.path.exists(out_path), f'Missing output: {metric}'
    data_arr = load_nifti_data(out_path)
    npt.assert_equal(data_arr.shape, volume.shape[:3])
    assert np.isfinite(data_arr).all(), f'Non-finite values in {metric}'
```

## Next Steps


---

*Source: test_reconst.py:463 | Complexity: Advanced | Last updated: 2026-05-18*