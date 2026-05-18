# How To: Doubleconnect

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test doubleconnect

## Prerequisites

**Required Modules:**
- `glob`
- `os`
- `shutil`
- `itertools`
- `pytest`
- `networkx`
- `interfaces`
- `test_base`
- `test_utils`
- `os`
- `os`


## Step-by-Step Guide

### Step 1: Assign a = pe.Node(...)

```python
a = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='a')
```

**Verification:**
```python
assert 'Trying to connect' in str(excinfo.value)
```

### Step 2: Assign b = pe.Node(...)

```python
b = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='b')
```

**Verification:**
```python
assert 'Trying to connect' in str(excinfo.value)
```

### Step 3: Assign flow1 = pe.Workflow(...)

```python
flow1 = pe.Workflow(name='test')
```

### Step 4: Call flow1.connect()

```python
flow1.connect(a, 'a', b, 'a')
```

**Verification:**
```python
assert 'Trying to connect' in str(excinfo.value)
```

### Step 5: Assign c = pe.Node(...)

```python
c = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='c')
```

### Step 6: Assign flow1 = pe.Workflow(...)

```python
flow1 = pe.Workflow(name='test2')
```

**Verification:**
```python
assert 'Trying to connect' in str(excinfo.value)
```

### Step 7: Call flow1.connect()

```python
flow1.connect(a, 'b', b, 'a')
```

### Step 8: Call flow1.connect()

```python
flow1.connect([(a, c, [('b', 'b')]), (b, c, [('a', 'b')])])
```


## Complete Example

```python
# Workflow
a = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='a')
b = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='b')
flow1 = pe.Workflow(name='test')
flow1.connect(a, 'a', b, 'a')
with pytest.raises(Exception) as excinfo:
    flow1.connect(a, 'b', b, 'a')
assert 'Trying to connect' in str(excinfo.value)
c = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='c')
flow1 = pe.Workflow(name='test2')
with pytest.raises(Exception) as excinfo:
    flow1.connect([(a, c, [('b', 'b')]), (b, c, [('a', 'b')])])
assert 'Trying to connect' in str(excinfo.value)
```

## Next Steps


---

*Source: test_workflows.py:69 | Complexity: Advanced | Last updated: 2026-05-18*