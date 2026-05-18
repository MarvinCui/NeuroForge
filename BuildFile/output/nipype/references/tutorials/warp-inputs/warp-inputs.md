# How To: Warp Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Warp inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), deoblique=dict(argstr='-deoblique'), environ=dict(nohash=True, usedefault=True), gridset=dict(argstr='-gridset %s', extensions=None), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), interp=dict(argstr='-%s'), matparent=dict(argstr='-matparent %s', extensions=None), mni2tta=dict(argstr='-mni2tta'), newgrid=dict(argstr='-newgrid %f'), num_threads=dict(nohash=True, usedefault=True), oblique_parent=dict(argstr='-oblique_parent %s', extensions=None), out_file=dict(argstr='-prefix %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_warp'), outputtype=dict(), save_warp=dict(requires=['verbose']), tta2mni=dict(argstr='-tta2mni'), verbose=dict(argstr='-verb'), zpad=dict(argstr='-zpad %d'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), deoblique=dict(argstr='-deoblique'), environ=dict(nohash=True, usedefault=True), gridset=dict(argstr='-gridset %s', extensions=None), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), interp=dict(argstr='-%s'), matparent=dict(argstr='-matparent %s', extensions=None), mni2tta=dict(argstr='-mni2tta'), newgrid=dict(argstr='-newgrid %f'), num_threads=dict(nohash=True, usedefault=True), oblique_parent=dict(argstr='-oblique_parent %s', extensions=None), out_file=dict(argstr='-prefix %s', extensions=None, keep_extension=True, name_source='in_file', name_template='%s_warp'), outputtype=dict(), save_warp=dict(requires=['verbose']), tta2mni=dict(argstr='-tta2mni'), verbose=dict(argstr='-verb'), zpad=dict(argstr='-zpad %d'))
```

## Next Steps


---

*Source: test_auto_Warp.py:6 | Complexity: Beginner | Last updated: 2026-05-18*