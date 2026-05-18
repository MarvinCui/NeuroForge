# How To: Epidewarp Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test EPIDeWarp inputs

## Prerequisites

**Required Modules:**
- `epi`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), cleanup=dict(argstr='--cleanup'), dph_file=dict(argstr='--dph %s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), epi_file=dict(argstr='--epi %s', extensions=None), epidw=dict(argstr='--epidw %s', genfile=False), esp=dict(argstr='--esp %s', usedefault=True), exf_file=dict(argstr='--exf %s', extensions=None), exfdw=dict(argstr='--exfdw %s', genfile=True), mag_file=dict(argstr='--mag %s', extensions=None, mandatory=True, position=0), nocleanup=dict(argstr='--nocleanup', usedefault=True), output_type=dict(), sigma=dict(argstr='--sigma %s', usedefault=True), tediff=dict(argstr='--tediff %s', usedefault=True), tmpdir=dict(argstr='--tmpdir %s', genfile=True), vsm=dict(argstr='--vsm %s', genfile=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), cleanup=dict(argstr='--cleanup'), dph_file=dict(argstr='--dph %s', extensions=None, mandatory=True), environ=dict(nohash=True, usedefault=True), epi_file=dict(argstr='--epi %s', extensions=None), epidw=dict(argstr='--epidw %s', genfile=False), esp=dict(argstr='--esp %s', usedefault=True), exf_file=dict(argstr='--exf %s', extensions=None), exfdw=dict(argstr='--exfdw %s', genfile=True), mag_file=dict(argstr='--mag %s', extensions=None, mandatory=True, position=0), nocleanup=dict(argstr='--nocleanup', usedefault=True), output_type=dict(), sigma=dict(argstr='--sigma %s', usedefault=True), tediff=dict(argstr='--tediff %s', usedefault=True), tmpdir=dict(argstr='--tmpdir %s', genfile=True), vsm=dict(argstr='--vsm %s', genfile=True))
```

## Next Steps


---

*Source: test_auto_EPIDeWarp.py:6 | Complexity: Beginner | Last updated: 2026-05-18*