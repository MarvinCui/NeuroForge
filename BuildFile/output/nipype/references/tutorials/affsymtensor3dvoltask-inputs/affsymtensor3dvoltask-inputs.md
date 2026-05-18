# How To: Affsymtensor3Dvoltask Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test affSymTensor3DVolTask inputs

## Prerequisites

**Required Modules:**
- `registration`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), deformation=dict(argstr='-deformation %g %g %g %g %g %g', xor=['transform']), environ=dict(nohash=True, usedefault=True), euler=dict(argstr='-euler %g %g %g', xor=['transform']), in_file=dict(argstr='-in %s', extensions=None, mandatory=True), interpolation=dict(argstr='-interp %s', usedefault=True), out_file=dict(argstr='-out %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_affxfmd'), reorient=dict(argstr='-reorient %s', usedefault=True), target=dict(argstr='-target %s', extensions=None, xor=['transform']), transform=dict(argstr='-trans %s', extensions=None, xor=['target', 'translation', 'euler', 'deformation']), translation=dict(argstr='-translation %g %g %g', xor=['transform']))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), deformation=dict(argstr='-deformation %g %g %g %g %g %g', xor=['transform']), environ=dict(nohash=True, usedefault=True), euler=dict(argstr='-euler %g %g %g', xor=['transform']), in_file=dict(argstr='-in %s', extensions=None, mandatory=True), interpolation=dict(argstr='-interp %s', usedefault=True), out_file=dict(argstr='-out %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_affxfmd'), reorient=dict(argstr='-reorient %s', usedefault=True), target=dict(argstr='-target %s', extensions=None, xor=['transform']), transform=dict(argstr='-trans %s', extensions=None, xor=['target', 'translation', 'euler', 'deformation']), translation=dict(argstr='-translation %g %g %g', xor=['transform']))
```

## Next Steps


---

*Source: test_auto_affSymTensor3DVolTask.py:6 | Complexity: Beginner | Last updated: 2026-05-18*