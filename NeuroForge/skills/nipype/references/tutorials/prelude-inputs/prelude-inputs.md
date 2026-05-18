# How To: Prelude Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test PRELUDE inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), complex_phase_file=dict(argstr='--complex=%s', extensions=None, mandatory=True, xor=['magnitude_file', 'phase_file']), end=dict(argstr='--end=%d'), environ=dict(nohash=True, usedefault=True), label_file=dict(argstr='--labels=%s', extensions=None, hash_files=False), labelprocess2d=dict(argstr='--labelslices'), magnitude_file=dict(argstr='--abs=%s', extensions=None, mandatory=True, xor=['complex_phase_file']), mask_file=dict(argstr='--mask=%s', extensions=None), num_partitions=dict(argstr='--numphasesplit=%d'), output_type=dict(), phase_file=dict(argstr='--phase=%s', extensions=None, mandatory=True, xor=['complex_phase_file']), process2d=dict(argstr='--slices', xor=['labelprocess2d']), process3d=dict(argstr='--force3D', xor=['labelprocess2d', 'process2d']), rawphase_file=dict(argstr='--rawphase=%s', extensions=None, hash_files=False), removeramps=dict(argstr='--removeramps'), savemask_file=dict(argstr='--savemask=%s', extensions=None, hash_files=False), start=dict(argstr='--start=%d'), threshold=dict(argstr='--thresh=%.10f'), unwrapped_phase_file=dict(argstr='--unwrap=%s', extensions=None, genfile=True, hash_files=False))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), complex_phase_file=dict(argstr='--complex=%s', extensions=None, mandatory=True, xor=['magnitude_file', 'phase_file']), end=dict(argstr='--end=%d'), environ=dict(nohash=True, usedefault=True), label_file=dict(argstr='--labels=%s', extensions=None, hash_files=False), labelprocess2d=dict(argstr='--labelslices'), magnitude_file=dict(argstr='--abs=%s', extensions=None, mandatory=True, xor=['complex_phase_file']), mask_file=dict(argstr='--mask=%s', extensions=None), num_partitions=dict(argstr='--numphasesplit=%d'), output_type=dict(), phase_file=dict(argstr='--phase=%s', extensions=None, mandatory=True, xor=['complex_phase_file']), process2d=dict(argstr='--slices', xor=['labelprocess2d']), process3d=dict(argstr='--force3D', xor=['labelprocess2d', 'process2d']), rawphase_file=dict(argstr='--rawphase=%s', extensions=None, hash_files=False), removeramps=dict(argstr='--removeramps'), savemask_file=dict(argstr='--savemask=%s', extensions=None, hash_files=False), start=dict(argstr='--start=%d'), threshold=dict(argstr='--thresh=%.10f'), unwrapped_phase_file=dict(argstr='--unwrap=%s', extensions=None, genfile=True, hash_files=False))
```

## Next Steps


---

*Source: test_auto_PRELUDE.py:6 | Complexity: Beginner | Last updated: 2026-05-18*