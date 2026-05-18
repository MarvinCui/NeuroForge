# How To: 3Dautomask Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 3dAutomask basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `afni_test_utils`

**Setup Required:**
```python
# Fixtures: data
```

## Step-by-Step Guide

### Step 1: Assign outfile_prefix = value

```python
outfile_prefix = data.outdir / 'masked_image.nii.gz'
```

### Step 2: Assign cmd = '\n    3dAutomask -prefix {outfile_prefix} {data.anat}\n    '

```python
cmd = '\n    3dAutomask -prefix {outfile_prefix} {data.anat}\n    '
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
outfile_prefix = data.outdir / 'masked_image.nii.gz'
cmd = '\n    3dAutomask -prefix {outfile_prefix} {data.anat}\n    '
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd)
differ.run()
```

## Next Steps


---

*Source: test_3dAutomask.py:7 | Complexity: Intermediate | Last updated: 2026-05-18*