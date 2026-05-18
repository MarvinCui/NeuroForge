# How To: Remove Similar Peaks

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test remove similar peaks

## Prerequisites

**Required Modules:**
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.reconst.recspeed`


## Step-by-Step Guide

### Step 1: Assign vertices = np.array(...)

```python
vertices = np.array([[1.0, 0.0, 0.0], [0.0, 1.0, 0.0], [0.0, 0.0, 1.0], [1.1, 1.0, 0.0], [0.0, 2.0, 1.0], [2.0, 1.0, 0.0], [1.0, 0.0, 0.0]])
```

### Step 2: Assign norms = np.sqrt(...)

```python
norms = np.sqrt((vertices * vertices).sum(-1))
```

### Step 3: Assign vertices = value

```python
vertices = vertices / norms[:, None]
```

### Step 4: Assign uv = remove_similar_vertices(...)

```python
uv = remove_similar_vertices(vertices, 0.01)
```

### Step 5: Call npt.assert_array_equal()

```python
npt.assert_array_equal(uv, vertices[:6])
```

### Step 6: Assign unknown = remove_similar_vertices(...)

```python
uv, mapping, index = remove_similar_vertices(vertices, 0.01, return_mapping=True, return_index=True)
```

### Step 7: Call npt.assert_array_equal()

```python
npt.assert_array_equal(uv, vertices[:6])
```

### Step 8: Call npt.assert_array_equal()

```python
npt.assert_array_equal(mapping, list(range(6)) + [0])
```

### Step 9: Call npt.assert_array_equal()

```python
npt.assert_array_equal(index, range(6))
```

### Step 10: Assign unknown = remove_similar_vertices(...)

```python
uv, mapping = remove_similar_vertices(vertices, 0.01, return_mapping=True)
```

### Step 11: Call npt.assert_array_equal()

```python
npt.assert_array_equal(uv, vertices[:6])
```

### Step 12: Call npt.assert_array_equal()

```python
npt.assert_array_equal(mapping, list(range(6)) + [0])
```

### Step 13: Assign unknown = remove_similar_vertices(...)

```python
uv, mapping = remove_similar_vertices(vertices, 30, return_mapping=True)
```

### Step 14: Call npt.assert_array_equal()

```python
npt.assert_array_equal(uv, vertices[:4])
```

### Step 15: Call npt.assert_array_equal()

```python
npt.assert_array_equal(mapping, list(range(4)) + [1, 0, 0])
```

### Step 16: Assign unknown = remove_similar_vertices(...)

```python
uv, mapping = remove_similar_vertices(vertices, 60, return_mapping=True)
```

### Step 17: Call npt.assert_array_equal()

```python
npt.assert_array_equal(uv, vertices[:3])
```

### Step 18: Call npt.assert_array_equal()

```python
npt.assert_array_equal(mapping, list(range(3)) + [0, 1, 0, 0])
```

### Step 19: Assign unknown = remove_similar_vertices(...)

```python
uv, index = remove_similar_vertices(vertices, 0.01, return_index=True)
```

### Step 20: Call npt.assert_array_equal()

```python
npt.assert_array_equal(uv, vertices[:6])
```

### Step 21: Call npt.assert_array_equal()

```python
npt.assert_array_equal(index, range(6))
```

### Step 22: Assign unknown = remove_similar_vertices(...)

```python
uv, index = remove_similar_vertices(vertices, 30, return_index=True)
```

### Step 23: Call npt.assert_array_equal()

```python
npt.assert_array_equal(uv, vertices[:4])
```

### Step 24: Call npt.assert_array_equal()

```python
npt.assert_array_equal(index, range(4))
```

### Step 25: Assign unknown = remove_similar_vertices(...)

```python
uv, index = remove_similar_vertices(vertices, 60, return_index=True)
```

### Step 26: Call npt.assert_array_equal()

```python
npt.assert_array_equal(uv, vertices[:3])
```

### Step 27: Call npt.assert_array_equal()

```python
npt.assert_array_equal(index, range(3))
```


## Complete Example

```python
# Workflow
vertices = np.array([[1.0, 0.0, 0.0], [0.0, 1.0, 0.0], [0.0, 0.0, 1.0], [1.1, 1.0, 0.0], [0.0, 2.0, 1.0], [2.0, 1.0, 0.0], [1.0, 0.0, 0.0]])
norms = np.sqrt((vertices * vertices).sum(-1))
vertices = vertices / norms[:, None]
uv = remove_similar_vertices(vertices, 0.01)
npt.assert_array_equal(uv, vertices[:6])
uv, mapping, index = remove_similar_vertices(vertices, 0.01, return_mapping=True, return_index=True)
npt.assert_array_equal(uv, vertices[:6])
npt.assert_array_equal(mapping, list(range(6)) + [0])
npt.assert_array_equal(index, range(6))
uv, mapping = remove_similar_vertices(vertices, 0.01, return_mapping=True)
npt.assert_array_equal(uv, vertices[:6])
npt.assert_array_equal(mapping, list(range(6)) + [0])
uv, mapping = remove_similar_vertices(vertices, 30, return_mapping=True)
npt.assert_array_equal(uv, vertices[:4])
npt.assert_array_equal(mapping, list(range(4)) + [1, 0, 0])
uv, mapping = remove_similar_vertices(vertices, 60, return_mapping=True)
npt.assert_array_equal(uv, vertices[:3])
npt.assert_array_equal(mapping, list(range(3)) + [0, 1, 0, 0])
uv, index = remove_similar_vertices(vertices, 0.01, return_index=True)
npt.assert_array_equal(uv, vertices[:6])
npt.assert_array_equal(index, range(6))
uv, index = remove_similar_vertices(vertices, 30, return_index=True)
npt.assert_array_equal(uv, vertices[:4])
npt.assert_array_equal(index, range(4))
uv, index = remove_similar_vertices(vertices, 60, return_index=True)
npt.assert_array_equal(uv, vertices[:3])
npt.assert_array_equal(index, range(3))
```

## Next Steps


---

*Source: test_peak_finding.py:80 | Complexity: Advanced | Last updated: 2026-05-18*