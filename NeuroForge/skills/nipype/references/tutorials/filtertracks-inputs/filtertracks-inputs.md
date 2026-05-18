# How To: Filtertracks Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test FilterTracks inputs

## Prerequisites

**Required Modules:**
- `tracking`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), debug=dict(argstr='-debug', position=1), environ=dict(nohash=True, usedefault=True), exclude_file=dict(argstr='-exclude %s', extensions=None, xor=['exclude_file', 'exclude_spec']), exclude_spec=dict(argstr='-exclude %s', position=2, sep=',', units='mm', xor=['exclude_file', 'exclude_spec']), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), include_file=dict(argstr='-include %s', extensions=None, xor=['include_file', 'include_spec']), include_spec=dict(argstr='-include %s', position=2, sep=',', units='mm', xor=['include_file', 'include_spec']), invert=dict(argstr='-invert'), minimum_tract_length=dict(argstr='-minlength %s', units='mm'), no_mask_interpolation=dict(argstr='-nomaskinterp'), out_file=dict(argstr='%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s_filt', position=-1), quiet=dict(argstr='-quiet', position=1))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), debug=dict(argstr='-debug', position=1), environ=dict(nohash=True, usedefault=True), exclude_file=dict(argstr='-exclude %s', extensions=None, xor=['exclude_file', 'exclude_spec']), exclude_spec=dict(argstr='-exclude %s', position=2, sep=',', units='mm', xor=['exclude_file', 'exclude_spec']), in_file=dict(argstr='%s', extensions=None, mandatory=True, position=-2), include_file=dict(argstr='-include %s', extensions=None, xor=['include_file', 'include_spec']), include_spec=dict(argstr='-include %s', position=2, sep=',', units='mm', xor=['include_file', 'include_spec']), invert=dict(argstr='-invert'), minimum_tract_length=dict(argstr='-minlength %s', units='mm'), no_mask_interpolation=dict(argstr='-nomaskinterp'), out_file=dict(argstr='%s', extensions=None, hash_files=False, name_source=['in_file'], name_template='%s_filt', position=-1), quiet=dict(argstr='-quiet', position=1))
```

## Next Steps


---

*Source: test_auto_FilterTracks.py:6 | Complexity: Beginner | Last updated: 2026-05-18*