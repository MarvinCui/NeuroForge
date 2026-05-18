# How To: Computeeigensystem Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ComputeEigensystem inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='< %s', extensions=None, mandatory=True, position=1), inputdatatype=dict(argstr='-inputdatatype %s', usedefault=True), inputmodel=dict(argstr='-inputmodel %s'), maxcomponents=dict(argstr='-maxcomponents %d'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), outputdatatype=dict(argstr='-outputdatatype %s', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='< %s', extensions=None, mandatory=True, position=1), inputdatatype=dict(argstr='-inputdatatype %s', usedefault=True), inputmodel=dict(argstr='-inputmodel %s'), maxcomponents=dict(argstr='-maxcomponents %d'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), outputdatatype=dict(argstr='-outputdatatype %s', usedefault=True))
```

## Next Steps


---

*Source: test_auto_ComputeEigensystem.py:6 | Complexity: Beginner | Last updated: 2026-05-18*