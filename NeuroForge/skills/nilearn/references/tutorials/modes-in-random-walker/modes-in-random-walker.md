# How To: Modes In Random Walker

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test modes in random walker

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

### Step 1: Assign img = value

```python
img = np.zeros((30, 30, 30)) + 0.1 * rng.standard_normal(size=(30, 30, 30))
```

**Verification:**
```python
assert (random_walker_cg.reshape(img.shape)[6, 6, 6] == 1).all()
```

### Step 2: Assign unknown = 1

```python
img[9:21, 9:21, 9:21] = 1
```

**Verification:**
```python
assert img.shape == random_walker_cg.shape
```

### Step 3: Assign unknown = 0

```python
img[10:20, 10:20, 10:20] = 0
```

### Step 4: Assign labels = np.zeros_like(...)

```python
labels = np.zeros_like(img)
```

### Step 5: Assign unknown = 1

```python
labels[6, 6, 6] = 1
```

### Step 6: Assign unknown = 2

```python
labels[14, 15, 16] = 2
```

### Step 7: Assign random_walker_cg = random_walker(...)

```python
random_walker_cg = random_walker(img, labels, beta=90)
```

**Verification:**
```python
assert (random_walker_cg.reshape(img.shape)[6, 6, 6] == 1).all()
```

### Step 8: Assign unknown = value

```python
labels[5:25, 26:29, 26:29] = -1
```

### Step 9: Call random_walker()

```python
random_walker(img, labels, beta=30)
```


## Complete Example

```python
# Setup
# Fixtures: rng

# Workflow
img = np.zeros((30, 30, 30)) + 0.1 * rng.standard_normal(size=(30, 30, 30))
img[9:21, 9:21, 9:21] = 1
img[10:20, 10:20, 10:20] = 0
labels = np.zeros_like(img)
labels[6, 6, 6] = 1
labels[14, 15, 16] = 2
random_walker_cg = random_walker(img, labels, beta=90)
assert (random_walker_cg.reshape(img.shape)[6, 6, 6] == 1).all()
assert img.shape == random_walker_cg.shape
labels[5:25, 26:29, 26:29] = -1
random_walker(img, labels, beta=30)
```

## Next Steps


---

*Source: test_segmentation.py:20 | Complexity: Advanced | Last updated: 2026-05-18*