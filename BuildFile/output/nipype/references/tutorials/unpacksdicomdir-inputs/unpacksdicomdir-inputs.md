# How To: Unpacksdicomdir Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test UnpackSDICOMDir inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), config=dict(argstr='-cfg %s', extensions=None, mandatory=True, xor=('run_info', 'config', 'seq_config')), dir_structure=dict(argstr='-%s'), environ=dict(nohash=True, usedefault=True), log_file=dict(argstr='-log %s', extensions=None), no_info_dump=dict(argstr='-noinfodump'), no_unpack_err=dict(argstr='-no-unpackerr'), output_dir=dict(argstr='-targ %s'), run_info=dict(argstr='-run %d %s %s %s', mandatory=True, xor=('run_info', 'config', 'seq_config')), scan_only=dict(argstr='-scanonly %s', extensions=None), seq_config=dict(argstr='-seqcfg %s', extensions=None, mandatory=True, xor=('run_info', 'config', 'seq_config')), source_dir=dict(argstr='-src %s', mandatory=True), spm_zeropad=dict(argstr='-nspmzeropad %d'), subjects_dir=dict())
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), config=dict(argstr='-cfg %s', extensions=None, mandatory=True, xor=('run_info', 'config', 'seq_config')), dir_structure=dict(argstr='-%s'), environ=dict(nohash=True, usedefault=True), log_file=dict(argstr='-log %s', extensions=None), no_info_dump=dict(argstr='-noinfodump'), no_unpack_err=dict(argstr='-no-unpackerr'), output_dir=dict(argstr='-targ %s'), run_info=dict(argstr='-run %d %s %s %s', mandatory=True, xor=('run_info', 'config', 'seq_config')), scan_only=dict(argstr='-scanonly %s', extensions=None), seq_config=dict(argstr='-seqcfg %s', extensions=None, mandatory=True, xor=('run_info', 'config', 'seq_config')), source_dir=dict(argstr='-src %s', mandatory=True), spm_zeropad=dict(argstr='-nspmzeropad %d'), subjects_dir=dict())
```

## Next Steps


---

*Source: test_auto_UnpackSDICOMDir.py:6 | Complexity: Beginner | Last updated: 2026-05-18*