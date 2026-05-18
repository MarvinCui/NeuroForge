# How To: Value

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that setting the value of progress has the desired effect

## Prerequisites

**Required Modules:**
- `psychopy`
- `test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.tests`
- `pathlib`


## Step-by-Step Guide

### Step 1: '\n        Check that setting the value of progress has the desired effect\n        '

```python
'\n        Check that setting the value of progress has the desired effect\n        '
```

### Step 2: Assign vals = value

```python
vals = [0, 0.3, 0.6, 1]
```

### Step 3: Assign layouts = value

```python
layouts = [{'anchor': 'left center', 'direction': 'horizontal'}, {'anchor': 'center center', 'direction': 'horizontal'}, {'anchor': 'right center', 'direction': 'horizontal'}, {'anchor': 'top center', 'direction': 'vertical'}, {'anchor': 'center center', 'direction': 'vertical'}, {'anchor': 'bottom center', 'direction': 'vertical'}]
```

### Step 4: Assign cases = value

```python
cases = []
```

### Step 5: Call self.win.flip()

```python
self.win.flip()
```

### Step 6: Assign self.obj.anchor = value

```python
self.obj.anchor = case['anchor']
```

### Step 7: Assign pos = value

```python
pos = [0, 0]
```

### Step 8: Assign self.obj.pos = pos

```python
self.obj.pos = pos
```

### Step 9: Assign self.obj.direction = value

```python
self.obj.direction = case['direction']
```

### Step 10: Assign self.obj.progress = value

```python
self.obj.progress = case['val']
```

### Step 11: Call self.obj.draw()

```python
self.obj.draw()
```

### Step 12: Call utils.compareScreenshot()

```python
utils.compareScreenshot(filename, self.win, crit=8)
```

### Step 13: Assign lo = lo.copy(...)

```python
lo = lo.copy()
```

### Step 14: Call lo.update()

```python
lo.update({'val': val})
```

### Step 15: Call cases.append()

```python
cases.append(lo)
```

### Step 16: Assign unknown = value

```python
pos[0] = -64
```

### Step 17: Assign unknown = 64

```python
pos[0] = 64
```

### Step 18: Assign unknown = value

```python
pos[1] = -32
```

### Step 19: Assign unknown = 32

```python
pos[1] = 32
```

### Step 20: Assign filename = value

```python
filename = f'{self.__class__.__name__}_testValue_%(direction)s_%(anchor)s_%(val)s.png' % case
```

### Step 21: Assign filename = value

```python
filename = f'{self.__class__.__name__}_testValue_minmax_%(val)s.png' % case
```


## Complete Example

```python
# Workflow
'\n        Check that setting the value of progress has the desired effect\n        '
vals = [0, 0.3, 0.6, 1]
layouts = [{'anchor': 'left center', 'direction': 'horizontal'}, {'anchor': 'center center', 'direction': 'horizontal'}, {'anchor': 'right center', 'direction': 'horizontal'}, {'anchor': 'top center', 'direction': 'vertical'}, {'anchor': 'center center', 'direction': 'vertical'}, {'anchor': 'bottom center', 'direction': 'vertical'}]
cases = []
for val in vals:
    for lo in layouts:
        lo = lo.copy()
        lo.update({'val': val})
        cases.append(lo)
for case in cases:
    self.win.flip()
    self.obj.anchor = case['anchor']
    pos = [0, 0]
    if 'left' in case['anchor']:
        pos[0] = -64
    if 'right' in case['anchor']:
        pos[0] = 64
    if 'bottom' in case['anchor']:
        pos[1] = -32
    if 'top' in case['anchor']:
        pos[1] = 32
    self.obj.pos = pos
    self.obj.direction = case['direction']
    self.obj.progress = case['val']
    self.obj.draw()
    if case['val'] not in (0, 1):
        filename = f'{self.__class__.__name__}_testValue_%(direction)s_%(anchor)s_%(val)s.png' % case
    else:
        filename = f'{self.__class__.__name__}_testValue_minmax_%(val)s.png' % case
    utils.compareScreenshot(filename, self.win, crit=8)
```

## Next Steps


---

*Source: test_progress.py:44 | Complexity: Advanced | Last updated: 2026-05-18*