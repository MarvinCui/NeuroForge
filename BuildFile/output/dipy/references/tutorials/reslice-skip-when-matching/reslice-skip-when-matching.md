# How To: Reslice Skip When Matching

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test ResliceFlow skips reslicing when voxel size already matches.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `logging`
- `pathlib`
- `tempfile`
- `nibabel`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.align.tests.test_imwarp`
- `dipy.align.tests.test_parzenhist`
- `dipy.align.transforms`
- `dipy.data`
- `dipy.io.image`
- `dipy.io.stateful_tractogram`
- `dipy.io.streamline`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`
- `dipy.utils.optpkg`
- `dipy.workflows.align`
- `logging`

**Setup Required:**
```python
# Fixtures: caplog
```

## Step-by-Step Guide

### Step 1: 'Test ResliceFlow skips reslicing when voxel size already matches.'

```python
'Test ResliceFlow skips reslicing when voxel size already matches.'
```

**Verification:**
```python
assert any(('Skipping reslicing' in record.message for record in info_records)), f'Expected INFO message about skipping. Found: {[r.message for r in info_records]}'
```

### Step 2: Assign unknown = get_fnames(...)

```python
data_path, _, _ = get_fnames(name='small_25')
```

**Verification:**
```python
assert any(('already matches target' in record.message for record in info_records)), 'Expected INFO message about matching voxel size'
```

### Step 3: Assign volume = load_nifti_data(...)

```python
volume = load_nifti_data(data_path)
```

### Step 4: Assign unknown = load_nifti(...)

```python
_, _, zooms = load_nifti(data_path, return_voxsize=True)
```

### Step 5: Assign info_records = value

```python
info_records = [r for r in caplog.records if r.levelname == 'INFO']
```

**Verification:**
```python
assert any(('Skipping reslicing' in record.message for record in info_records)), f'Expected INFO message about skipping. Found: {[r.message for r in info_records]}'
```

### Step 6: Assign out_path = value

```python
out_path = reslice_flow.last_generated_outputs['out_resliced']
```

### Step 7: Assign resliced = load_nifti_data(...)

```python
resliced = load_nifti_data(out_path)
```

### Step 8: Call npt.assert_equal()

```python
npt.assert_equal(resliced.shape, volume.shape)
```

### Step 9: Assign reslice_flow = ResliceFlow(...)

```python
reslice_flow = ResliceFlow()
```

### Step 10: Call reslice_flow.run()

```python
reslice_flow.run(data_path, new_vox_size=list(zooms[:3]), out_dir=out_dir)
```


## Complete Example

```python
# Setup
# Fixtures: caplog

# Workflow
'Test ResliceFlow skips reslicing when voxel size already matches.'
import logging
with TemporaryDirectory() as out_dir:
    data_path, _, _ = get_fnames(name='small_25')
    volume = load_nifti_data(data_path)
    _, _, zooms = load_nifti(data_path, return_voxsize=True)
    with caplog.at_level(logging.INFO, logger='dipy'):
        reslice_flow = ResliceFlow()
        reslice_flow.run(data_path, new_vox_size=list(zooms[:3]), out_dir=out_dir)
    info_records = [r for r in caplog.records if r.levelname == 'INFO']
    assert any(('Skipping reslicing' in record.message for record in info_records)), f'Expected INFO message about skipping. Found: {[r.message for r in info_records]}'
    assert any(('already matches target' in record.message for record in info_records)), 'Expected INFO message about matching voxel size'
    out_path = reslice_flow.last_generated_outputs['out_resliced']
    resliced = load_nifti_data(out_path)
    npt.assert_equal(resliced.shape, volume.shape)
```

## Next Steps


---

*Source: test_align.py:99 | Complexity: Advanced | Last updated: 2026-05-18*