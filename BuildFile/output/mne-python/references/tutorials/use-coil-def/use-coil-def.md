# How To: Use Coil Def

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test use_coil_def.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `itertools`
- `pathlib`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne.bem`
- `mne.channels`
- `mne.datasets`
- `mne.dipole`
- `mne.forward`
- `mne.forward._compute_forward`
- `mne.forward._make_forward`
- `mne.forward.tests.test_forward`
- `mne.io`
- `mne.simulation`
- `mne.source_estimate`
- `mne.source_space._source_space`
- `mne.surface`
- `mne.transforms`
- `mne.utils`

**Setup Required:**
```python
# Fixtures: tmp_path
```

## Step-by-Step Guide

### Step 1: 'Test use_coil_def.'

```python
'Test use_coil_def.'
```

### Step 2: Assign info = create_info(...)

```python
info = create_info(1, 1000.0, 'mag')
```

### Step 3: Assign unknown = 9999

```python
info['chs'][0]['coil_type'] = 9999
```

### Step 4: Assign unknown = value

```python
info['chs'][0]['loc'][:] = [0, 0, 0.02, 1, 0, 0, 0, 1, 0, 0, 0, 1]
```

### Step 5: Assign unknown = Transform(...)

```python
info['dev_head_t'] = Transform('meg', 'head')
```

### Step 6: Assign sphere = make_sphere_model(...)

```python
sphere = make_sphere_model((0.0, 0.0, 0.0), 0.01)
```

### Step 7: Assign src = setup_volume_source_space(...)

```python
src = setup_volume_source_space(pos=5, sphere=sphere)
```

### Step 8: Assign trans = Transform(...)

```python
trans = Transform('head', 'mri', None)
```

### Step 9: Assign coil_fname = value

```python
coil_fname = tmp_path / 'coil_def.dat'
```

### Step 10: Call make_forward_solution()

```python
make_forward_solution(info, trans, src, sphere)
```

### Step 11: Call fid.write()

```python
fid.write('# custom cube coil def\n1   9999    2   8  3e-03  0.000e+00     "Test"\n  0.1250 -0.750e-03 -0.750e-03 -0.750e-03  0.000  0.000')
```

### Step 12: Call fid.write()

```python
fid.write('# custom cube coil def\n1   9999    2   8  3e-03  0.000e+00     "Test"\n  0.1250 -0.750e-03 -0.750e-03 -0.750e-03  0.000  0.000  1.000\n  0.1250 -0.750e-03  0.750e-03 -0.750e-03  0.000  0.000  1.000\n  0.1250  0.750e-03 -0.750e-03 -0.750e-03  0.000  0.000  1.000\n  0.1250  0.750e-03  0.750e-03 -0.750e-03  0.000  0.000  1.000\n  0.1250 -0.750e-03 -0.750e-03  0.750e-03  0.000  0.000  1.000\n  0.1250 -0.750e-03  0.750e-03  0.750e-03  0.000  0.000  1.000\n  0.1250  0.750e-03 -0.750e-03  0.750e-03  0.000  0.000  1.000\n  0.1250  0.750e-03  0.750e-03  0.750e-03  0.000  0.000  1.000')
```

### Step 13: Call make_forward_solution()

```python
make_forward_solution(info, trans, src, sphere)
```

### Step 14: Call make_forward_solution()

```python
make_forward_solution(info, trans, src, sphere)
```


## Complete Example

```python
# Setup
# Fixtures: tmp_path

# Workflow
'Test use_coil_def.'
info = create_info(1, 1000.0, 'mag')
info['chs'][0]['coil_type'] = 9999
info['chs'][0]['loc'][:] = [0, 0, 0.02, 1, 0, 0, 0, 1, 0, 0, 0, 1]
info['dev_head_t'] = Transform('meg', 'head')
sphere = make_sphere_model((0.0, 0.0, 0.0), 0.01)
src = setup_volume_source_space(pos=5, sphere=sphere)
trans = Transform('head', 'mri', None)
with pytest.raises(RuntimeError, match='coil definition not found'):
    make_forward_solution(info, trans, src, sphere)
coil_fname = tmp_path / 'coil_def.dat'
with open(coil_fname, 'w') as fid:
    fid.write('# custom cube coil def\n1   9999    2   8  3e-03  0.000e+00     "Test"\n  0.1250 -0.750e-03 -0.750e-03 -0.750e-03  0.000  0.000')
with pytest.raises(RuntimeError, match='Could not interpret'):
    with use_coil_def(coil_fname):
        make_forward_solution(info, trans, src, sphere)
with open(coil_fname, 'w') as fid:
    fid.write('# custom cube coil def\n1   9999    2   8  3e-03  0.000e+00     "Test"\n  0.1250 -0.750e-03 -0.750e-03 -0.750e-03  0.000  0.000  1.000\n  0.1250 -0.750e-03  0.750e-03 -0.750e-03  0.000  0.000  1.000\n  0.1250  0.750e-03 -0.750e-03 -0.750e-03  0.000  0.000  1.000\n  0.1250  0.750e-03  0.750e-03 -0.750e-03  0.000  0.000  1.000\n  0.1250 -0.750e-03 -0.750e-03  0.750e-03  0.000  0.000  1.000\n  0.1250 -0.750e-03  0.750e-03  0.750e-03  0.000  0.000  1.000\n  0.1250  0.750e-03 -0.750e-03  0.750e-03  0.000  0.000  1.000\n  0.1250  0.750e-03  0.750e-03  0.750e-03  0.000  0.000  1.000')
with use_coil_def(coil_fname):
    make_forward_solution(info, trans, src, sphere)
```

## Next Steps


---

*Source: test_make_forward.py:849 | Complexity: Advanced | Last updated: 2026-05-18*