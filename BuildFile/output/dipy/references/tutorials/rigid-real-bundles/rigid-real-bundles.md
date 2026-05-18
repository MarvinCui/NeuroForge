# How To: Rigid Real Bundles

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test rigid real bundles

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

### Step 1: Assign bundle_initial = value

```python
bundle_initial = fornix_streamlines()[:20]
```

**Verification:**
```python
assert_raises(ValueError, StreamlineLinearRegistration, method='Whatever')
```

### Step 2: Assign unknown = center_streamlines(...)

```python
bundle, shift = center_streamlines(bundle_initial)
```

### Step 3: Assign mat = compose_matrix44(...)

```python
mat = compose_matrix44([0, 0, 20, 45.0, 0, 0])
```

### Step 4: Assign bundle2 = transform_streamlines(...)

```python
bundle2 = transform_streamlines(bundle, mat)
```

### Step 5: Assign bundle_sum_distance = BundleSumDistanceMatrixMetric(...)

```python
bundle_sum_distance = BundleSumDistanceMatrixMetric()
```

### Step 6: Assign srr = StreamlineLinearRegistration(...)

```python
srr = StreamlineLinearRegistration(metric=bundle_sum_distance, x0=np.zeros(6), method='Powell')
```

### Step 7: Assign new_bundle2 = srr.optimize.transform(...)

```python
new_bundle2 = srr.optimize(bundle, bundle2).transform(bundle2)
```

### Step 8: Call evaluate_convergence()

```python
evaluate_convergence(bundle, new_bundle2)
```

### Step 9: Assign bundle_min_distance = BundleMinDistanceMatrixMetric(...)

```python
bundle_min_distance = BundleMinDistanceMatrixMetric()
```

### Step 10: Assign srr = StreamlineLinearRegistration(...)

```python
srr = StreamlineLinearRegistration(metric=bundle_min_distance, x0=np.zeros(6), method='Powell')
```

### Step 11: Assign new_bundle2 = srr.optimize.transform(...)

```python
new_bundle2 = srr.optimize(bundle, bundle2).transform(bundle2)
```

### Step 12: Call evaluate_convergence()

```python
evaluate_convergence(bundle, new_bundle2)
```

### Step 13: Call assert_raises()

```python
assert_raises(ValueError, StreamlineLinearRegistration, method='Whatever')
```


## Complete Example

```python
# Workflow
bundle_initial = fornix_streamlines()[:20]
bundle, shift = center_streamlines(bundle_initial)
mat = compose_matrix44([0, 0, 20, 45.0, 0, 0])
bundle2 = transform_streamlines(bundle, mat)
bundle_sum_distance = BundleSumDistanceMatrixMetric()
srr = StreamlineLinearRegistration(metric=bundle_sum_distance, x0=np.zeros(6), method='Powell')
new_bundle2 = srr.optimize(bundle, bundle2).transform(bundle2)
evaluate_convergence(bundle, new_bundle2)
bundle_min_distance = BundleMinDistanceMatrixMetric()
srr = StreamlineLinearRegistration(metric=bundle_min_distance, x0=np.zeros(6), method='Powell')
new_bundle2 = srr.optimize(bundle, bundle2).transform(bundle2)
evaluate_convergence(bundle, new_bundle2)
assert_raises(ValueError, StreamlineLinearRegistration, method='Whatever')
```

## Next Steps


---

*Source: test_streamlinear.py:92 | Complexity: Advanced | Last updated: 2026-05-18*