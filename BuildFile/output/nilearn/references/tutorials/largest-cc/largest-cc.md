# How To: Largest Cc

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check the extraction of the largest connected component.

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn._utils`
- `nilearn._utils.ndimage`


## Step-by-Step Guide

### Step 1: 'Check the extraction of the largest connected component.'

```python
'Check the extraction of the largest connected component.'
```

### Step 2: Assign a = np.zeros(...)

```python
a = np.zeros((6, 6, 6))
```

### Step 3: Assign unknown = 1

```python
a[1:3, 1:3, 1:3] = 1
```

### Step 4: Call np.testing.assert_equal()

```python
np.testing.assert_equal(a, largest_connected_component(a))
```

### Step 5: Assign a_change_type = a.astype(...)

```python
a_change_type = a.astype('>f8')
```

### Step 6: Call np.testing.assert_equal()

```python
np.testing.assert_equal(a, largest_connected_component(a_change_type))
```

### Step 7: Assign b = a.copy(...)

```python
b = a.copy()
```

### Step 8: Assign unknown = 1

```python
b[5, 5, 5] = 1
```

### Step 9: Call np.testing.assert_equal()

```python
np.testing.assert_equal(a, largest_connected_component(b))
```

### Step 10: Assign b_change_type = b.astype(...)

```python
b_change_type = b.astype('>f8')
```

### Step 11: Call np.testing.assert_equal()

```python
np.testing.assert_equal(a, largest_connected_component(b_change_type))
```

### Step 12: Assign img = data_gen.generate_labeled_regions(...)

```python
img = data_gen.generate_labeled_regions(shape=(10, 11, 12), n_regions=2)
```

### Step 13: Call largest_connected_component()

```python
largest_connected_component(a)
```

### Step 14: Call largest_connected_component()

```python
largest_connected_component(img)
```

### Step 15: Call largest_connected_component()

```python
largest_connected_component('Test String')
```


## Complete Example

```python
# Workflow
'Check the extraction of the largest connected component.'
a = np.zeros((6, 6, 6))
with pytest.raises(ValueError):
    largest_connected_component(a)
a[1:3, 1:3, 1:3] = 1
np.testing.assert_equal(a, largest_connected_component(a))
a_change_type = a.astype('>f8')
np.testing.assert_equal(a, largest_connected_component(a_change_type))
b = a.copy()
b[5, 5, 5] = 1
np.testing.assert_equal(a, largest_connected_component(b))
b_change_type = b.astype('>f8')
np.testing.assert_equal(a, largest_connected_component(b_change_type))
img = data_gen.generate_labeled_regions(shape=(10, 11, 12), n_regions=2)
with pytest.raises(ValueError):
    largest_connected_component(img)
with pytest.raises(ValueError):
    largest_connected_component('Test String')
```

## Next Steps


---

*Source: test_ndimage.py:10 | Complexity: Advanced | Last updated: 2026-05-18*