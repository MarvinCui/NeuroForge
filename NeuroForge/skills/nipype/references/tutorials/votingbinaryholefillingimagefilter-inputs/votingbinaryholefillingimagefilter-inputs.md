# How To: Votingbinaryholefillingimagefilter Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test VotingBinaryHoleFillingImageFilter inputs

## Prerequisites

**Required Modules:**
- `votingbinaryholefillingimagefilter`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), background=dict(argstr='--background %d'), environ=dict(nohash=True, usedefault=True), foreground=dict(argstr='--foreground %d'), inputVolume=dict(argstr='%s', extensions=None, position=-2), majorityThreshold=dict(argstr='--majorityThreshold %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), radius=dict(argstr='--radius %s', sep=','))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), background=dict(argstr='--background %d'), environ=dict(nohash=True, usedefault=True), foreground=dict(argstr='--foreground %d'), inputVolume=dict(argstr='%s', extensions=None, position=-2), majorityThreshold=dict(argstr='--majorityThreshold %d'), outputVolume=dict(argstr='%s', hash_files=False, position=-1), radius=dict(argstr='--radius %s', sep=','))
```

## Next Steps


---

*Source: test_auto_VotingBinaryHoleFillingImageFilter.py:6 | Complexity: Beginner | Last updated: 2026-05-18*