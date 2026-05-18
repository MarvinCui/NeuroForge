# How To: Cluster Level With Covariates

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test non-parametric inference with cluster-level inference in     the context of covariates.
    

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pandas`
- `pytest`
- `nibabel`
- `numpy.testing`
- `scipy`
- `nilearn._utils.data_gen`
- `nilearn.exceptions`
- `nilearn.glm.first_level`
- `nilearn.glm.second_level`
- `nilearn.image`
- `nilearn.maskers`
- `nilearn.reporting`
- `conftest`

**Setup Required:**
```python
# Fixtures: shape_3d_default, rng, n_subjects
```

## Step-by-Step Guide

### Step 1: 'Test non-parametric inference with cluster-level inference in     the context of covariates.\n    '

```python
'Test non-parametric inference with cluster-level inference in     the context of covariates.\n    '
```

**Verification:**
```python
assert logp_unc_cluster_sizes == logp_max_cluster_sizes
```

### Step 2: Assign shapes = value

```python
shapes = ((*shape_3d_default, 1),)
```

### Step 3: Assign unknown = generate_fake_fmri_data_and_design(...)

```python
mask, fmri_data, _ = generate_fake_fmri_data_and_design(shapes)
```

### Step 4: Assign unc_pval = 0.1

```python
unc_pval = 0.1
```

### Step 5: Assign cov1 = rng.random(...)

```python
cov1 = rng.random(n_subjects)
```

### Step 6: Assign cov2 = rng.random(...)

```python
cov2 = rng.random(n_subjects)
```

### Step 7: Assign X = pd.DataFrame(...)

```python
X = pd.DataFrame({'cov1': cov1, 'cov2': cov2, 'intercept': 1})
```

### Step 8: Assign kernels = rng.uniform(...)

```python
kernels = rng.uniform(low=0, high=5, size=n_subjects)
```

### Step 9: Assign Y = value

```python
Y = [smooth_img(fmri_data[0], kernel) for kernel in kernels]
```

### Step 10: Assign out = non_parametric_inference(...)

```python
out = non_parametric_inference(Y, design_matrix=X, mask=mask, model_intercept=False, second_level_contrast='intercept', n_perm=int(1 / unc_pval), threshold=unc_pval)
```

### Step 11: Assign df = value

```python
df = len(Y) - X.shape[1]
```

### Step 12: Assign neg_log_pval = value

```python
neg_log_pval = -np.log10(stats.t.sf(get_data(out['t']), df=df))
```

### Step 13: Assign logp_unc = new_img_like(...)

```python
logp_unc = new_img_like(out['t'], neg_log_pval)
```

### Step 14: Assign logp_unc_cluster_sizes = list(...)

```python
logp_unc_cluster_sizes = list(get_clusters_table(logp_unc, -np.log10(unc_pval))['Cluster Size (mm3)'])
```

### Step 15: Assign logp_max_cluster_sizes = list(...)

```python
logp_max_cluster_sizes = list(get_clusters_table(out['logp_max_size'], unc_pval)['Cluster Size (mm3)'])
```

### Step 16: Call logp_unc_cluster_sizes.sort()

```python
logp_unc_cluster_sizes.sort()
```

### Step 17: Call logp_max_cluster_sizes.sort()

```python
logp_max_cluster_sizes.sort()
```

**Verification:**
```python
assert logp_unc_cluster_sizes == logp_max_cluster_sizes
```


## Complete Example

```python
# Setup
# Fixtures: shape_3d_default, rng, n_subjects

# Workflow
'Test non-parametric inference with cluster-level inference in     the context of covariates.\n    '
shapes = ((*shape_3d_default, 1),)
mask, fmri_data, _ = generate_fake_fmri_data_and_design(shapes)
unc_pval = 0.1
cov1 = rng.random(n_subjects)
cov2 = rng.random(n_subjects)
X = pd.DataFrame({'cov1': cov1, 'cov2': cov2, 'intercept': 1})
kernels = rng.uniform(low=0, high=5, size=n_subjects)
Y = [smooth_img(fmri_data[0], kernel) for kernel in kernels]
out = non_parametric_inference(Y, design_matrix=X, mask=mask, model_intercept=False, second_level_contrast='intercept', n_perm=int(1 / unc_pval), threshold=unc_pval)
df = len(Y) - X.shape[1]
neg_log_pval = -np.log10(stats.t.sf(get_data(out['t']), df=df))
logp_unc = new_img_like(out['t'], neg_log_pval)
logp_unc_cluster_sizes = list(get_clusters_table(logp_unc, -np.log10(unc_pval))['Cluster Size (mm3)'])
logp_max_cluster_sizes = list(get_clusters_table(out['logp_max_size'], unc_pval)['Cluster Size (mm3)'])
logp_unc_cluster_sizes.sort()
logp_max_cluster_sizes.sort()
assert logp_unc_cluster_sizes == logp_max_cluster_sizes
```

## Next Steps


---

*Source: test_non_parametric_inference.py:250 | Complexity: Advanced | Last updated: 2026-05-18*