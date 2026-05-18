# How To: 3Ddttonoisydwi

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 3dDTtoNoisyDWI

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `afni_test_utils`
- `pathlib`
- `pytest`
- `sys`

**Setup Required:**
```python
# Fixtures: data, ptaylor_env
```

## Step-by-Step Guide

### Step 1: Assign opref = value

```python
opref = data.outdir / 'o.3dDTtoNoisyDWI'
```

### Step 2: Assign cmd = value

```python
cmd = f'\n    3dDTtoNoisyDWI\n        -echo_edu\n            -grads {data.grad_cvec_n_one}\n        -choose_seed 7\n        -dt_in {data.DT_DT}\n        -mask {data.mask_minisphere_dwi}\n        -noise_DWI 0.05\n        -noise_B0 0\n        -prefix {opref}\n    '
```

### Step 3: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.split())
```

### Step 4: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd)
```

### Step 5: Call differ.run()

```python
differ.run()
```


## Complete Example

```python
# Setup
# Fixtures: data, ptaylor_env

# Workflow
opref = data.outdir / 'o.3dDTtoNoisyDWI'
cmd = f'\n    3dDTtoNoisyDWI\n        -echo_edu\n            -grads {data.grad_cvec_n_one}\n        -choose_seed 7\n        -dt_in {data.DT_DT}\n        -mask {data.mask_minisphere_dwi}\n        -noise_DWI 0.05\n        -noise_B0 0\n        -prefix {opref}\n    '
cmd = ' '.join(cmd.split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_ptaylor.py:139 | Complexity: Intermediate | Last updated: 2026-05-18*