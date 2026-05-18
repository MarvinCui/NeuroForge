# How To: 3Dcalc Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 3dcalc basic

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `afni_test_utils`
- `filecmp`

**Setup Required:**
```python
# Fixtures: data
```

## Step-by-Step Guide

### Step 1: Assign outfile = value

```python
outfile = data.outdir / 'outside_brain.nii.gz'
```

### Step 2: Assign cmd = "\n    3dcalc -a {data.anatomical} -b {data.no_skull} -expr 'a*not(b)' -prefix {outfile}\n    "

```python
cmd = "\n    3dcalc -a {data.anatomical} -b {data.no_skull} -expr 'a*not(b)' -prefix {outfile}\n    "
```

### Step 3: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 4: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, kwargs_log={'append_to_ignored': ['Output dataset']})
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
outfile = data.outdir / 'outside_brain.nii.gz'
cmd = "\n    3dcalc -a {data.anatomical} -b {data.no_skull} -expr 'a*not(b)' -prefix {outfile}\n    "
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd, kwargs_log={'append_to_ignored': ['Output dataset']})
differ.run()
```

## Next Steps


---

*Source: test_3dcalc.py:11 | Complexity: Intermediate | Last updated: 2026-05-18*