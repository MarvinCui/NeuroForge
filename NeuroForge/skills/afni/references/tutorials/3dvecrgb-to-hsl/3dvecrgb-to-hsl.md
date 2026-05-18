# How To: 3Dvecrgb To Hsl

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 3dVecRGB to HSL

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
opref = data.outdir / 'o.3dVecRGB_to_HSL'
```

### Step 2: Assign cmd = value

```python
cmd = f'\n    3dVecRGB_to_HSL\n        -echo_edu\n        -in_vec {data.DT_V1}\n        -in_scal {data.DT_FA}\n        -mask {data.mask_DWI}\n        -prefix {opref}\n    '
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
opref = data.outdir / 'o.3dVecRGB_to_HSL'
cmd = f'\n    3dVecRGB_to_HSL\n        -echo_edu\n        -in_vec {data.DT_V1}\n        -in_scal {data.DT_FA}\n        -mask {data.mask_DWI}\n        -prefix {opref}\n    '
cmd = ' '.join(cmd.split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_ptaylor.py:179 | Complexity: Intermediate | Last updated: 2026-05-18*