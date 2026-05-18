# How To: Rigid Parallel Lines

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rigid parallel lines

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.align.bundlemin`
- `dipy.align.streamlinear`
- `dipy.core.geometry`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign bundle_initial = simulated_bundle(...)

```python
bundle_initial = simulated_bundle()
```

### Step 2: Assign unknown = center_streamlines(...)

```python
bundle, shift = center_streamlines(bundle_initial)
```

### Step 3: Assign mat = compose_matrix44(...)

```python
mat = compose_matrix44([20, 0, 10, 0, 40, 0])
```

### Step 4: Assign bundle2 = transform_streamlines(...)

```python
bundle2 = transform_streamlines(bundle, mat)
```

### Step 5: Assign bundle_sum_distance = BundleSumDistanceMatrixMetric(...)

```python
bundle_sum_distance = BundleSumDistanceMatrixMetric()
```

### Step 6: Assign options = value

```python
options = {'maxcor': 100, 'ftol': 1e-09, 'gtol': 1e-16, 'eps': 0.001}
```

### Step 7: Assign srr = StreamlineLinearRegistration(...)

```python
srr = StreamlineLinearRegistration(metric=bundle_sum_distance, x0=np.zeros(6), method='L-BFGS-B', bounds=None, options=options)
```

### Step 8: Assign new_bundle2 = srr.optimize.transform(...)

```python
new_bundle2 = srr.optimize(bundle, bundle2).transform(bundle2)
```

### Step 9: Call evaluate_convergence()

```python
evaluate_convergence(bundle, new_bundle2)
```


## Complete Example

```python
# Workflow
bundle_initial = simulated_bundle()
bundle, shift = center_streamlines(bundle_initial)
mat = compose_matrix44([20, 0, 10, 0, 40, 0])
bundle2 = transform_streamlines(bundle, mat)
bundle_sum_distance = BundleSumDistanceMatrixMetric()
options = {'maxcor': 100, 'ftol': 1e-09, 'gtol': 1e-16, 'eps': 0.001}
srr = StreamlineLinearRegistration(metric=bundle_sum_distance, x0=np.zeros(6), method='L-BFGS-B', bounds=None, options=options)
new_bundle2 = srr.optimize(bundle, bundle2).transform(bundle2)
evaluate_convergence(bundle, new_bundle2)
```

## Next Steps


---

*Source: test_streamlinear.py:71 | Complexity: Advanced | Last updated: 2026-05-18*