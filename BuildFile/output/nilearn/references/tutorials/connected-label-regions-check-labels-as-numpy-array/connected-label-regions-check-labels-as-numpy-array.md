# How To: Connected Label Regions Check Labels As Numpy Array

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test the names of the brain regions given in labels.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nibabel`
- `scipy.ndimage`
- `nilearn._utils.data_gen`
- `nilearn._utils.estimator_checks`
- `nilearn._utils.versions`
- `nilearn.conftest`
- `nilearn.exceptions`
- `nilearn.image`
- `nilearn.regions`
- `nilearn.regions.region_extractor`
- `sklearn.utils.estimator_checks`
- `nilearn._utils.estimator_checks`

**Setup Required:**
```python
# Fixtures: img_labels
```

## Step-by-Step Guide

### Step 1: 'Test the names of the brain regions given in labels.'

```python
'Test the names of the brain regions given in labels.'
```

**Verification:**
```python
assert new_labels2 != ''
```

### Step 2: Assign labels = value

```python
labels = [f'region_{x}' for x in 'abcdefghi']
```

**Verification:**
```python
assert len(new_labels2) >= len(labels)
```

### Step 3: Assign labels = np.asarray(...)

```python
labels = np.asarray(labels)
```

**Verification:**
```python
assert len(provided_labels) < len(unique_labels)
```

### Step 4: Assign unknown = connected_label_regions(...)

```python
_, new_labels2 = connected_label_regions(img_labels, labels=labels)
```

**Verification:**
```python
assert new_labels2 != ''
```

### Step 5: Assign unique_labels = set(...)

```python
unique_labels = set(np.unique(np.asarray(get_data(img_labels))))
```

### Step 6: Call unique_labels.remove()

```python
unique_labels.remove(0)
```

### Step 7: Assign provided_labels = value

```python
provided_labels = [f'region_{x}' for x in 'acfghi']
```

**Verification:**
```python
assert len(provided_labels) < len(unique_labels)
```

### Step 8: Call connected_label_regions()

```python
connected_label_regions(img_labels, labels=provided_labels)
```


## Complete Example

```python
# Setup
# Fixtures: img_labels

# Workflow
'Test the names of the brain regions given in labels.'
labels = [f'region_{x}' for x in 'abcdefghi']
labels = np.asarray(labels)
_, new_labels2 = connected_label_regions(img_labels, labels=labels)
assert new_labels2 != ''
assert len(new_labels2) >= len(labels)
unique_labels = set(np.unique(np.asarray(get_data(img_labels))))
unique_labels.remove(0)
provided_labels = [f'region_{x}' for x in 'acfghi']
assert len(provided_labels) < len(unique_labels)
with pytest.raises(ValueError):
    connected_label_regions(img_labels, labels=provided_labels)
```

## Next Steps


---

*Source: test_region_extractor.py:525 | Complexity: Advanced | Last updated: 2026-05-18*