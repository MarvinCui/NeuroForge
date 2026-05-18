# How To: Tracking Error

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test tracking error

## Prerequisites

**Required Modules:**
- `warnings`
- `nibabel`
- `numpy`
- `numpy.testing`
- `dipy.core.sphere`
- `dipy.data`
- `dipy.direction.peaks`
- `dipy.reconst.shm`
- `dipy.tracking`
- `dipy.tracking.stopping_criterion`
- `dipy.tracking.streamline`
- `dipy.tracking.utils`


## Step-by-Step Guide

### Step 1: Assign sh = np.array(...)

```python
sh = np.array([(64, 61, 57)])
```

### Step 2: Assign seeds = value

```python
seeds = [np.array([0.0, 0.0, 0.0], 'float'), np.array([1.0, 2.0, 3.0], 'float')]
```

### Step 3: Assign mask = np.ones(...)

```python
mask = np.ones((10, 10, 10))
```

### Step 4: Assign sc = BinaryStoppingCriterion(...)

```python
sc = BinaryStoppingCriterion(mask)
```

### Step 5: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), sf=sh, sh=sh)
```

### Step 6: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4))
```

### Step 7: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), pam=sh)
```

### Step 8: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), sf=sh)
```

### Step 9: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), sh=sh, seed_directions=1)
```

### Step 10: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), sh=sh, seed_directions=[1])
```

### Step 11: Call npt.assert_raises()

```python
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), sf=sh, seed_directions=[1])
```


## Complete Example

```python
# Workflow
sh = np.array([(64, 61, 57)])
seeds = [np.array([0.0, 0.0, 0.0], 'float'), np.array([1.0, 2.0, 3.0], 'float')]
mask = np.ones((10, 10, 10))
sc = BinaryStoppingCriterion(mask)
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), sf=sh, sh=sh)
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4))
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), pam=sh)
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), sf=sh)
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), sh=sh, seed_directions=1)
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), sh=sh, seed_directions=[1])
npt.assert_raises(ValueError, tracker.deterministic_tracking, seeds, sc, np.eye(4), sf=sh, seed_directions=[1])
```

## Next Steps


---

*Source: test_tracker.py:120 | Complexity: Advanced | Last updated: 2026-05-18*