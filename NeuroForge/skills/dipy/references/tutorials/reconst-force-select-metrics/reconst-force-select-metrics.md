# How To: Reconst Force Select Metrics

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: mock, workflow, integration

## Overview

Workflow: save_metrics limits which output files are written.

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

### Step 1: 'save_metrics limits which output files are written.'

```python
'save_metrics limits which output files are written.'
```

**Verification:**
```python
assert os.path.exists(flow.last_generated_outputs['out_fa'])
```

### Step 2: Assign unknown = get_fnames(...)

```python
data_path, bval_path, bvec_path = get_fnames(name='small_64D')
```

**Verification:**
```python
assert os.path.exists(flow.last_generated_outputs['out_md'])
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
_patch_generate(monkeypatch, _make_fake_simulations(len(bvals)))
```

### Step 9: Assign flow = ReconstForceFlow(...)

```python
flow = ReconstForceFlow()
```

### Step 10: Call flow.run()

```python
flow.run(str(data_path), str(bval_path), str(bvec_path), str(mask_path), n_neighbors=5, engine='serial', save_metrics=['fa', 'md'], out_dir=str(tmp_path), out_fa='only_fa.nii.gz', out_md='only_md.nii.gz')
```

**Verification:**
```python
assert os.path.exists(flow.last_generated_outputs['out_fa'])
```


## Complete Example

```python
# Setup
# Fixtures: monkeypatch, tmp_path

# Workflow
'save_metrics limits which output files are written.'
data_path, bval_path, bvec_path = get_fnames(name='small_64D')
volume, affine = load_nifti(data_path)
mask = np.ones(volume.shape[:3], dtype=np.uint8)
mask_path = tmp_path / 'mask.nii.gz'
save_nifti(mask_path, mask, affine)
bvals, _ = read_bvals_bvecs(bval_path, bvec_path)
_patch_generate(monkeypatch, _make_fake_simulations(len(bvals)))
flow = ReconstForceFlow()
flow.run(str(data_path), str(bval_path), str(bvec_path), str(mask_path), n_neighbors=5, engine='serial', save_metrics=['fa', 'md'], out_dir=str(tmp_path), out_fa='only_fa.nii.gz', out_md='only_md.nii.gz')
assert os.path.exists(flow.last_generated_outputs['out_fa'])
assert os.path.exists(flow.last_generated_outputs['out_md'])
```

## Next Steps


---

*Source: test_reconst.py:507 | Complexity: Advanced | Last updated: 2026-05-18*