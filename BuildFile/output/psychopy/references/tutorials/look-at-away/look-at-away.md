# How To: Look At Away

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test look at away

## Prerequisites

**Required Modules:**
- `numpy`
- `pytest`
- `psychopy.tests`
- `test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy`


## Step-by-Step Guide

### Step 1: Assign looks = np.array(...)

```python
looks = np.array([[0.1, 0.2], [0.3, 0.4], [0.6, 0.65], [0.9, 1]])
```

**Verification:**
```python
assert all(np.isclose(self.obj.timesOn, looks[:, 0], 0.05))
```

### Step 2: Assign t = 0

```python
t = 0
```

**Verification:**
```python
assert all(np.isclose(self.obj.timesOff, looks[:, 1], 0.05))
```

### Step 3: Assign clock = core.Clock(...)

```python
clock = core.Clock()
```

**Verification:**
```python
assert self.obj.numLooks == looks.shape[0]
```

### Step 4: Call self._lookAway()

```python
self._lookAway()
```

**Verification:**
```python
assert all(np.isclose(self.obj.timesOn, looks[:, 0], 0.05))
```

### Step 5: Call pytest.skip()

```python
pytest.skip()
```

### Step 6: Assign inLook = np.logical_and(...)

```python
inLook = np.logical_and(looks[:, 0] < t, looks[:, 1] > t)
```

### Step 7: Assign t = clock.getTime(...)

```python
t = clock.getTime()
```

### Step 8: Call self._lookAt()

```python
self._lookAt()
```

### Step 9: Call self._lookAway()

```python
self._lookAway()
```

### Step 10: Call self.obj.timesOn.append()

```python
self.obj.timesOn.append(t)
```

### Step 11: Assign self.obj.wasLookedIn = True

```python
self.obj.wasLookedIn = True
```

### Step 12: Call self.obj.timesOff.append()

```python
self.obj.timesOff.append(t)
```

### Step 13: Assign self.obj.wasLookedIn = False

```python
self.obj.wasLookedIn = False
```


## Complete Example

```python
# Workflow
if utils.RUNNING_IN_VM:
    pytest.skip()
looks = np.array([[0.1, 0.2], [0.3, 0.4], [0.6, 0.65], [0.9, 1]])
t = 0
clock = core.Clock()
self._lookAway()
while t < looks.max() + 0.1:
    inLook = np.logical_and(looks[:, 0] < t, looks[:, 1] > t)
    if any(inLook):
        self._lookAt()
    else:
        self._lookAway()
    if self.obj.isLookedIn and (not self.obj.wasLookedIn):
        self.obj.timesOn.append(t)
        self.obj.wasLookedIn = True
    if self.obj.wasLookedIn and (not self.obj.isLookedIn):
        self.obj.timesOff.append(t)
        self.obj.wasLookedIn = False
    t = clock.getTime()
assert all(np.isclose(self.obj.timesOn, looks[:, 0], 0.05))
assert all(np.isclose(self.obj.timesOff, looks[:, 1], 0.05))
assert self.obj.numLooks == looks.shape[0]
```

## Next Steps


---

*Source: test_roi.py:62 | Complexity: Advanced | Last updated: 2026-05-18*