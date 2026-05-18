# How To: Editable

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test editable

## Prerequisites

**Required Modules:**
- `pathlib`
- `numpy`
- `psychopy`
- `psychopy.alerts`
- `psychopy.alerts._errorHandler`
- `psychopy.tests.test_visual.test_basevisual`
- `psychopy.tests.test_experiment.test_component_compile_python`
- `psychopy.visual`
- `psychopy.visual`
- `psychopy.tools.fontmanager`
- `pytest`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: Assign self.textbox.editable = True

```python
self.textbox.editable = True
```

**Verification:**
```python
assert self.textbox in editables
```

### Step 2: Assign textbox2 = TextBox2(...)

```python
textbox2 = TextBox2(self.win, '', 'Noto Sans', pos=(0.5, 0.5), size=(1, 1), units='height', letterHeight=0.1, colorSpace='rgb', editable=True)
```

**Verification:**
```python
assert textbox2 in editables
```

### Step 3: Assign editables = value

```python
editables = []
```

**Verification:**
```python
assert self.win.currentEditable == textbox2
```

### Step 4: Assign self.win.currentEditable = value

```python
self.win.currentEditable = self.textbox
```

**Verification:**
```python
assert self.textbox not in editables
```

### Step 5: Call self.win.nextEditable()

```python
self.win.nextEditable()
```

**Verification:**
```python
assert textbox2 not in editables
```

### Step 6: Assign self.textbox.editable = False

```python
self.textbox.editable = False
```

### Step 7: Assign textbox2.editable = False

```python
textbox2.editable = False
```

### Step 8: Assign editables = value

```python
editables = []
```

**Verification:**
```python
assert self.textbox not in editables
```

### Step 9: Call editables.append()

```python
editables.append(ref())
```

### Step 10: Call editables.append()

```python
editables.append(ref())
```


## Complete Example

```python
# Workflow
self.textbox.editable = True
textbox2 = TextBox2(self.win, '', 'Noto Sans', pos=(0.5, 0.5), size=(1, 1), units='height', letterHeight=0.1, colorSpace='rgb', editable=True)
editables = []
for ref in self.win._editableChildren:
    editables.append(ref())
assert self.textbox in editables
assert textbox2 in editables
self.win.currentEditable = self.textbox
self.win.nextEditable()
assert self.win.currentEditable == textbox2
self.textbox.editable = False
textbox2.editable = False
editables = []
for ref in self.win._editableChildren:
    editables.append(ref())
assert self.textbox not in editables
assert textbox2 not in editables
del textbox2
```

## Next Steps


---

*Source: test_textbox.py:473 | Complexity: Advanced | Last updated: 2026-05-18*