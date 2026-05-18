# How To: Zeropad Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test Zeropad inputs

## Prerequisites

**Required Modules:**
- `utils`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(A=dict(argstr='-A %i', xor=['master']), AP=dict(argstr='-AP %i', xor=['master']), I=dict(argstr='-I %i', xor=['master']), IS=dict(argstr='-IS %i', xor=['master']), L=dict(argstr='-L %i', xor=['master']), P=dict(argstr='-P %i', xor=['master']), R=dict(argstr='-R %i', xor=['master']), RL=dict(argstr='-RL %i', xor=['master']), S=dict(argstr='-S %i', xor=['master']), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), master=dict(argstr='-master %s', extensions=None, xor=['I', 'S', 'A', 'P', 'L', 'R', 'z', 'RL', 'AP', 'IS', 'mm']), mm=dict(argstr='-mm', xor=['master']), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_template='zeropad'), outputtype=dict(), z=dict(argstr='-z %i', xor=['master']))
```


## Complete Example

```python
# Workflow
input_map = dict(A=dict(argstr='-A %i', xor=['master']), AP=dict(argstr='-AP %i', xor=['master']), I=dict(argstr='-I %i', xor=['master']), IS=dict(argstr='-IS %i', xor=['master']), L=dict(argstr='-L %i', xor=['master']), P=dict(argstr='-P %i', xor=['master']), R=dict(argstr='-R %i', xor=['master']), RL=dict(argstr='-RL %i', xor=['master']), S=dict(argstr='-S %i', xor=['master']), args=dict(argstr='%s'), environ=dict(nohash=True, usedefault=True), in_files=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=-1), master=dict(argstr='-master %s', extensions=None, xor=['I', 'S', 'A', 'P', 'L', 'R', 'z', 'RL', 'AP', 'IS', 'mm']), mm=dict(argstr='-mm', xor=['master']), num_threads=dict(nohash=True, usedefault=True), out_file=dict(argstr='-prefix %s', extensions=None, name_template='zeropad'), outputtype=dict(), z=dict(argstr='-z %i', xor=['master']))
```

## Next Steps


---

*Source: test_auto_Zeropad.py:6 | Complexity: Beginner | Last updated: 2026-05-18*