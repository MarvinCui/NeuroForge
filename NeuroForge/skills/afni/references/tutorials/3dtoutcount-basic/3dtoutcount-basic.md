# How To: 3Dtoutcount Basic

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test 3dToutcount basic

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
outfile = data.outdir / 'outcount_1D'
```

### Step 2: Assign cmd = '\n    3dToutcount\n        -automask\n        -fraction\n        -polort 3\n        -legendre {data.epi}\n    '

```python
cmd = '\n    3dToutcount\n        -automask\n        -fraction\n        -polort 3\n        -legendre {data.epi}\n    '
```

### Step 3: Assign cmd = unknown.join(...)

```python
cmd = ' '.join(cmd.format(**locals()).split())
```

### Step 4: Assign differ = tools.OutputDiffer(...)

```python
differ = tools.OutputDiffer(data, cmd, kwargs_log={'append_to_ignored': ['3dToutcount: AFNI version=']})
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
outfile = data.outdir / 'outcount_1D'
cmd = '\n    3dToutcount\n        -automask\n        -fraction\n        -polort 3\n        -legendre {data.epi}\n    '
cmd = ' '.join(cmd.format(**locals()).split())
differ = tools.OutputDiffer(data, cmd, kwargs_log={'append_to_ignored': ['3dToutcount: AFNI version=']})
differ.run()
```

## Next Steps


---

*Source: test_3dToutcount.py:7 | Complexity: Intermediate | Last updated: 2026-05-18*