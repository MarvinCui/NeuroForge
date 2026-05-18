# How To: Serialization

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test serialization

## Prerequisites

**Required Modules:**
- `importlib`
- `copy`
- `pathlib`
- `psychopy`
- `psychopy.tests`
- `psychopy.tests.test_visual.test_basevisual`
- `psychopy.tools.stimulustools`
- `psychopy`


## Step-by-Step Guide

### Step 1: Assign win = visual.Window(...)

```python
win = visual.Window()
```

**Verification:**
```python
assert isinstance(win, cls)
```

### Step 2: Assign params = serialize(...)

```python
params = serialize(win, includeClass=True)
```

### Step 3: Assign mod = importlib.import_module(...)

```python
mod = importlib.import_module(params.pop('__module__'))
```

### Step 4: Assign cls = getattr(...)

```python
cls = getattr(mod, params.pop('__class__'))
```

**Verification:**
```python
assert isinstance(win, cls)
```

### Step 5: Assign dupe = cls(...)

```python
dupe = cls(**params)
```

### Step 6: Call dupe.close()

```python
dupe.close()
```


## Complete Example

```python
# Workflow
win = visual.Window()
params = serialize(win, includeClass=True)
mod = importlib.import_module(params.pop('__module__'))
cls = getattr(mod, params.pop('__class__'))
assert isinstance(win, cls)
dupe = cls(**params)
dupe.close()
```

## Next Steps


---

*Source: test_window.py:12 | Complexity: Intermediate | Last updated: 2026-05-18*