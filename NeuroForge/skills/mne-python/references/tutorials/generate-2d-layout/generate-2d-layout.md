# How To: Generate 2D Layout

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test creation of a layout from 2d points.

## Prerequisites

**Required Modules:**
- `copy`
- `pathlib`
- `matplotlib.pyplot`
- `numpy`
- `pytest`
- `numpy.testing`
- `mne`
- `mne._fiff.constants`
- `mne._fiff.meas_info`
- `mne.channels`
- `mne.channels.layout`
- `mne.defaults`
- `mne.io`


## Step-by-Step Guide

### Step 1: 'Test creation of a layout from 2d points.'

```python
'Test creation of a layout from 2d points.'
```

**Verification:**
```python
assert lt.pos[:, :2].max() == 1
```

### Step 2: Assign snobg = 10

```python
snobg = 10
```

**Verification:**
```python
assert lt.pos[:, :2].min() == 0
```

### Step 3: Assign sbg = 15

```python
sbg = 15
```

**Verification:**
```python
assert_allclose(xy[comp_2] / float(xy[comp_1]), lt.pos[comp_2] / float(lt.pos[comp_1]))
```

### Step 4: Assign side = range(...)

```python
side = range(snobg)
```

**Verification:**
```python
assert_allclose(lt.pos[0, [2, 3]], [w, h])
```

### Step 5: Assign bg_image = np.random.RandomState.randn(...)

```python
bg_image = np.random.RandomState(42).randn(sbg, sbg)
```

**Verification:**
```python
assert lt.pos.shape[1] == 4
```

### Step 6: Assign unknown = value

```python
w, h = [0.2, 0.5]
```

**Verification:**
```python
assert len(lt.box) == 4
```

### Step 7: Assign xy = np.array(...)

```python
xy = np.array([(i, j) for i in side for j in side])
```

**Verification:**
```python
assert_allclose(lt_bg.pos[:, :2].max(), xy.max() / float(sbg))
```

### Step 8: Assign lt = generate_2d_layout(...)

```python
lt = generate_2d_layout(xy, w=w, h=h)
```

### Step 9: Assign unknown = value

```python
comp_1, comp_2 = [(5, 0), (7, 0)]
```

**Verification:**
```python
assert lt.pos[:, :2].max() == 1
```

### Step 10: Call assert_allclose()

```python
assert_allclose(lt.pos[0, [2, 3]], [w, h])
```

**Verification:**
```python
assert lt.pos.shape[1] == 4
```

### Step 11: Assign lt_bg = generate_2d_layout(...)

```python
lt_bg = generate_2d_layout(xy, bg_image=bg_image)
```

### Step 12: Call assert_allclose()

```python
assert_allclose(lt_bg.pos[:, :2].max(), xy.max() / float(sbg))
```

### Step 13: Call assert_allclose()

```python
assert_allclose(xy[comp_2] / float(xy[comp_1]), lt.pos[comp_2] / float(lt.pos[comp_1]))
```


## Complete Example

```python
# Workflow
'Test creation of a layout from 2d points.'
snobg = 10
sbg = 15
side = range(snobg)
bg_image = np.random.RandomState(42).randn(sbg, sbg)
w, h = [0.2, 0.5]
xy = np.array([(i, j) for i in side for j in side])
lt = generate_2d_layout(xy, w=w, h=h)
comp_1, comp_2 = [(5, 0), (7, 0)]
assert lt.pos[:, :2].max() == 1
assert lt.pos[:, :2].min() == 0
with np.errstate(invalid='ignore'):
    assert_allclose(xy[comp_2] / float(xy[comp_1]), lt.pos[comp_2] / float(lt.pos[comp_1]))
assert_allclose(lt.pos[0, [2, 3]], [w, h])
assert lt.pos.shape[1] == 4
assert len(lt.box) == 4
lt_bg = generate_2d_layout(xy, bg_image=bg_image)
assert_allclose(lt_bg.pos[:, :2].max(), xy.max() / float(sbg))
```

## Next Steps


---

*Source: test_layout.py:381 | Complexity: Advanced | Last updated: 2026-05-18*