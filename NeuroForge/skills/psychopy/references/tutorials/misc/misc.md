# How To: Misc

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test misc

## Prerequisites

**Required Modules:**
- `os`
- `sys`
- `pytest`
- `psychopy`
- `psychopy.hardware`
- `psychopy.hardware.emulator`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: Assign MR_settings = BASE_MR_SETTINGS.copy(...)

```python
MR_settings = BASE_MR_SETTINGS.copy()
```

### Step 2: Call MR_settings.update()

```python
MR_settings.update({'sync': 'equal'})
```

### Step 3: Assign vol = launchScan(...)

```python
vol = launchScan(self.win, MR_settings, globalClock=self.globalClock, simResponses=[(0.1, 'a'), (0.2, 1)], mode='Test', log=False)
```

### Step 4: Assign min_MR_settings = value

```python
min_MR_settings = {'TR': 0.2, 'volumes': 3}
```

### Step 5: Assign vol = launchScan(...)

```python
vol = launchScan(self.win, min_MR_settings, globalClock=self.globalClock, mode='Test', log=False)
```

### Step 6: Call core.wait()

```python
core.wait(1, 0)
```


## Complete Example

```python
# Workflow
MR_settings = BASE_MR_SETTINGS.copy()
MR_settings.update({'sync': 'equal'})
vol = launchScan(self.win, MR_settings, globalClock=self.globalClock, simResponses=[(0.1, 'a'), (0.2, 1)], mode='Test', log=False)
min_MR_settings = {'TR': 0.2, 'volumes': 3}
vol = launchScan(self.win, min_MR_settings, globalClock=self.globalClock, mode='Test', log=False)
core.wait(1, 0)
```

## Next Steps


---

*Source: test_emulator.py:84 | Complexity: Intermediate | Last updated: 2026-05-18*