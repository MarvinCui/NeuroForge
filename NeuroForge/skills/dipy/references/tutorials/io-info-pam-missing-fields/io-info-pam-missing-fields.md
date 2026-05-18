# How To: Io Info Pam Missing Fields

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test io info pam missing fields

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `importlib`
- `inspect`
- `logging`
- `pathlib`
- `shutil`
- `sys`
- `tempfile`
- `numpy`
- `numpy.testing`
- `pytest`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.data.fetcher`
- `dipy.direction.peaks`
- `dipy.io.image`
- `dipy.io.peaks`
- `dipy.io.streamline`
- `dipy.io.utils`
- `dipy.reconst`
- `dipy.reconst.shm`
- `dipy.testing`
- `dipy.utils.optpkg`
- `dipy.utils.tripwire`
- `dipy.workflows.base`
- `dipy.workflows.io`

**Setup Required:**
```python
# Fixtures: caplog
```

## Step-by-Step Guide

### Step 1: Assign pam = PeaksAndMetrics(...)

```python
pam = PeaksAndMetrics()
```

### Step 2: Assign pam.peak_dirs = np.zeros(...)

```python
pam.peak_dirs = np.zeros((5, 5, 5, 3, 3))
```

### Step 3: Assign pam.peak_values = np.zeros(...)

```python
pam.peak_values = np.zeros((5, 5, 5, 3))
```

### Step 4: Assign pam.peak_indices = np.zeros(...)

```python
pam.peak_indices = np.zeros((5, 5, 5, 3))
```

### Step 5: Assign pam.sphere = default_sphere

```python
pam.sphere = default_sphere
```

### Step 6: Assign pam.total_weight = 0.0

```python
pam.total_weight = 0.0
```

### Step 7: Assign pam.ang_thr = 0.0

```python
pam.ang_thr = 0.0
```

### Step 8: Assign pam.affine = None

```python
pam.affine = None
```

### Step 9: Assign pam.shm_coeff = None

```python
pam.shm_coeff = None
```

### Step 10: Assign pam.B = None

```python
pam.B = None
```

### Step 11: Assign pam.gfa = None

```python
pam.gfa = None
```

### Step 12: Assign pam.qa = None

```python
pam.qa = None
```

### Step 13: Assign pam.odf = None

```python
pam.odf = None
```

### Step 14: Assign lines = caplog.text.splitlines(...)

```python
lines = caplog.text.splitlines()
```

### Step 15: Assign pam_fname = value

```python
pam_fname = Path(out_dir) / 'minimal.pam5'
```

### Step 16: Call save_pam()

```python
save_pam(pam_fname, pam)
```

### Step 17: Assign io_info_flow = IoInfoFlow(...)

```python
io_info_flow = IoInfoFlow()
```

### Step 18: Assign matching = value

```python
matching = [line for line in lines if label in line and 'Not available' in line]
```

### Step 19: Call npt.assert_equal()

```python
npt.assert_equal(len(matching) > 0, True)
```

### Step 20: Call io_info_flow.run()

```python
io_info_flow.run(pam_fname)
```


## Complete Example

```python
# Setup
# Fixtures: caplog

# Workflow
pam = PeaksAndMetrics()
pam.peak_dirs = np.zeros((5, 5, 5, 3, 3))
pam.peak_values = np.zeros((5, 5, 5, 3))
pam.peak_indices = np.zeros((5, 5, 5, 3))
pam.sphere = default_sphere
pam.total_weight = 0.0
pam.ang_thr = 0.0
pam.affine = None
pam.shm_coeff = None
pam.B = None
pam.gfa = None
pam.qa = None
pam.odf = None
with TemporaryDirectory() as out_dir:
    pam_fname = Path(out_dir) / 'minimal.pam5'
    save_pam(pam_fname, pam)
    io_info_flow = IoInfoFlow()
    with caplog.at_level(logging.INFO, logger='dipy'):
        io_info_flow.run(pam_fname)
lines = caplog.text.splitlines()
for label in ['Voxel size', 'Voxel order', 'SH coefficients shape', 'SH order', 'B matrix shape', 'GFA shape', 'QA shape', 'ODF shape', 'Affine matrix']:
    matching = [line for line in lines if label in line and 'Not available' in line]
    npt.assert_equal(len(matching) > 0, True)
```

## Next Steps


---

*Source: test_io.py:115 | Complexity: Advanced | Last updated: 2026-05-18*