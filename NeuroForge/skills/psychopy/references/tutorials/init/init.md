# How To: Init

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test init

## Prerequisites

**Required Modules:**
- `psychopy.visual`
- `pytest`
- `pyglet`


## Step-by-Step Guide

### Step 1: Assign m = CustomMouse(...)

```python
m = CustomMouse(self.win, showLimitBox=True, autoLog=False)
```

**Verification:**
```python
assert (m.leftLimit, m.topLimit, m.rightLimit, m.bottomLimit) == (-1, 1, 0.99, -0.98)
```

### Step 2: Call m.getPos()

```python
m.getPos()
```

**Verification:**
```python
assert m.visible == True
```

### Step 3: Call m.draw()

```python
m.draw()
```

**Verification:**
```python
assert m.showLimitBox == True
```

### Step 4: Assign m.clickOnUp, m.wasDown = True

```python
m.clickOnUp = m.wasDown = True
```

**Verification:**
```python
assert m.clickOnUp == False
```

### Step 5: Assign m.isDownNow = False

```python
m.isDownNow = False
```

**Verification:**
```python
assert (m.leftLimit, m.topLimit, m.rightLimit, m.bottomLimit) == (-64.0, 128.0, 59.0, -118.0)
```

### Step 6: Call m.draw()

```python
m.draw()
```

**Verification:**
```python
assert m.visible == True
```

### Step 7: Call m.getClicks()

```python
m.getClicks()
```

**Verification:**
```python
assert m.showLimitBox == m.clickOnUp == False
```

### Step 8: Call m.resetClicks()

```python
m.resetClicks()
```

### Step 9: Call m.getVisible()

```python
m.getVisible()
```

### Step 10: Call m.setVisible()

```python
m.setVisible(False)
```

### Step 11: Call m.setPointer()

```python
m.setPointer(TextStim(self.win, text='x'))
```

### Step 12: Assign m = CustomMouse(...)

```python
m = CustomMouse(self.winpix, autoLog=False)
```

**Verification:**
```python
assert (m.leftLimit, m.topLimit, m.rightLimit, m.bottomLimit) == (-64.0, 128.0, 59.0, -118.0)
```

### Step 13: Call m.getPos()

```python
m.getPos()
```

### Step 14: Call m.setPointer()

```python
m.setPointer('a')
```


## Complete Example

```python
# Workflow
m = CustomMouse(self.win, showLimitBox=True, autoLog=False)
assert (m.leftLimit, m.topLimit, m.rightLimit, m.bottomLimit) == (-1, 1, 0.99, -0.98)
assert m.visible == True
assert m.showLimitBox == True
assert m.clickOnUp == False
m.getPos()
m.draw()
m.clickOnUp = m.wasDown = True
m.isDownNow = False
m.draw()
m.getClicks()
m.resetClicks()
m.getVisible()
m.setVisible(False)
with pytest.raises(AttributeError):
    m.setPointer('a')
m.setPointer(TextStim(self.win, text='x'))
m = CustomMouse(self.winpix, autoLog=False)
assert (m.leftLimit, m.topLimit, m.rightLimit, m.bottomLimit) == (-64.0, 128.0, 59.0, -118.0)
assert m.visible == True
assert m.showLimitBox == m.clickOnUp == False
m.getPos()
```

## Next Steps


---

*Source: test_custommouse.py:19 | Complexity: Advanced | Last updated: 2026-05-18*