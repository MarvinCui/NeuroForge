# How To: Lpca Flow

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test lpca flow

## Prerequisites

**Required Modules:**
- `pathlib`
- `tempfile`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.data`
- `dipy.io.image`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.utils.optpkg`
- `dipy.workflows.denoise`


## Step-by-Step Guide

### Step 1: Assign lpca_flow = LPCAFlow(...)

```python
lpca_flow = LPCAFlow()
```

**Verification:**
```python
assert_true(Path(lpca_flow.last_generated_outputs['out_denoised']).is_file())
```

### Step 2: Call lpca_flow.run()

```python
lpca_flow.run(data_path, fbvals, fbvecs, out_dir=out_dir)
```

### Step 3: Call assert_true()

```python
assert_true(Path(lpca_flow.last_generated_outputs['out_denoised']).is_file())
```

### Step 4: Assign unknown = get_fnames(...)

```python
data_path, fbvals, fbvecs = get_fnames()
```


## Complete Example

```python
# Workflow
with TemporaryDirectory() as out_dir:
    data_path, fbvals, fbvecs = get_fnames()
lpca_flow = LPCAFlow()
lpca_flow.run(data_path, fbvals, fbvecs, out_dir=out_dir)
assert_true(Path(lpca_flow.last_generated_outputs['out_denoised']).is_file())
```

## Next Steps


---

*Source: test_denoise.py:67 | Complexity: Intermediate | Last updated: 2026-05-18*