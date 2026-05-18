# How To: Dtiprocess Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes
**Tags**: workflow, integration

## Overview

Workflow: test dtiprocess outputs

## Prerequisites

**Required Modules:**
- `diffusion`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(RD_output=dict(extensions=None), color_fa_output=dict(extensions=None), deformation_output=dict(extensions=None), fa_gradient_output=dict(extensions=None), fa_gradmag_output=dict(extensions=None), fa_output=dict(extensions=None), frobenius_norm_output=dict(extensions=None), lambda1_output=dict(extensions=None), lambda2_output=dict(extensions=None), lambda3_output=dict(extensions=None), md_output=dict(extensions=None), negative_eigenvector_output=dict(extensions=None), outmask=dict(extensions=None), principal_eigenvector_output=dict(extensions=None), rot_output=dict(extensions=None))
```

**Verification:**
```python
assert getattr(outputs.traits()[key], metakey) == value
```

### Step 2: Assign outputs = dtiprocess.output_spec(...)

```python
outputs = dtiprocess.output_spec()
```

**Verification:**
```python
assert getattr(outputs.traits()[key], metakey) == value
```


## Complete Example

```python
# Workflow
output_map = dict(RD_output=dict(extensions=None), color_fa_output=dict(extensions=None), deformation_output=dict(extensions=None), fa_gradient_output=dict(extensions=None), fa_gradmag_output=dict(extensions=None), fa_output=dict(extensions=None), frobenius_norm_output=dict(extensions=None), lambda1_output=dict(extensions=None), lambda2_output=dict(extensions=None), lambda3_output=dict(extensions=None), md_output=dict(extensions=None), negative_eigenvector_output=dict(extensions=None), outmask=dict(extensions=None), principal_eigenvector_output=dict(extensions=None), rot_output=dict(extensions=None))
outputs = dtiprocess.output_spec()
for key, metadata in list(output_map.items()):
    for metakey, value in list(metadata.items()):
        assert getattr(outputs.traits()[key], metakey) == value
```

## Next Steps


---

*Source: test_auto_dtiprocess.py:130 | Complexity: Beginner | Last updated: 2026-05-18*