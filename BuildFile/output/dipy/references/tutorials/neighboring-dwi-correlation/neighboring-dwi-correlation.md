# How To: Neighboring Dwi Correlation

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test NDC under various conditions.

## Prerequisites

**Required Modules:**
- `numpy`
- `dipy.core.geometry`
- `dipy.core.gradients`
- `dipy.stats.qc`


## Step-by-Step Guide

### Step 1: 'Test NDC under various conditions.'

```python
'Test NDC under various conditions.'
```

**Verification:**
```python
assert np.allclose(real_r, estimated_ndc)
```

### Step 2: Assign unknown = create_test_data(...)

```python
real_r, dwi_data, mask, gtab = create_test_data(test_r=0.3, cube_size=10, mask_size=6, num_dwi_vols=10, num_b0s=2)
```

**Verification:**
```python
assert maskless_ndc != real_r
```

### Step 3: Assign estimated_ndc = neighboring_dwi_correlation(...)

```python
estimated_ndc = neighboring_dwi_correlation(dwi_data, gtab, mask=mask)
```

**Verification:**
```python
assert np.allclose(real_r, estimated_ndc)
```

### Step 4: Assign maskless_ndc = neighboring_dwi_correlation(...)

```python
maskless_ndc = neighboring_dwi_correlation(dwi_data, gtab)
```

**Verification:**
```python
assert np.allclose(real_r, estimated_ndc)
```

### Step 5: Assign unknown = create_test_data(...)

```python
real_r, dwi_data, mask, gtab = create_test_data(test_r=0.3, cube_size=10, mask_size=6, num_dwi_vols=10, num_b0s=0)
```

**Verification:**
```python
assert np.allclose(real_r, estimated_ndc)
```

### Step 6: Assign estimated_ndc = neighboring_dwi_correlation(...)

```python
estimated_ndc = neighboring_dwi_correlation(dwi_data, gtab, mask=mask)
```

**Verification:**
```python
assert np.allclose(real_r, estimated_ndc)
```

### Step 7: Assign unknown = create_test_data(...)

```python
real_r, dwi_data, mask, gtab = create_test_data(test_r=0.8, cube_size=10, mask_size=6, num_dwi_vols=10, num_b0s=2)
```

### Step 8: Assign estimated_ndc = neighboring_dwi_correlation(...)

```python
estimated_ndc = neighboring_dwi_correlation(dwi_data, gtab, mask=mask)
```

**Verification:**
```python
assert np.allclose(real_r, estimated_ndc)
```

### Step 9: Assign unknown = create_test_data(...)

```python
real_r, dwi_data, mask, gtab = create_test_data(test_r=0.5, cube_size=100, mask_size=49, num_dwi_vols=160, num_b0s=2)
```

### Step 10: Assign estimated_ndc = neighboring_dwi_correlation(...)

```python
estimated_ndc = neighboring_dwi_correlation(dwi_data, gtab, mask=mask)
```

**Verification:**
```python
assert np.allclose(real_r, estimated_ndc)
```


## Complete Example

```python
# Workflow
'Test NDC under various conditions.'
real_r, dwi_data, mask, gtab = create_test_data(test_r=0.3, cube_size=10, mask_size=6, num_dwi_vols=10, num_b0s=2)
estimated_ndc = neighboring_dwi_correlation(dwi_data, gtab, mask=mask)
assert np.allclose(real_r, estimated_ndc)
maskless_ndc = neighboring_dwi_correlation(dwi_data, gtab)
assert maskless_ndc != real_r
real_r, dwi_data, mask, gtab = create_test_data(test_r=0.3, cube_size=10, mask_size=6, num_dwi_vols=10, num_b0s=0)
estimated_ndc = neighboring_dwi_correlation(dwi_data, gtab, mask=mask)
assert np.allclose(real_r, estimated_ndc)
real_r, dwi_data, mask, gtab = create_test_data(test_r=0.8, cube_size=10, mask_size=6, num_dwi_vols=10, num_b0s=2)
estimated_ndc = neighboring_dwi_correlation(dwi_data, gtab, mask=mask)
assert np.allclose(real_r, estimated_ndc)
real_r, dwi_data, mask, gtab = create_test_data(test_r=0.5, cube_size=100, mask_size=49, num_dwi_vols=160, num_b0s=2)
estimated_ndc = neighboring_dwi_correlation(dwi_data, gtab, mask=mask)
assert np.allclose(real_r, estimated_ndc)
```

## Next Steps


---

*Source: test_qc.py:90 | Complexity: Advanced | Last updated: 2026-05-18*