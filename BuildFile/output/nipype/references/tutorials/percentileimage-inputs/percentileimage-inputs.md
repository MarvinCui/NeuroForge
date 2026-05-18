# How To: Percentileimage Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test PercentileImage inputs

## Prerequisites

**Required Modules:**
- `maths`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='-%sperc', position=4, usedefault=True), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), internal_datatype=dict(argstr='-dt %s', position=1), nan2zeros=dict(argstr='-nan', position=3), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-2), output_datatype=dict(argstr='-odt %s', position=-1), output_type=dict(), perc=dict(argstr='%f', position=5))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), dimension=dict(argstr='-%sperc', position=4, usedefault=True), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=2), internal_datatype=dict(argstr='-dt %s', position=1), nan2zeros=dict(argstr='-nan', position=3), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-2), output_datatype=dict(argstr='-odt %s', position=-1), output_type=dict(), perc=dict(argstr='%f', position=5))
```

## Next Steps


---

*Source: test_auto_PercentileImage.py:6 | Complexity: Beginner | Last updated: 2026-05-18*