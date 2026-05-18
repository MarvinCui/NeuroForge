# How To: Getrating

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test getRating

## Prerequisites

**Required Modules:**
- `pathlib`
- `psychopy.tests`
- `psychopy.tests.test_visual.test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.visual.window`
- `psychopy.visual.slider`
- `psychopy.visual.elementarray`
- `psychopy.visual.shape`
- `psychopy.visual.rect`
- `psychopy`
- `numpy`
- `random`


## Step-by-Step Guide

### Step 1: Assign s = Slider(...)

```python
s = Slider(self.win, size=(1, 0.1))
```

**Verification:**
```python
assert s.getRating() == minRating
```

### Step 2: Assign unknown = value

```python
minRating, maxRating = (1, 5)
```

**Verification:**
```python
assert s.getRating() == maxRating
```

### Step 3: Assign s.rating = 1

```python
s.rating = 1
```

**Verification:**
```python
assert s.getRating() == minRating
```

### Step 4: Assign s.rating = 5

```python
s.rating = 5
```

**Verification:**
```python
assert s.getRating() == maxRating
```

### Step 5: Assign s.rating = 0

```python
s.rating = 0
```

**Verification:**
```python
assert s.getRating() == minRating
```

### Step 6: Assign s.rating = 6

```python
s.rating = 6
```

**Verification:**
```python
assert s.getRating() == maxRating
```


## Complete Example

```python
# Workflow
s = Slider(self.win, size=(1, 0.1))
minRating, maxRating = (1, 5)
s.rating = 1
assert s.getRating() == minRating
s.rating = 5
assert s.getRating() == maxRating
s.rating = 0
assert s.getRating() == minRating
s.rating = 6
assert s.getRating() == maxRating
```

## Next Steps


---

*Source: test_slider.py:297 | Complexity: Intermediate | Last updated: 2026-05-18*