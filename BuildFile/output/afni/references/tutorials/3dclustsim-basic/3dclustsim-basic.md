# How To: 3Dclustsim Basic

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 3dClustSim basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `afni_test_utils.misc`
- `afni_test_utils`
- `pytest`

**Setup Required:**
```python
# Fixtures: data, add_env_vars
```

## Step-by-Step Guide

### Step 1: Assign seedval = 31416

```python
seedval = 31416
```

### Step 2: Assign kwargs_log = value

```python
kwargs_log = {'append_to_ignored': ['Clock time', 'but max simulated alpha=']}
```

### Step 3: Assign outfile_prefix = value

```python
outfile_prefix = data.outdir / 'clust_sim_out'
```

### Step 4: Assign cmd = '\n    3dClustSim\n        -nxyz 16 8 4\n        -dxyz 3 3 3\n        -BALL\n        -acf 0.7 3 3\n        -LOTS\n        -seed {seedval}\n        -prefix {outfile_prefix}\n    '

```python
cmd = '\n    3dClustSim\n        -nxyz 16 8 4\n        -dxyz 3 3 3\n        -BALL\n        -acf 0.7 3 3\n        -LOTS\n        -seed {seedval}\n        -prefix {outfile_prefix}\n    '
```

### Step 5: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 6: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, kwargs_1d={'all_close_kwargs': {'rtol': 0.15}}, kwargs_log=kwargs_log, add_env_vars=add_env_vars)
```

### Step 7: Call differ.run()

```python
differ.run(timeout=60)
```


## Complete Example

```python
# Setup
# Fixtures: data, add_env_vars

# Workflow
seedval = 31416
kwargs_log = {'append_to_ignored': ['Clock time', 'but max simulated alpha=']}
outfile_prefix = data.outdir / 'clust_sim_out'
cmd = '\n    3dClustSim\n        -nxyz 16 8 4\n        -dxyz 3 3 3\n        -BALL\n        -acf 0.7 3 3\n        -LOTS\n        -seed {seedval}\n        -prefix {outfile_prefix}\n    '
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd, kwargs_1d={'all_close_kwargs': {'rtol': 0.15}}, kwargs_log=kwargs_log, add_env_vars=add_env_vars)
differ.run(timeout=60)
```

## Next Steps


---

*Source: test_3dClustSim.py:24 | Complexity: Intermediate | Last updated: 2026-05-18*