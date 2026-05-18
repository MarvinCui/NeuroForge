# How To: B0Calc Inputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test B0Calc inputs

## Prerequisites

**Required Modules:**
- `possum`


## Step-by-Step Guide

### Step 1: Assign input_map = dict(...)

```python
input_map = dict(args=dict(argstr='%s'), chi_air=dict(argstr='--chi0=%e', usedefault=True), compute_xyz=dict(argstr='--xyz', usedefault=True), delta=dict(argstr='-d %e', usedefault=True), directconv=dict(argstr='--directconv', usedefault=True), environ=dict(nohash=True, usedefault=True), extendboundary=dict(argstr='--extendboundary=%0.2f', usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=0), out_file=dict(argstr='-o %s', extensions=None, name_source=['in_file'], name_template='%s_b0field', output_name='out_file', position=1), output_type=dict(), x_b0=dict(argstr='--b0x=%0.2f', usedefault=True, xor=['xyz_b0']), x_grad=dict(argstr='--gx=%0.4f', usedefault=True), xyz_b0=dict(argstr='--b0x=%0.2f --b0y=%0.2f --b0=%0.2f', xor=['x_b0', 'y_b0', 'z_b0']), y_b0=dict(argstr='--b0y=%0.2f', usedefault=True, xor=['xyz_b0']), y_grad=dict(argstr='--gy=%0.4f', usedefault=True), z_b0=dict(argstr='--b0=%0.2f', usedefault=True, xor=['xyz_b0']), z_grad=dict(argstr='--gz=%0.4f', usedefault=True))
```


## Complete Example

```python
# Workflow
input_map = dict(args=dict(argstr='%s'), chi_air=dict(argstr='--chi0=%e', usedefault=True), compute_xyz=dict(argstr='--xyz', usedefault=True), delta=dict(argstr='-d %e', usedefault=True), directconv=dict(argstr='--directconv', usedefault=True), environ=dict(nohash=True, usedefault=True), extendboundary=dict(argstr='--extendboundary=%0.2f', usedefault=True), in_file=dict(argstr='-i %s', extensions=None, mandatory=True, position=0), out_file=dict(argstr='-o %s', extensions=None, name_source=['in_file'], name_template='%s_b0field', output_name='out_file', position=1), output_type=dict(), x_b0=dict(argstr='--b0x=%0.2f', usedefault=True, xor=['xyz_b0']), x_grad=dict(argstr='--gx=%0.4f', usedefault=True), xyz_b0=dict(argstr='--b0x=%0.2f --b0y=%0.2f --b0=%0.2f', xor=['x_b0', 'y_b0', 'z_b0']), y_b0=dict(argstr='--b0y=%0.2f', usedefault=True, xor=['xyz_b0']), y_grad=dict(argstr='--gy=%0.4f', usedefault=True), z_b0=dict(argstr='--b0=%0.2f', usedefault=True, xor=['xyz_b0']), z_grad=dict(argstr='--gz=%0.4f', usedefault=True))
```

## Next Steps


---

*Source: test_auto_B0Calc.py:6 | Complexity: Beginner | Last updated: 2026-05-18*