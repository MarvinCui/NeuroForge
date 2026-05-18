# How To: Bet Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test BET inputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), center=dict(argstr='-c %s', units='voxels'), environ=dict(nohash=True, usedefault=True), frac=dict(argstr='-f %.2f'), functional=dict(argstr='-F', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=0), mask=dict(argstr='-m'), mesh=dict(argstr='-e'), no_output=dict(argstr='-n'), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=1), outline=dict(argstr='-o'), output_type=dict(), padding=dict(argstr='-Z', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), radius=dict(argstr='-r %d', units='mm'), reduce_bias=dict(argstr='-B', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), remove_eyes=dict(argstr='-S', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), robust=dict(argstr='-R', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), skull=dict(argstr='-s'), surfaces=dict(argstr='-A', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), t2_guided=dict(argstr='-A2 %s', extensions=None, xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), threshold=dict(argstr='-t'), vertical_gradient=dict(argstr='-g %.2f'))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), center=dict(argstr='-c %s', units='voxels'), environ=dict(nohash=True, usedefault=True), frac=dict(argstr='-f %.2f'), functional=dict(argstr='-F', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), in_file=dict(argstr='%s', copyfile=False, extensions=None, mandatory=True, position=0), mask=dict(argstr='-m'), mesh=dict(argstr='-e'), no_output=dict(argstr='-n'), out_file=dict(argstr='%s', extensions=None, genfile=True, hash_files=False, position=1), outline=dict(argstr='-o'), output_type=dict(), padding=dict(argstr='-Z', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), radius=dict(argstr='-r %d', units='mm'), reduce_bias=dict(argstr='-B', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), remove_eyes=dict(argstr='-S', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), robust=dict(argstr='-R', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), skull=dict(argstr='-s'), surfaces=dict(argstr='-A', xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), t2_guided=dict(argstr='-A2 %s', extensions=None, xor=('functional', 'reduce_bias', 'robust', 'padding', 'remove_eyes', 'surfaces', 't2_guided')), threshold=dict(argstr='-t'), vertical_gradient=dict(argstr='-g %.2f'))
```

## Next Steps


---

*Source: test_auto_BET.py:6 | Complexity: Beginner | Last updated: 2026-05-18*