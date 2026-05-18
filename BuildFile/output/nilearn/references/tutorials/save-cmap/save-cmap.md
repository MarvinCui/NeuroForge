# How To: Save Cmap

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test covers _save_cmap as well as _bytes_io_to_base64.

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
# Fixtures: cmap, n_colors
```

## Step-by-Step Guide

### Step 1: 'Test covers _save_cmap as well as _bytes_io_to_base64.'

```python
'Test covers _save_cmap as well as _bytes_io_to_base64.'
```

**Verification:**
```python
assert np.allclose(img, expected, atol=0.1)
```

### Step 2: Assign cmap_io = BytesIO(...)

```python
cmap_io = BytesIO()
```

### Step 3: Call _save_cm()

```python
_save_cm(cmap_io, cmap, format='png', n_colors=n_colors)
```

### Step 4: Assign cmap_base64 = _bytes_io_to_base64(...)

```python
cmap_base64 = _bytes_io_to_base64(cmap_io)
```

### Step 5: Assign decoded_io = BytesIO(...)

```python
decoded_io = BytesIO()
```

### Step 6: Call decoded_io.write()

```python
decoded_io.write(base64.b64decode(cmap_base64))
```

### Step 7: Call decoded_io.seek()

```python
decoded_io.seek(0)
```

### Step 8: Assign img = plt.imread(...)

```python
img = plt.imread(decoded_io, format='png')
```

### Step 9: Assign expected = plt.get_cmap(...)

```python
expected = plt.get_cmap(cmap)(np.linspace(0, 1, n_colors))
```

**Verification:**
```python
assert np.allclose(img, expected, atol=0.1)
```


## Complete Example

```python
# Setup
# Fixtures: cmap, n_colors

# Workflow
'Test covers _save_cmap as well as _bytes_io_to_base64.'
cmap_io = BytesIO()
_save_cm(cmap_io, cmap, format='png', n_colors=n_colors)
cmap_base64 = _bytes_io_to_base64(cmap_io)
decoded_io = BytesIO()
decoded_io.write(base64.b64decode(cmap_base64))
decoded_io.seek(0)
img = plt.imread(decoded_io, format='png')
expected = plt.get_cmap(cmap)(np.linspace(0, 1, n_colors))
assert np.allclose(img, expected, atol=0.1)
```

## Next Steps


---

*Source: test_html_stat_map.py:157 | Complexity: Advanced | Last updated: 2026-05-18*