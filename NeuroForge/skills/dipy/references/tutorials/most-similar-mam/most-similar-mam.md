# How To: Most Similar Mam

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test most similar mam

## Prerequisites

**Required Modules:**
- `warnings`
- `numpy`
- `numpy.testing`
- `dipy.data`
- `dipy.io.streamline`
- `dipy.testing`
- `dipy.testing.decorators`
- `dipy.tracking`
- `dipy.tracking.streamline`
- `time`


## Step-by-Step Guide

### Step 1: Assign xyz1 = np.array(...)

```python
xyz1 = np.array([[0, 0, 0], [1, 0, 0], [2, 0, 0], [3, 0, 0]], dtype='float32')
```

### Step 2: Assign xyz2 = np.array(...)

```python
xyz2 = np.array([[0, 1, 1], [1, 0, 1], [2, 3, -2]], dtype='float32')
```

### Step 3: Assign xyz3 = np.array(...)

```python
xyz3 = np.array([[-1, 0, 0], [2, 0, 0], [2, 3, 0], [3, 0, 0]], dtype='float32')
```

### Step 4: Assign tracks = value

```python
tracks = [xyz1, xyz2, xyz3]
```

### Step 5: Call pf.most_similar_track_mam()

```python
pf.most_similar_track_mam(tracks, metric=metric)
```


## Complete Example

```python
# Workflow
xyz1 = np.array([[0, 0, 0], [1, 0, 0], [2, 0, 0], [3, 0, 0]], dtype='float32')
xyz2 = np.array([[0, 1, 1], [1, 0, 1], [2, 3, -2]], dtype='float32')
xyz3 = np.array([[-1, 0, 0], [2, 0, 0], [2, 3, 0], [3, 0, 0]], dtype='float32')
tracks = [xyz1, xyz2, xyz3]
for metric in ('avg', 'min', 'max'):
    pf.most_similar_track_mam(tracks, metric=metric)
```

## Next Steps


---

*Source: test_distances.py:305 | Complexity: Intermediate | Last updated: 2026-05-18*