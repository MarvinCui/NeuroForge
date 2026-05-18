# How To: Picopdfs Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test PicoPDFs inputs

## Prerequisites

**Required Modules:**
- `dti`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), directmap=dict(argstr='-directmap'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='< %s', extensions=None, mandatory=True, position=1), inputmodel=dict(argstr='-inputmodel %s', position=2, usedefault=True), luts=dict(argstr='-luts %s', mandatory=True), maxcomponents=dict(argstr='-maxcomponents %d', units='NA'), numpds=dict(argstr='-numpds %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), pdf=dict(argstr='-pdf %s', position=4, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), directmap=dict(argstr='-directmap'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='< %s', extensions=None, mandatory=True, position=1), inputmodel=dict(argstr='-inputmodel %s', position=2, usedefault=True), luts=dict(argstr='-luts %s', mandatory=True), maxcomponents=dict(argstr='-maxcomponents %d', units='NA'), numpds=dict(argstr='-numpds %d', units='NA'), out_file=dict(argstr='> %s', extensions=None, genfile=True, position=-1), pdf=dict(argstr='-pdf %s', position=4, usedefault=True))
```

## Next Steps


---

*Source: test_auto_PicoPDFs.py:6 | Complexity: Beginner | Last updated: 2026-05-18*