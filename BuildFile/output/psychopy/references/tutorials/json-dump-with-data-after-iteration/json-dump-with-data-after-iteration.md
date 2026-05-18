# How To: Json Dump With Data After Iteration

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test json dump with data after iteration

## Prerequisites

**Required Modules:**
- `os`
- `glob`
- `os.path`
- `shutil`
- `tempfile`
- `numpy`
- `io`
- `json_tricks`
- `pytest`
- `psychopy`
- `psychopy.tools.filetools`
- `psychopy.tests`


## Step-by-Step Guide

### Step 1: Assign t = data.TrialHandler2(...)

```python
t = data.TrialHandler2(self.conditions, nReps=5)
```

**Verification:**
```python
assert t == t_loaded
```

### Step 2: Call t.addData()

```python
t.addData('foo', 'bar')
```

### Step 3: Call t.__next__()

```python
t.__next__()
```

### Step 4: Assign dump = t.saveAsJson(...)

```python
dump = t.saveAsJson()
```

### Step 5: Assign t.origin = ''

```python
t.origin = ''
```

### Step 6: Assign t_loaded = json_tricks.loads(...)

```python
t_loaded = json_tricks.loads(dump)
```

### Step 7: Assign t_loaded._rng = np.random.default_rng(...)

```python
t_loaded._rng = np.random.default_rng()
```

### Step 8: Assign t_loaded._rng.bit_generator.state = value

```python
t_loaded._rng.bit_generator.state = t_loaded._rng_state
```

**Verification:**
```python
assert t == t_loaded
```


## Complete Example

```python
# Workflow
t = data.TrialHandler2(self.conditions, nReps=5)
t.addData('foo', 'bar')
t.__next__()
dump = t.saveAsJson()
t.origin = ''
t_loaded = json_tricks.loads(dump)
t_loaded._rng = np.random.default_rng()
t_loaded._rng.bit_generator.state = t_loaded._rng_state
del t_loaded._rng_state
assert t == t_loaded
```

## Next Steps


---

*Source: test_TrialHandler2.py:236 | Complexity: Advanced | Last updated: 2026-05-18*