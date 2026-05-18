# How To: Splinefilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SplineFilter inputs

## Prerequisites

**Required Modules:**
- `postproc`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), output_file=dict(argstr='%s', extensions=None, position=2, usedefault=True), step_length=dict(argstr='%f', mandatory=True, position=1), track_file=dict(argstr='%s', extensions=None, mandatory=True, position=0))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), output_file=dict(argstr='%s', extensions=None, position=2, usedefault=True), step_length=dict(argstr='%f', mandatory=True, position=1), track_file=dict(argstr='%s', extensions=None, mandatory=True, position=0))
```

## Next Steps


---

*Source: test_auto_SplineFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*