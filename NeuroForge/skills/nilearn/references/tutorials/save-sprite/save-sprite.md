# How To: Save Sprite

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test covers _save_sprite as well as _bytes_io_to_base64.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `base64`
- `io`
- `numpy`
- `pytest`
- `matplotlib`
- `nibabel`
- `nilearn`
- `nilearn.conftest`
- `nilearn.image`
- `nilearn.plotting._engine_utils`
- `nilearn.plotting.html_stat_map`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: 'Test covers _save_sprite as well as _bytes_io_to_base64.'

```python
'Test covers _save_sprite as well as _bytes_io_to_base64.'
```

**Verification:**
```python
assert np.allclose(img, cmapped, atol=0.1)
```

### Step 2: Assign data = rng.uniform.reshape(...)

```python
data = rng.uniform(size=140).reshape(7, 5, 4)
```

### Step 3: Assign mask = np.zeros(...)

```python
mask = np.zeros((7, 5, 4), dtype=int)
```

### Step 4: Assign unknown = 1

```python
mask[1:-1, 1:-1, 1:-1] = 1
```

### Step 5: Assign sprite_io = BytesIO(...)

```python
sprite_io = BytesIO()
```

### Step 6: Call _save_sprite()

```python
_save_sprite(data, sprite_io, vmin=0, vmax=1, mask=mask, format='png')
```

### Step 7: Assign sprite_base64 = _bytes_io_to_base64(...)

```python
sprite_base64 = _bytes_io_to_base64(sprite_io)
```

### Step 8: Assign decoded_io = BytesIO(...)

```python
decoded_io = BytesIO()
```

### Step 9: Call decoded_io.write()

```python
decoded_io.write(base64.b64decode(sprite_base64))
```

### Step 10: Call decoded_io.seek()

```python
decoded_io.seek(0)
```

### Step 11: Assign img = plt.imread(...)

```python
img = plt.imread(decoded_io, format='png')
```

### Step 12: Assign correct_img = np.ma.array(...)

```python
correct_img = np.ma.array(_data_to_sprite(data), mask=_data_to_sprite(mask))
```

### Step 13: Assign correct_img = plt.Normalize(...)

```python
correct_img = plt.Normalize(0, 1)(correct_img)
```

### Step 14: Assign cmapped = plt.get_cmap(...)

```python
cmapped = plt.get_cmap('Greys')(correct_img)
```

**Verification:**
```python
assert np.allclose(img, cmapped, atol=0.1)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
'Test covers _save_sprite as well as _bytes_io_to_base64.'
data = rng.uniform(size=140).reshape(7, 5, 4)
mask = np.zeros((7, 5, 4), dtype=int)
mask[1:-1, 1:-1, 1:-1] = 1
sprite_io = BytesIO()
_save_sprite(data, sprite_io, vmin=0, vmax=1, mask=mask, format='png')
sprite_base64 = _bytes_io_to_base64(sprite_io)
decoded_io = BytesIO()
decoded_io.write(base64.b64decode(sprite_base64))
decoded_io.seek(0)
img = plt.imread(decoded_io, format='png')
correct_img = np.ma.array(_data_to_sprite(data), mask=_data_to_sprite(mask))
correct_img = plt.Normalize(0, 1)(correct_img)
cmapped = plt.get_cmap('Greys')(correct_img)
assert np.allclose(img, cmapped, atol=0.1)
```

## Next Steps


---

*Source: test_html_stat_map.py:129 | Complexity: Advanced | Last updated: 2026-05-18*