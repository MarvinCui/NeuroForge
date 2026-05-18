# How To: Two Runs Model

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Create two runs of data.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `json`
- `warnings`
- `numpy`
- `pandas`
- `pytest`
- `nilearn._utils.data_gen`
- `nilearn._utils.helpers`
- `nilearn.glm.first_level`
- `nilearn.glm.io`
- `nilearn.glm.second_level`
- `nilearn.maskers`

**Setup Required:**
```python
# Fixtures: n_cols_design_matrix
```

## Step-by-Step Guide

### Step 1: 'Create two runs of data.'

```python
'Create two runs of data.'
```

### Step 2: Assign unknown = value

```python
shapes, rk = ([(7, 8, 9, 10), (7, 8, 9, 10)], n_cols_design_matrix)
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
```

### Step 4: Assign mapper = value

```python
mapper = {design_matrices[0].columns[0]: 'AAA', design_matrices[0].columns[1]: 'BBB'}
```

### Step 5: Assign unknown = unknown.rename(...)

```python
design_matrices[0] = design_matrices[0].rename(columns=mapper)
```

### Step 6: Assign mapper = value

```python
mapper = {design_matrices[1].columns[0]: 'AAA', design_matrices[1].columns[1]: 'BBB'}
```

### Step 7: Assign unknown = unknown.rename(...)

```python
design_matrices[1] = design_matrices[1].rename(columns=mapper)
```

### Step 8: Assign masker = NiftiMasker(...)

```python
masker = NiftiMasker(mask)
```

### Step 9: Call masker.fit()

```python
masker.fit()
```


## Complete Example

```python
# Setup
# Fixtures: n_cols_design_matrix

# Workflow
'Create two runs of data.'
shapes, rk = ([(7, 8, 9, 10), (7, 8, 9, 10)], n_cols_design_matrix)
mask, fmri_data, design_matrices = generate_fake_fmri_data_and_design(shapes, rk)
mapper = {design_matrices[0].columns[0]: 'AAA', design_matrices[0].columns[1]: 'BBB'}
design_matrices[0] = design_matrices[0].rename(columns=mapper)
mapper = {design_matrices[1].columns[0]: 'AAA', design_matrices[1].columns[1]: 'BBB'}
design_matrices[1] = design_matrices[1].rename(columns=mapper)
masker = NiftiMasker(mask)
masker.fit()
return FirstLevelModel(mask_img=None, minimize_memory=False).fit(fmri_data, design_matrices=design_matrices)
```

## Next Steps


---

*Source: test_io.py:185 | Complexity: Advanced | Last updated: 2026-05-18*