# How To: Smm Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test SMM inputs

## Prerequisites

**Required Modules:**
- `model`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), mask=dict(argstr='--mask="%s"', copyfile=False, extensions=None, mandatory=True, position=1), no_deactivation_class=dict(argstr='--zfstatmode', position=2), output_type=dict(), spatial_data_file=dict(argstr='--sdf="%s"', copyfile=False, extensions=None, mandatory=True, position=0))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), mask=dict(argstr='--mask="%s"', copyfile=False, extensions=None, mandatory=True, position=1), no_deactivation_class=dict(argstr='--zfstatmode', position=2), output_type=dict(), spatial_data_file=dict(argstr='--sdf="%s"', copyfile=False, extensions=None, mandatory=True, position=0))
```

## Next Steps


---

*Source: test_auto_SMM.py:6 | Complexity: Beginner | Last updated: 2026-05-18*