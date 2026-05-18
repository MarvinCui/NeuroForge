# How To: Bad Inputs

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test bad inputs

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `numpy`
- `pytest`
- `nilearn._utils.segmentation`

**Setup Required:**
```python
# Fixtures: rng
```

## Step-by-Step Guide

### Step 1: Assign img = np.ones(...)

```python
img = np.ones(10)
```

### Step 2: Assign labels = np.arange(...)

```python
labels = np.arange(10)
```

### Step 3: Assign img = rng.normal(...)

```python
img = rng.normal(size=(3, 3, 3, 3, 3))
```

### Step 4: Assign labels = np.arange.reshape(...)

```python
labels = np.arange(3 ** 5).reshape(img.shape)
```

### Step 5: Assign img = rng.normal(...)

```python
img = rng.normal(size=(10, 10))
```

### Step 6: Assign labels = np.zeros(...)

```python
labels = np.zeros((10, 10))
```

### Step 7: Assign unknown = 2

```python
labels[2, 4] = 2
```

### Step 8: Assign unknown = 5

```python
labels[6, 8] = 5
```

### Step 9: Call random_walker()

```python
random_walker(img, labels)
```

### Step 10: Call random_walker()

```python
random_walker(img, labels)
```

### Step 11: Call random_walker()

```python
random_walker(img, labels, spacing=(1,))
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
img = np.ones(10)
labels = np.arange(10)
with pytest.raises(ValueError):
    random_walker(img, labels)
img = rng.normal(size=(3, 3, 3, 3, 3))
labels = np.arange(3 ** 5).reshape(img.shape)
with pytest.raises(ValueError):
    random_walker(img, labels)
img = rng.normal(size=(10, 10))
labels = np.zeros((10, 10))
labels[2, 4] = 2
labels[6, 8] = 5
with pytest.raises(ValueError):
    random_walker(img, labels, spacing=(1,))
```

## Next Steps


---

*Source: test_segmentation.py:105 | Complexity: Advanced | Last updated: 2026-05-18*