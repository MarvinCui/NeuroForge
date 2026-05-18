# How To: Same Number Of Points

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test same number of points

## Prerequisites

- [ ] Setup code must be executed first

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

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign A = value

```python
A = [rng.random((10, 3)), rng.random((20, 3))]
```

**Verification:**
```python
assert_raises(ValueError, slr.optimize, A, B)
```

### Step 2: Assign B = value

```python
B = [rng.random((21, 3)), rng.random((30, 3))]
```

**Verification:**
```python
assert_raises(ValueError, slr.optimize, C, D)
```

### Step 3: Assign C = value

```python
C = [rng.random((10, 3)), rng.random((10, 3))]
```

**Verification:**
```python
assert_raises(ValueError, slr.optimize, C, B)
```

### Step 4: Assign D = value

```python
D = [rng.random((20, 3)), rng.random((20, 3))]
```

### Step 5: Assign slr = StreamlineLinearRegistration(...)

```python
slr = StreamlineLinearRegistration()
```

### Step 6: Call assert_raises()

```python
assert_raises(ValueError, slr.optimize, A, B)
```

### Step 7: Call assert_raises()

```python
assert_raises(ValueError, slr.optimize, C, D)
```

### Step 8: Call assert_raises()

```python
assert_raises(ValueError, slr.optimize, C, B)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
A = [rng.random((10, 3)), rng.random((20, 3))]
B = [rng.random((21, 3)), rng.random((30, 3))]
C = [rng.random((10, 3)), rng.random((10, 3))]
D = [rng.random((20, 3)), rng.random((20, 3))]
slr = StreamlineLinearRegistration()
assert_raises(ValueError, slr.optimize, A, B)
assert_raises(ValueError, slr.optimize, C, D)
assert_raises(ValueError, slr.optimize, C, B)
```

## Next Steps


---

*Source: test_streamlinear.py:207 | Complexity: Advanced | Last updated: 2026-05-18*