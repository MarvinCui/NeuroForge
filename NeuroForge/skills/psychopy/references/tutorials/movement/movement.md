# How To: Movement

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test movement

## Prerequisites

**Required Modules:**
- `psychopy`
- `pathlib`


## Step-by-Step Guide

### Step 1: Assign cases = value

```python
cases = []
```

### Step 2: Assign intervals = 3

```python
intervals = 3
```

### Step 3: Call self.win.flip()

```python
self.win.flip()
```

### Step 4: Assign self.obj.azimuth = value

```python
self.obj.azimuth = case['azimuth']
```

### Step 5: Assign self.obj.elevation = value

```python
self.obj.elevation = case['elevation']
```

### Step 6: Call self.obj.draw()

```python
self.obj.draw()
```

### Step 7: Assign exemplar = value

```python
exemplar = self.path / 'testPanorama_mvmt_{azimuth:.1f}_{elevation:.1f}.png'.format(**case)
```

### Step 8: Call utils.compareScreenshot()

```python
utils.compareScreenshot(str(exemplar), self.win, crit=7)
```

### Step 9: Call self.win.flip()

```python
self.win.flip()
```

### Step 10: Call cases.append()

```python
cases.append({'azimuth': az * 2 / intervals - 1, 'elevation': (al + 1) * 2 / intervals - 1})
```


## Complete Example

```python
# Workflow
cases = []
intervals = 3
for az in range(intervals):
    for al in range(intervals - 1):
        cases.append({'azimuth': az * 2 / intervals - 1, 'elevation': (al + 1) * 2 / intervals - 1})
cases += [{'azimuth': 0, 'elevation': -1}, {'azimuth': 0, 'elevation': 1}]
self.win.flip()
for case in cases:
    self.obj.azimuth = case['azimuth']
    self.obj.elevation = case['elevation']
    self.obj.draw()
    exemplar = self.path / 'testPanorama_mvmt_{azimuth:.1f}_{elevation:.1f}.png'.format(**case)
    utils.compareScreenshot(str(exemplar), self.win, crit=7)
    self.win.flip()
```

## Next Steps


---

*Source: test_panorama.py:12 | Complexity: Advanced | Last updated: 2026-05-18*