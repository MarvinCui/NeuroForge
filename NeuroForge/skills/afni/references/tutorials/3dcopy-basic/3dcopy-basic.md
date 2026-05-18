# How To: 3Dcopy Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 3dcopy basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `afni_test_utils`

**Setup Required:**
```python
# Fixtures: data
```

## Step-by-Step Guide

### Step 1: Assign outfile = value

```python
outfile = data.outdir / 'copied.nii.gz'
```

### Step 2: Assign cmd = '\n    3dcopy {data.anatomical} {outfile}\n    '

```python
cmd = '\n    3dcopy {data.anatomical} {outfile}\n    '
```

### Step 3: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
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
# Fixtures: data

# Workflow
outfile = data.outdir / 'copied.nii.gz'
cmd = '\n    3dcopy {data.anatomical} {outfile}\n    '
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_3dcopy.py:7 | Complexity: Intermediate | Last updated: 2026-05-18*