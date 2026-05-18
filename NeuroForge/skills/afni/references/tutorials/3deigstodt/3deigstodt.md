# How To: 3Deigstodt

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 3dEigsToDT

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
opref = data.outdir / 'o.3dEigsToDT'
```

### Step 2: Assign cmd = value

```python
cmd = f"\n    3dEigsToDT\n    -echo_edu\n    -eig_vals '{data.tests_data_dir / fatdir2}/DT_L*'\n    -eig_vecs '{data.tests_data_dir / fatdir2}/DT_V*'\n    -prefix {opref}\n    "
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
opref = data.outdir / 'o.3dEigsToDT'
cmd = f"\n    3dEigsToDT\n    -echo_edu\n    -eig_vals '{data.tests_data_dir / fatdir2}/DT_L*'\n    -eig_vecs '{data.tests_data_dir / fatdir2}/DT_V*'\n    -prefix {opref}\n    "
cmd = ' '.join(cmd.split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_ptaylor.py:161 | Complexity: Intermediate | Last updated: 2026-05-18*