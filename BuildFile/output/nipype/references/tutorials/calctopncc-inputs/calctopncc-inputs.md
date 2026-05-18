# How To: Calctopncc Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test CalcTopNCC inputs

## Prerequisites

**Required Modules:**
- `label_fusion`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-target %s', extensions=None, mandatory=True, position=1), in_templates=dict(argstr='%s', mandatory=True, position=3), mask_file=dict(argstr='-mask %s', extensions=None), num_templates=dict(argstr='-templates %s', mandatory=True, position=2), top_templates=dict(argstr='-n %s', mandatory=True, position=4))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-target %s', extensions=None, mandatory=True, position=1), in_templates=dict(argstr='%s', mandatory=True, position=3), mask_file=dict(argstr='-mask %s', extensions=None), num_templates=dict(argstr='-templates %s', mandatory=True, position=2), top_templates=dict(argstr='-n %s', mandatory=True, position=4))
```

## Next Steps


---

*Source: test_auto_CalcTopNCC.py:6 | Complexity: Beginner | Last updated: 2026-05-18*