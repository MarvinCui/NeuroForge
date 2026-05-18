# How To: Susan Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SUSAN inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), brightness_threshold=dict(argstr='%.10f', mandatory=True, position=2), dimension=dict(argstr='%d', position=4, usedefault=True), environ=dict(nohash=True, usedefault=True), fwhm=dict(argstr='%.10f', mandatory=True, position=3), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=1), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-1), output_type=dict(), usans=dict(argstr='', position=6, usedefault=True), use_median=dict(argstr='%d', position=5, usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), brightness_threshold=dict(argstr='%.10f', mandatory=True, position=2), dimension=dict(argstr='%d', position=4, usedefault=True), environ=dict(nohash=True, usedefault=True), fwhm=dict(argstr='%.10f', mandatory=True, position=3), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=1), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=-1), output_type=dict(), usans=dict(argstr='', position=6, usedefault=True), use_median=dict(argstr='%d', position=5, usedefault=True))
```

## Next Steps


---

*Source: test_auto_SUSAN.py:6 | Complexity: Beginner | Last updated: 2026-05-18*