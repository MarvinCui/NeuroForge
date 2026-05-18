# How To: Recordrating

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test recordRating

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
assert len(s.history) == counter
```

### Step 2: Assign unknown = value

```python
minRating, maxRating = (1, 5)
```

**Verification:**
```python
assert len(ratings) == counter
```

### Step 3: Assign counter = 0

```python
counter = 0
```

**Verification:**
```python
assert min(ratings) == minRating
```

### Step 4: Assign ratings = value

```python
ratings = [rating[0] for rating in s.history]
```

**Verification:**
```python
assert max(ratings) == maxRating
```

### Step 5: Assign RT = value

```python
RT = [rt[1] for rt in s.history]
```

**Verification:**
```python
assert len(RT) == counter
```

### Step 6: Call s.recordRating()

```python
s.recordRating(rates, random.random())
```

**Verification:**
```python
assert max(RT) <= 1
```


## Complete Example

```python
# Workflow
s = Slider(self.win, size=(1, 0.1))
minRating, maxRating = (1, 5)
counter = 0
for rates in range(0, 7):
    s.recordRating(rates, random.random())
    counter += 1
ratings = [rating[0] for rating in s.history]
RT = [rt[1] for rt in s.history]
assert len(s.history) == counter
assert len(ratings) == counter
assert min(ratings) == minRating
assert max(ratings) == maxRating
assert len(RT) == counter
assert max(RT) <= 1
assert min(RT) >= 0
```

## Next Steps


---

*Source: test_slider.py:270 | Complexity: Intermediate | Last updated: 2026-05-18*