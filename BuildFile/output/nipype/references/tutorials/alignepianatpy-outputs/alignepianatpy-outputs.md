# How To: Alignepianatpy Outputs

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate dict: test AlignEpiAnatPy outputs

## Prerequisites

**Required Modules:**
- `preprocess`


## Step-by-Step Guide

### Step 1: Assign output_map = dict(...)

```python
output_map = dict(anat_al_mat=dict(extensions=None), anat_al_orig=dict(extensions=None), epi_al_mat=dict(extensions=None), epi_al_orig=dict(extensions=None), epi_al_tlrc_mat=dict(extensions=None), epi_reg_al_mat=dict(extensions=None), epi_tlrc_al=dict(extensions=None), epi_vr_al_mat=dict(extensions=None), epi_vr_motion=dict(extensions=None), skullstrip=dict(extensions=None))
```


## Complete Example

```python
# Workflow
output_map = dict(anat_al_mat=dict(extensions=None), anat_al_orig=dict(extensions=None), epi_al_mat=dict(extensions=None), epi_al_orig=dict(extensions=None), epi_al_tlrc_mat=dict(extensions=None), epi_reg_al_mat=dict(extensions=None), epi_tlrc_al=dict(extensions=None), epi_vr_al_mat=dict(extensions=None), epi_vr_motion=dict(extensions=None), skullstrip=dict(extensions=None))
```

## Next Steps


---

*Source: test_auto_AlignEpiAnatPy.py:67 | Complexity: Beginner | Last updated: 2026-05-18*