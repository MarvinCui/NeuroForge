# How To: Gettime

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test getTime

## Prerequisites

**Required Modules:**
- `psychopy.tests`
- `psychopy.tests.test_iohub.testutil`
- `psychopy.iohub`
- `psychopy.core`


## Step-by-Step Guide

### Step 1: Assign ta = Computer.currentSec(...)

```python
ta = Computer.currentSec()
```

**Verification:**
```python
assert ta <= tb <= tc <= tp
```

### Step 2: Assign tb = Computer.currentTime(...)

```python
tb = Computer.currentTime()
```

**Verification:**
```python
assert tp - ta < 0.002
```

### Step 3: Assign tc = Computer.getTime(...)

```python
tc = Computer.getTime()
```

**Verification:**
```python
assert ta <= tb <= tc <= tp
```

### Step 4: Assign tp = getTime(...)

```python
tp = getTime()
```

**Verification:**
```python
assert tp - ta < 0.01
```

### Step 5: Assign ta = getTime(...)

```python
ta = getTime()
```

### Step 6: Assign tb = self.io.getTime(...)

```python
tb = self.io.getTime()
```

### Step 7: Assign tc = self.io.getTime(...)

```python
tc = self.io.getTime()
```

### Step 8: Assign tp = getTime(...)

```python
tp = getTime()
```

**Verification:**
```python
assert ta <= tb <= tc <= tp
```


## Complete Example

```python
# Workflow
ta = Computer.currentSec()
tb = Computer.currentTime()
tc = Computer.getTime()
tp = getTime()
assert ta <= tb <= tc <= tp
assert tp - ta < 0.002
ta = getTime()
tb = self.io.getTime()
tc = self.io.getTime()
tp = getTime()
assert ta <= tb <= tc <= tp
assert tp - ta < 0.01
```

## Next Steps


---

*Source: test_computer.py:31 | Complexity: Advanced | Last updated: 2026-05-18*