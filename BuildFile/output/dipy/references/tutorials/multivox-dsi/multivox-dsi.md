# How To: Multivox Dsi

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test multivox dsi

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.gradients`
- `dipy.core.sphere_stats`
- `dipy.core.subdivide_octahedron`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst.dsi`
- `dipy.reconst.odf`
- `dipy.reconst.tests.test_dsi`
- `dipy.sims.voxel`


## Step-by-Step Guide

### Step 1: Assign unknown = dsi_deconv_voxels(...)

```python
data, gtab = dsi_deconv_voxels()
```

**Verification:**
```python
assert_equal(data.shape[:-1] + (35, 35, 35), PDF.shape)
```

### Step 2: Assign DS = DiffusionSpectrumDeconvModel(...)

```python
DS = DiffusionSpectrumDeconvModel(gtab)
```

**Verification:**
```python
assert_equal(np.all(np.isreal(PDF)), True)
```

### Step 3: Assign DSfit = DS.fit(...)

```python
DSfit = DS.fit(data)
```

### Step 4: Assign PDF = DSfit.pdf(...)

```python
PDF = DSfit.pdf()
```

### Step 5: Call assert_equal()

```python
assert_equal(data.shape[:-1] + (35, 35, 35), PDF.shape)
```

### Step 6: Call assert_equal()

```python
assert_equal(np.all(np.isreal(PDF)), True)
```


## Complete Example

```python
# Workflow
data, gtab = dsi_deconv_voxels()
DS = DiffusionSpectrumDeconvModel(gtab)
DSfit = DS.fit(data)
PDF = DSfit.pdf()
assert_equal(data.shape[:-1] + (35, 35, 35), PDF.shape)
assert_equal(np.all(np.isreal(PDF)), True)
```

## Next Steps


---

*Source: test_dsi_deconv.py:62 | Complexity: Intermediate | Last updated: 2026-05-18*