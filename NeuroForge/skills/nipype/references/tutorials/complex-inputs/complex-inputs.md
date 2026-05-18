# How To: Complex Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Complex inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), complex_cartesian=dict(argstr='-complex', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), complex_in_file=dict(argstr='%s', extensions=None, position=2), complex_in_file2=dict(argstr='%s', extensions=None, position=3), complex_merge=dict(argstr='-complexmerge', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge', 'start_vol', 'end_vol']), complex_out_file=dict(argstr='%s', extensions=None, genfile=True, position=-3, xor=['complex_out_file', 'magnitude_out_file', 'phase_out_file', 'real_out_file', 'imaginary_out_file', 'real_polar', 'real_cartesian']), complex_polar=dict(argstr='-complexpolar', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), complex_split=dict(argstr='-complexsplit', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), end_vol=dict(argstr='%d', position=-1), environ=dict(nohash=True, usedefault=True), imaginary_in_file=dict(argstr='%s', extensions=None, position=3), imaginary_out_file=dict(argstr='%s', extensions=None, genfile=True, position=-3, xor=['complex_out_file', 'magnitude_out_file', 'phase_out_file', 'real_polar', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), magnitude_in_file=dict(argstr='%s', extensions=None, position=2), magnitude_out_file=dict(argstr='%s', extensions=None, genfile=True, position=-4, xor=['complex_out_file', 'real_out_file', 'imaginary_out_file', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), output_type=dict(), phase_in_file=dict(argstr='%s', extensions=None, position=3), phase_out_file=dict(argstr='%s', extensions=None, genfile=True, position=-3, xor=['complex_out_file', 'real_out_file', 'imaginary_out_file', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), real_cartesian=dict(argstr='-realcartesian', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), real_in_file=dict(argstr='%s', extensions=None, position=2), real_out_file=dict(argstr='%s', extensions=None, genfile=True, position=-4, xor=['complex_out_file', 'magnitude_out_file', 'phase_out_file', 'real_polar', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), real_polar=dict(argstr='-realpolar', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), start_vol=dict(argstr='%d', position=-2))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), complex_cartesian=dict(argstr='-complex', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), complex_in_file=dict(argstr='%s', extensions=None, position=2), complex_in_file2=dict(argstr='%s', extensions=None, position=3), complex_merge=dict(argstr='-complexmerge', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge', 'start_vol', 'end_vol']), complex_out_file=dict(argstr='%s', extensions=None, genfile=True, position=-3, xor=['complex_out_file', 'magnitude_out_file', 'phase_out_file', 'real_out_file', 'imaginary_out_file', 'real_polar', 'real_cartesian']), complex_polar=dict(argstr='-complexpolar', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), complex_split=dict(argstr='-complexsplit', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), end_vol=dict(argstr='%d', position=-1), environ=dict(nohash=True, usedefault=True), imaginary_in_file=dict(argstr='%s', extensions=None, position=3), imaginary_out_file=dict(argstr='%s', extensions=None, genfile=True, position=-3, xor=['complex_out_file', 'magnitude_out_file', 'phase_out_file', 'real_polar', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), magnitude_in_file=dict(argstr='%s', extensions=None, position=2), magnitude_out_file=dict(argstr='%s', extensions=None, genfile=True, position=-4, xor=['complex_out_file', 'real_out_file', 'imaginary_out_file', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), output_type=dict(), phase_in_file=dict(argstr='%s', extensions=None, position=3), phase_out_file=dict(argstr='%s', extensions=None, genfile=True, position=-3, xor=['complex_out_file', 'real_out_file', 'imaginary_out_file', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), real_cartesian=dict(argstr='-realcartesian', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), real_in_file=dict(argstr='%s', extensions=None, position=2), real_out_file=dict(argstr='%s', extensions=None, genfile=True, position=-4, xor=['complex_out_file', 'magnitude_out_file', 'phase_out_file', 'real_polar', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), real_polar=dict(argstr='-realpolar', position=1, xor=['real_polar', 'real_cartesian', 'complex_cartesian', 'complex_polar', 'complex_split', 'complex_merge']), start_vol=dict(argstr='%d', position=-2))
```

## Next Steps


---

*Source: test_auto_Complex.py:6 | Complexity: Beginner | Last updated: 2026-05-18*