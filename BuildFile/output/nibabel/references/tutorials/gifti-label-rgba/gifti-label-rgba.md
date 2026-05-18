# How To: Gifti Label Rgba

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test gifti label rgba

## Prerequisites

**Required Modules:**
- `itertools`
- `sys`
- `io`
- `numpy`
- `pytest`
- `numpy.testing`
- `nibabel.tmpdirs`
- `fileholders`
- `nifti1`
- `testing`
- `test_parse_gifti_fast`
- `gifti`


## Step-by-Step Guide

### Step 1: Assign rgba = rng.random(...)

```python
rgba = rng.random(4)
```

**Verification:**
```python
assert_array_equal(rgba, gl1.rgba)
```

### Step 2: Assign kwargs = dict(...)

```python
kwargs = dict(zip(['red', 'green', 'blue', 'alpha'], rgba))
```

**Verification:**
```python
assert not np.allclose(rgba, gl1.rgba)
```

### Step 3: Assign gl1 = GiftiLabel(...)

```python
gl1 = GiftiLabel(**kwargs)
```

**Verification:**
```python
assert_array_equal(rgba, gl2.rgba)
```

### Step 4: Call assert_array_equal()

```python
assert_array_equal(rgba, gl1.rgba)
```

**Verification:**
```python
assert not np.allclose(rgba, gl2.rgba)
```

### Step 5: Assign gl1.red = value

```python
gl1.red = 2 * gl1.red
```

**Verification:**
```python
assert len(gl4.rgba) == 4
```

### Step 6: Assign gl2 = GiftiLabel(...)

```python
gl2 = GiftiLabel()
```

**Verification:**
```python
assert np.all([elem is None for elem in gl4.rgba])
```

### Step 7: Assign gl2.rgba = rgba

```python
gl2.rgba = rgba
```

### Step 8: Call assert_array_equal()

```python
assert_array_equal(rgba, gl2.rgba)
```

### Step 9: Assign gl2.blue = value

```python
gl2.blue = 2 * gl2.blue
```

**Verification:**
```python
assert not np.allclose(rgba, gl2.rgba)
```

### Step 10: Assign gl3 = GiftiLabel(...)

```python
gl3 = GiftiLabel(**kwargs)
```

### Step 11: Call pytest.raises()

```python
pytest.raises(ValueError, assign_rgba, gl3, rgba[:2])
```

### Step 12: Call pytest.raises()

```python
pytest.raises(ValueError, assign_rgba, gl3, rgba.tolist() + rgba.tolist())
```

### Step 13: Assign gl4 = GiftiLabel(...)

```python
gl4 = GiftiLabel()
```

**Verification:**
```python
assert len(gl4.rgba) == 4
```

### Step 14: Assign gl.rgba = val

```python
gl.rgba = val
```


## Complete Example

```python
# Workflow
rgba = rng.random(4)
kwargs = dict(zip(['red', 'green', 'blue', 'alpha'], rgba))
gl1 = GiftiLabel(**kwargs)
assert_array_equal(rgba, gl1.rgba)
gl1.red = 2 * gl1.red
assert not np.allclose(rgba, gl1.rgba)
gl2 = GiftiLabel()
gl2.rgba = rgba
assert_array_equal(rgba, gl2.rgba)
gl2.blue = 2 * gl2.blue
assert not np.allclose(rgba, gl2.rgba)

def assign_rgba(gl, val):
    gl.rgba = val
gl3 = GiftiLabel(**kwargs)
pytest.raises(ValueError, assign_rgba, gl3, rgba[:2])
pytest.raises(ValueError, assign_rgba, gl3, rgba.tolist() + rgba.tolist())
gl4 = GiftiLabel()
assert len(gl4.rgba) == 4
assert np.all([elem is None for elem in gl4.rgba])
```

## Next Steps


---

*Source: test_gifti.py:376 | Complexity: Advanced | Last updated: 2026-05-18*