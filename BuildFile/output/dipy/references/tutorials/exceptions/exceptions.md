# How To: Exceptions

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test exceptions

## Prerequisites

**Required Modules:**
- `itertools`
- `numpy`
- `numpy.testing`
- `scipy`
- `dipy.align`
- `dipy.align.metrics`
- `dipy.testing.decorators`


## Step-by-Step Guide

### Step 1: Call assert_raises()

```python
assert_raises(ValueError, SSDMetric, 3, step_type='unknown_metric_name')
```

**Verification:**
```python
assert_raises(ValueError, CCMetric, invalid_dim)
```

### Step 2: Call assert_raises()

```python
assert_raises(ValueError, EMMetric, 3, step_type='unknown_metric_name')
```

**Verification:**
```python
assert_raises(ValueError, EMMetric, invalid_dim)
```

### Step 3: Assign shapes_2d = itertools.product(...)

```python
shapes_2d = itertools.product((5, 8), (8, 5))
```

**Verification:**
```python
assert_raises(ValueError, SSDMetric, invalid_dim)
```

### Step 4: Assign shapes_3d = itertools.product(...)

```python
shapes_3d = itertools.product((5, 8), (8, 5), (30, 50))
```

**Verification:**
```python
assert_raises(ValueError, SSDMetric, 3, step_type='unknown_metric_name')
```

### Step 5: Assign all_shapes = itertools.chain(...)

```python
all_shapes = itertools.chain(shapes_2d, shapes_3d)
```

**Verification:**
```python
assert_raises(ValueError, EMMetric, 3, step_type='unknown_metric_name')
```

### Step 6: Assign metric = init_metric(...)

```python
metric = init_metric((9, 9), 4)
```

**Verification:**
```python
assert_raises(ValueError, metric.initialize_iteration)
```

### Step 7: Call metric.initialize_iteration()

```python
metric.initialize_iteration()
```

### Step 8: Call assert_raises()

```python
assert_raises(ValueError, CCMetric, invalid_dim)
```

### Step 9: Call assert_raises()

```python
assert_raises(ValueError, EMMetric, invalid_dim)
```

### Step 10: Call assert_raises()

```python
assert_raises(ValueError, SSDMetric, invalid_dim)
```

### Step 11: Assign dim = len(...)

```python
dim = len(shape)
```

### Step 12: Assign metric = CCMetric(...)

```python
metric = CCMetric(dim, radius=radius)
```

### Step 13: Call metric.set_static_image()

```python
metric.set_static_image(np.arange(np.prod(shape), dtype=float).reshape(shape), np.eye(4), np.ones(dim), np.eye(3))
```

### Step 14: Call metric.set_moving_image()

```python
metric.set_moving_image(np.arange(np.prod(shape), dtype=float).reshape(shape), np.eye(4), np.ones(dim), np.eye(3))
```

### Step 15: Assign metric = init_metric(...)

```python
metric = init_metric(shape, 4)
```

### Step 16: Call assert_raises()

```python
assert_raises(ValueError, metric.initialize_iteration)
```


## Complete Example

```python
# Workflow
for invalid_dim in [-1, 0, 1, 4, 5]:
    assert_raises(ValueError, CCMetric, invalid_dim)
    assert_raises(ValueError, EMMetric, invalid_dim)
    assert_raises(ValueError, SSDMetric, invalid_dim)
assert_raises(ValueError, SSDMetric, 3, step_type='unknown_metric_name')
assert_raises(ValueError, EMMetric, 3, step_type='unknown_metric_name')

def init_metric(shape, radius):
    dim = len(shape)
    metric = CCMetric(dim, radius=radius)
    metric.set_static_image(np.arange(np.prod(shape), dtype=float).reshape(shape), np.eye(4), np.ones(dim), np.eye(3))
    metric.set_moving_image(np.arange(np.prod(shape), dtype=float).reshape(shape), np.eye(4), np.ones(dim), np.eye(3))
    return metric
shapes_2d = itertools.product((5, 8), (8, 5))
shapes_3d = itertools.product((5, 8), (8, 5), (30, 50))
all_shapes = itertools.chain(shapes_2d, shapes_3d)
for shape in all_shapes:
    metric = init_metric(shape, 4)
    assert_raises(ValueError, metric.initialize_iteration)
metric = init_metric((9, 9), 4)
metric.initialize_iteration()
```

## Next Steps


---

*Source: test_metrics.py:12 | Complexity: Advanced | Last updated: 2026-05-18*