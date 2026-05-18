# How To: Convertwarp Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test ConvertWarp inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(abswarp=dict(argstr='--abs', xor=['relwarp']), args=dict(argstr='%s'), cons_jacobian=dict(argstr='--constrainj'), environ=dict(nohash=True, usedefault=True), jacobian_max=dict(argstr='--jmax=%f'), jacobian_min=dict(argstr='--jmin=%f'), midmat=dict(argstr='--midmat=%s', extensions=None), out_abswarp=dict(argstr='--absout', xor=['out_relwarp']), out_file=dict(argstr='--out=%s', extensions=None, name_source=['reference'], name_template='%s_concatwarp', output_name='out_file', position=-1), out_relwarp=dict(argstr='--relout', xor=['out_abswarp']), output_type=dict(), postmat=dict(argstr='--postmat=%s', extensions=None), premat=dict(argstr='--premat=%s', extensions=None), reference=dict(argstr='--ref=%s', extensions=None, mandatory=True, position=1), relwarp=dict(argstr='--rel', xor=['abswarp']), shift_direction=dict(argstr='--shiftdir=%s', requires=['shift_in_file']), shift_in_file=dict(argstr='--shiftmap=%s', extensions=None), warp1=dict(argstr='--warp1=%s', extensions=None), warp2=dict(argstr='--warp2=%s', extensions=None))
```


## Complete Example

```python
# Workflow
input_map = dict(abswarp=dict(argstr='--abs', xor=['relwarp']), args=dict(argstr='%s'), cons_jacobian=dict(argstr='--constrainj'), environ=dict(nohash=True, usedefault=True), jacobian_max=dict(argstr='--jmax=%f'), jacobian_min=dict(argstr='--jmin=%f'), midmat=dict(argstr='--midmat=%s', extensions=None), out_abswarp=dict(argstr='--absout', xor=['out_relwarp']), out_file=dict(argstr='--out=%s', extensions=None, name_source=['reference'], name_template='%s_concatwarp', output_name='out_file', position=-1), out_relwarp=dict(argstr='--relout', xor=['out_abswarp']), output_type=dict(), postmat=dict(argstr='--postmat=%s', extensions=None), premat=dict(argstr='--premat=%s', extensions=None), reference=dict(argstr='--ref=%s', extensions=None, mandatory=True, position=1), relwarp=dict(argstr='--rel', xor=['abswarp']), shift_direction=dict(argstr='--shiftdir=%s', requires=['shift_in_file']), shift_in_file=dict(argstr='--shiftmap=%s', extensions=None), warp1=dict(argstr='--warp1=%s', extensions=None), warp2=dict(argstr='--warp2=%s', extensions=None))
```

## Next Steps


---

*Source: test_auto_ConvertWarp.py:6 | Complexity: Beginner | Last updated: 2026-05-18*