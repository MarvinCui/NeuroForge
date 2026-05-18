# How To: Computemeandiffusivity Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ComputeMeanDiffusivity inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='< %s', extensions=None, mandatory=True, position=1), inputdatatype=dict(argstr='-inputdatatype %s'), inputmodel=dict(argstr='-inputmodel %s'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), outputdatatype=dict(argstr='-outputdatatype %s'), scheme_file=dict(argstr='%s', extensions=None, position=2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='< %s', extensions=None, mandatory=True, position=1), inputdatatype=dict(argstr='-inputdatatype %s'), inputmodel=dict(argstr='-inputmodel %s'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), outputdatatype=dict(argstr='-outputdatatype %s'), scheme_file=dict(argstr='%s', extensions=None, position=2))
```

## Next Steps


---

*Source: test_auto_ComputeMeanDiffusivity.py:6 | Complexity: Beginner | Last updated: 2026-05-18*