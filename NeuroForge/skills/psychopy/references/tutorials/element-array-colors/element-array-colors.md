# How To: Element Array Colors

**Difficulty**: Beginner
**Estimated Time**: 5 minutes

## Overview

Instantiate ElementArrayStim: test element array colors

## Prerequisites

**Required Modules:**
- `psychopy.alerts`
- `psychopy.alerts._errorHandler`
- `psychopy.tests`
- `psychopy`
- `numpy`


## Step-by-Step Guide

### Step 1: Assign obj = visual.ElementArrayStim(...)

```python
obj = visual.ElementArrayStim(self.win, units='pix', fieldPos=(0, 0), fieldSize=(128, 128), fieldShape='square', nElements=2, sizes=[[64, 128], [64, 128]], xys=[[-32, 0], [32, 0]], elementMask=None, elementTex=None)
```


## Complete Example

```python
# Workflow
obj = visual.ElementArrayStim(self.win, units='pix', fieldPos=(0, 0), fieldSize=(128, 128), fieldShape='square', nElements=2, sizes=[[64, 128], [64, 128]], xys=[[-32, 0], [32, 0]], elementMask=None, elementTex=None)
```

## Next Steps


---

*Source: test_color.py:112 | Complexity: Beginner | Last updated: 2026-05-18*