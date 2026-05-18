# How To: With Simulated Bundles2

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test with simulated bundles2

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `numpy.testing`
- `dipy.segment.clustering`
- `dipy.segment.featurespeed`
- `dipy.segment.metricspeed`
- `dipy.testing.decorators`
- `dipy.tracking.streamline`


## Step-by-Step Guide

### Step 1: Assign bundles = bearing_bundles(...)

```python
bundles = bearing_bundles(4, 2)
```

**Verification:**
```python
assert_equal(tree.refdata, streamlines)
```

### Step 2: Call bundles.append()

```python
bundles.append(straight_bundle(1))
```

### Step 3: Assign streamlines = list(...)

```python
streamlines = list(itertools.chain(*bundles))
```

### Step 4: Assign thresholds = value

```python
thresholds = [10, 2, 1]
```

### Step 5: Assign qbx_class = QuickBundlesX(...)

```python
qbx_class = QuickBundlesX(thresholds)
```

### Step 6: Assign tree = qbx_class.cluster(...)

```python
tree = qbx_class.cluster(streamlines)
```

### Step 7: Call assert_equal()

```python
assert_equal(tree.refdata, streamlines)
```


## Complete Example

```python
# Workflow
bundles = bearing_bundles(4, 2)
bundles.append(straight_bundle(1))
streamlines = list(itertools.chain(*bundles))
thresholds = [10, 2, 1]
qbx_class = QuickBundlesX(thresholds)
tree = qbx_class.cluster(streamlines)
assert_equal(tree.refdata, streamlines)
```

## Next Steps


---

*Source: test_qbx.py:158 | Complexity: Intermediate | Last updated: 2026-05-18*