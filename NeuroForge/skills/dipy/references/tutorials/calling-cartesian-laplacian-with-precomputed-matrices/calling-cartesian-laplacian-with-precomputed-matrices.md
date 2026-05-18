# How To: Calling Cartesian Laplacian With Precomputed Matrices

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test calling cartesian laplacian with precomputed matrices

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `pytest`
- `scipy.integrate`
- `dipy.core.gradients`
- `dipy.data`
- `dipy.reconst`
- `dipy.reconst.shm`
- `dipy.sims.voxel`
- `dipy.testing.decorators`

**Setup Required:**
```python
# Fixtures: radial_order, time_order, ut, us
```

## Step-by-Step Guide

### Step 1: Assign ind_mat = qtdmri.qtdmri_index_matrix(...)

```python
ind_mat = qtdmri.qtdmri_index_matrix(radial_order, time_order)
```

**Verification:**
```python
assert_array_almost_equal(laplacian_matrix_precomputed, laplacian_matrix_regular)
```

### Step 2: Assign part4_reg_mat_tau = qtdmri.part4_reg_matrix_tau(...)

```python
part4_reg_mat_tau = qtdmri.part4_reg_matrix_tau(ind_mat, 1.0)
```

### Step 3: Assign part23_reg_mat_tau = qtdmri.part23_reg_matrix_tau(...)

```python
part23_reg_mat_tau = qtdmri.part23_reg_matrix_tau(ind_mat, 1.0)
```

### Step 4: Assign part1_reg_mat_tau = qtdmri.part1_reg_matrix_tau(...)

```python
part1_reg_mat_tau = qtdmri.part1_reg_matrix_tau(ind_mat, 1.0)
```

### Step 5: Assign unknown = mapmri.mapmri_STU_reg_matrices(...)

```python
S_mat, T_mat, U_mat = mapmri.mapmri_STU_reg_matrices(radial_order)
```

### Step 6: Assign laplacian_matrix_precomputed = qtdmri.qtdmri_laplacian_reg_matrix(...)

```python
laplacian_matrix_precomputed = qtdmri.qtdmri_laplacian_reg_matrix(ind_mat, us, ut, S_mat=S_mat, T_mat=T_mat, U_mat=U_mat, part1_ut_precomp=part1_reg_mat_tau, part23_ut_precomp=part23_reg_mat_tau, part4_ut_precomp=part4_reg_mat_tau)
```

### Step 7: Assign laplacian_matrix_regular = qtdmri.qtdmri_laplacian_reg_matrix(...)

```python
laplacian_matrix_regular = qtdmri.qtdmri_laplacian_reg_matrix(ind_mat, us, ut)
```

### Step 8: Call assert_array_almost_equal()

```python
assert_array_almost_equal(laplacian_matrix_precomputed, laplacian_matrix_regular)
```


## Complete Example

```python
# Setup
# Fixtures: radial_order, time_order, ut, us

# Workflow
ind_mat = qtdmri.qtdmri_index_matrix(radial_order, time_order)
part4_reg_mat_tau = qtdmri.part4_reg_matrix_tau(ind_mat, 1.0)
part23_reg_mat_tau = qtdmri.part23_reg_matrix_tau(ind_mat, 1.0)
part1_reg_mat_tau = qtdmri.part1_reg_matrix_tau(ind_mat, 1.0)
S_mat, T_mat, U_mat = mapmri.mapmri_STU_reg_matrices(radial_order)
laplacian_matrix_precomputed = qtdmri.qtdmri_laplacian_reg_matrix(ind_mat, us, ut, S_mat=S_mat, T_mat=T_mat, U_mat=U_mat, part1_ut_precomp=part1_reg_mat_tau, part23_ut_precomp=part23_reg_mat_tau, part4_ut_precomp=part4_reg_mat_tau)
laplacian_matrix_regular = qtdmri.qtdmri_laplacian_reg_matrix(ind_mat, us, ut)
assert_array_almost_equal(laplacian_matrix_precomputed, laplacian_matrix_regular)
```

## Next Steps


---

*Source: test_qtdmri.py:432 | Complexity: Advanced | Last updated: 2026-05-18*