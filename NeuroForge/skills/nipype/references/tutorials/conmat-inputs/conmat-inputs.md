# How To: Conmat Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Conmat inputs

## Prerequisites

**Required Modules:**
- `connectivity`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True), output_root=dict(argstr='-outputroot %s', extensions=None, genfile=True), scalar_file=dict(argstr='-scalarfile %s', extensions=None, requires=['tract_stat']), target_file=dict(argstr='-targetfile %s', extensions=None, mandatory=True), targetname_file=dict(argstr='-targetnamefile %s', extensions=None), tract_prop=dict(argstr='-tractstat %s', units='NA', xor=['tract_stat']), tract_stat=dict(argstr='-tractstat %s', requires=['scalar_file'], units='NA', xor=['tract_prop']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-inputfile %s', extensions=None, mandatory=True), output_root=dict(argstr='-outputroot %s', extensions=None, genfile=True), scalar_file=dict(argstr='-scalarfile %s', extensions=None, requires=['tract_stat']), target_file=dict(argstr='-targetfile %s', extensions=None, mandatory=True), targetname_file=dict(argstr='-targetnamefile %s', extensions=None), tract_prop=dict(argstr='-tractstat %s', units='NA', xor=['tract_stat']), tract_stat=dict(argstr='-tractstat %s', requires=['scalar_file'], units='NA', xor=['tract_prop']))
```

## Next Steps


---

*Source: test_auto_Conmat.py:6 | Complexity: Beginner | Last updated: 2026-05-18*