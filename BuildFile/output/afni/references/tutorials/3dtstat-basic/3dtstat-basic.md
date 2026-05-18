# How To: 3Dtstat Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test 3dTstat basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `afni_test_utils`

**Setup Required:**
```python
# Fixtures: data, statistic
```

## Step-by-Step Guide

### Step 1: Assign outfile = value

```python
outfile = data.outdir / 'stat.nii.gz'
```

### Step 2: Assign cmd = '\n    3dTstat\n        -prefix {outfile}\n        -{statistic}\n        {data.epi}\n    '

```python
cmd = '\n    3dTstat\n        -prefix {outfile}\n        -{statistic}\n        {data.epi}\n    '
```

### Step 3: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 4: Assign kwargs_scans = value

```python
kwargs_scans = {'data_kwargs': {}, 'header_kwargs': {}}
```

### Step 5: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, kwargs_scans=kwargs_scans)
```

### Step 6: Call differ.run()

```python
differ.run(timeout=60)
```


## Complete Example

```python
# Setup
# Fixtures: data, statistic

# Workflow
outfile = data.outdir / 'stat.nii.gz'
cmd = '\n    3dTstat\n        -prefix {outfile}\n        -{statistic}\n        {data.epi}\n    '
cmd = ' '.join(cmd.format(**locals()).split())
kwargs_scans = {'data_kwargs': {}, 'header_kwargs': {}}
differ = tools.OutputDiffer(data, cmd, kwargs_scans=kwargs_scans)
differ.run(timeout=60)
```

## Next Steps


---

*Source: test_3dTstat.py:57 | Complexity: Intermediate | Last updated: 2026-05-18*