# How To: Contrastmgr Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ContrastMgr inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), contrast_num=dict(argstr='-cope'), corrections=dict(copyfile=False, extensions=None, mandatory=True), dof_file=dict(argstr='', copyfile=False, extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), fcon_file=dict(argstr='-f %s', extensions=None), output_type=dict(), param_estimates=dict(argstr='', copyfile=False, mandatory=True), sigmasquareds=dict(argstr='', copyfile=False, extensions=None, mandatory=True, position=-2), suffix=dict(argstr='-suffix %s'), tcon_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), contrast_num=dict(argstr='-cope'), corrections=dict(copyfile=False, extensions=None, mandatory=True), dof_file=dict(argstr='', copyfile=False, extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), fcon_file=dict(argstr='-f %s', extensions=None), output_type=dict(), param_estimates=dict(argstr='', copyfile=False, mandatory=True), sigmasquareds=dict(argstr='', copyfile=False, extensions=None, mandatory=True, position=-2), suffix=dict(argstr='-suffix %s'), tcon_file=dict(argstr='%s', extensions=None, mandatory=True, position=-1))
```

## Next Steps


---

*Source: test_auto_ContrastMgr.py:6 | Complexity: Beginner | Last updated: 2026-05-18*