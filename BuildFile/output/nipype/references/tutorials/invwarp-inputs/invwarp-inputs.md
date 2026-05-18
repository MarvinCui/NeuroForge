# How To: Invwarp Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test InvWarp inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(absolute=dict(argstr='--abs', xor=['relative']), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inverse_warp=dict(argstr='--out=%s', extensions=None, hash_files=False, name_source=['warp'], name_template='%s_inverse'), jacobian_max=dict(argstr='--jmax=%f'), jacobian_min=dict(argstr='--jmin=%f'), niter=dict(argstr='--niter=%d'), noconstraint=dict(argstr='--noconstraint'), output_type=dict(), reference=dict(argstr='--ref=%s', extensions=None, mandatory=True), regularise=dict(argstr='--regularise=%f'), relative=dict(argstr='--rel', xor=['absolute']), warp=dict(argstr='--warp=%s', extensions=None, mandatory=True))
```


## Complete Example

```python
# Workflow
input_map = dict(absolute=dict(argstr='--abs', xor=['relative']), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), inverse_warp=dict(argstr='--out=%s', extensions=None, hash_files=False, name_source=['warp'], name_template='%s_inverse'), jacobian_max=dict(argstr='--jmax=%f'), jacobian_min=dict(argstr='--jmin=%f'), niter=dict(argstr='--niter=%d'), noconstraint=dict(argstr='--noconstraint'), output_type=dict(), reference=dict(argstr='--ref=%s', extensions=None, mandatory=True), regularise=dict(argstr='--regularise=%f'), relative=dict(argstr='--rel', xor=['absolute']), warp=dict(argstr='--warp=%s', extensions=None, mandatory=True))
```

## Next Steps


---

*Source: test_auto_InvWarp.py:6 | Complexity: Beginner | Last updated: 2026-05-18*