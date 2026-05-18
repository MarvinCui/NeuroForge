# How To: Correct Biasfield Flow

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test correct biasfield flow

## Prerequisites

**Required Modules:**
- `pathlib`
- `tempfile`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.data`
- `dipy.io.image`
- `dipy.nn.evac`
- `dipy.utils.optpkg`
- `dipy.workflows.nn`


## Step-by-Step Guide

### Step 1: Assign args = value

```python
args = {'input_files': fdata, 'bval': fbval, 'bvec': fbvec, 'method': 'random', 'out_dir': out_dir}
```

**Verification:**
```python
assert corrected_data.shape == volume.shape
```

### Step 2: Call npt.assert_raises()

```python
npt.assert_raises(SystemExit, bias_flow.run, **args)
```

### Step 3: Assign unknown = get_fnames(...)

```python
fdata, fbval, fbvec = get_fnames(name='small_25')
```

### Step 4: Assign args = value

```python
args = {'input_files': fdata, 'bval': fbval, 'bvec': fbvec, 'out_dir': out_dir}
```

### Step 5: Assign bias_flow = BiasFieldCorrectionFlow(...)

```python
bias_flow = BiasFieldCorrectionFlow()
```

### Step 6: Call bias_flow.run()

```python
bias_flow.run(**args)
```

### Step 7: Assign corrected_name = value

```python
corrected_name = bias_flow.last_generated_outputs['out_corrected']
```

### Step 8: Assign corrected_data = load_nifti_data(...)

```python
corrected_data = load_nifti_data(Path(out_dir) / corrected_name)
```

### Step 9: Call npt.assert_almost_equal()

```python
npt.assert_almost_equal(corrected_data.mean(), 44.00769230769231, decimal=0)
```

### Step 10: Assign t1_path = get_fnames(...)

```python
t1_path = get_fnames(name='stanford_t1')
```

### Step 11: Assign unknown = load_nifti(...)

```python
volume, affine = load_nifti(t1_path)
```

### Step 12: Assign bias_flow = BiasFieldCorrectionFlow(...)

```python
bias_flow = BiasFieldCorrectionFlow()
```

### Step 13: Call bias_flow.run()

```python
bias_flow.run(t1_path, out_dir=out_dir, method='n4')
```

### Step 14: Assign corrected_name = value

```python
corrected_name = bias_flow.last_generated_outputs['out_corrected']
```

### Step 15: Assign corrected_data = load_nifti_data(...)

```python
corrected_data = load_nifti_data(Path(out_dir) / corrected_name)
```

**Verification:**
```python
assert corrected_data.shape == volume.shape
```


## Complete Example

```python
# Workflow
if have_nn:
    with TemporaryDirectory() as out_dir:
        t1_path = get_fnames(name='stanford_t1')
        volume, affine = load_nifti(t1_path)
        bias_flow = BiasFieldCorrectionFlow()
        bias_flow.run(t1_path, out_dir=out_dir, method='n4')
        corrected_name = bias_flow.last_generated_outputs['out_corrected']
        corrected_data = load_nifti_data(Path(out_dir) / corrected_name)
        assert corrected_data.shape == volume.shape
with TemporaryDirectory() as out_dir:
    fdata, fbval, fbvec = get_fnames(name='small_25')
    args = {'input_files': fdata, 'bval': fbval, 'bvec': fbvec, 'out_dir': out_dir}
    bias_flow = BiasFieldCorrectionFlow()
    bias_flow.run(**args)
    corrected_name = bias_flow.last_generated_outputs['out_corrected']
    corrected_data = load_nifti_data(Path(out_dir) / corrected_name)
    npt.assert_almost_equal(corrected_data.mean(), 44.00769230769231, decimal=0)
args = {'input_files': fdata, 'bval': fbval, 'bvec': fbvec, 'method': 'random', 'out_dir': out_dir}
npt.assert_raises(SystemExit, bias_flow.run, **args)
```

## Next Steps


---

*Source: test_nn.py:48 | Complexity: Advanced | Last updated: 2026-05-18*