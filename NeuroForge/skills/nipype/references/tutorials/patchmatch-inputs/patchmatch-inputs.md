# How To: Patchmatch Inputs

**Difficulty**: Intermediate
**Estimated Time**: 5 minutes
**Tags**: mock

## Overview

Instantiate dict: test PatchMatch inputs

## Prerequisites

**Required Modules:**
- `patchmatch`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), cs_size=dict(argstr='-cs %i'), database_file=dict(argstr='-db %s', extensions=None, mandatory=True, position=3), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), it_num=dict(argstr='-it %i'), mask_file=dict(argstr='-m %s', extensions=None, mandatory=True, position=2), match_num=dict(argstr='-match %i'), out_file=dict(argstr='-o %s', extensions=None, name_source=['in_file'], name_template='%s_pm.nii.gz', position=4), patch_size=dict(argstr='-size %i'), pm_num=dict(argstr='-pm %i'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), cs_size=dict(argstr='-cs %i'), database_file=dict(argstr='-db %s', extensions=None, mandatory=True, position=3), environ=dict(nohash=True, usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=1), it_num=dict(argstr='-it %i'), mask_file=dict(argstr='-m %s', extensions=None, mandatory=True, position=2), match_num=dict(argstr='-match %i'), out_file=dict(argstr='-o %s', extensions=None, name_source=['in_file'], name_template='%s_pm.nii.gz', position=4), patch_size=dict(argstr='-size %i'), pm_num=dict(argstr='-pm %i'))
```

## Next Steps


---

*Source: test_auto_PatchMatch.py:6 | Complexity: Intermediate | Last updated: 2026-05-18*