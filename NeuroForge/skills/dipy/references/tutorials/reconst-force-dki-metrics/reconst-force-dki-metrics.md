# How To: Reconst Force Dki Metrics

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: DKI metrics are saved when compute_kurtosis=True.

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

### Step 1: 'DKI metrics are saved when compute_kurtosis=True.'

```python
'DKI metrics are saved when compute_kurtosis=True.'
```

**Verification:**
```python
assert os.path.exists(out_path), f'Missing DKI output: {metric}'
```

### Step 2: Assign unknown = get_fnames(...)

```python
data_path, bval_path, bvec_path = get_fnames(name='small_64D')
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

### Step 8: Call _patch_generate()

```python
_patch_generate(monkeypatch, _make_fake_simulations_dki(len(bvals)))
```

### Step 9: Assign flow = ReconstForceFlow(...)

```python
flow = ReconstForceFlow()
```

### Step 10: Call flow.run()

```python
flow.run(str(data_path), str(bval_path), str(bvec_path), str(mask_path), n_neighbors=5, engine='serial', compute_kurtosis=True, out_dir=str(tmp_path))
```

### Step 11: Assign out_path = value

```python
out_path = flow.last_generated_outputs[f'out_{metric}']
```

**Verification:**
```python
assert os.path.exists(out_path), f'Missing DKI output: {metric}'
```

### Step 12: Assign data_arr = load_nifti_data(...)

```python
data_arr = load_nifti_data(out_path)
```

### Step 13: Call npt.assert_equal()

```python
npt.assert_equal(data_arr.shape, volume.shape[:3])
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch, tmp_path

# Workflow
'DKI metrics are saved when compute_kurtosis=True.'
data_path, bval_path, bvec_path = get_fnames(name='small_64D')
volume, affine = load_nifti(data_path)
mask = np.ones(volume.shape[:3], dtype=np.uint8)
mask_path = tmp_path / 'mask.nii.gz'
save_nifti(mask_path, mask, affine)
bvals, _ = read_bvals_bvecs(bval_path, bvec_path)
_patch_generate(monkeypatch, _make_fake_simulations_dki(len(bvals)))
flow = ReconstForceFlow()
flow.run(str(data_path), str(bval_path), str(bvec_path), str(mask_path), n_neighbors=5, engine='serial', compute_kurtosis=True, out_dir=str(tmp_path))
for metric in ['mk', 'ak', 'rk', 'kfa']:
    out_path = flow.last_generated_outputs[f'out_{metric}']
    assert os.path.exists(out_path), f'Missing DKI output: {metric}'
    data_arr = load_nifti_data(out_path)
    npt.assert_equal(data_arr.shape, volume.shape[:3])
```

## Next Steps


---

*Source: test_reconst.py:536 | Complexity: Advanced | Last updated: 2026-05-18*