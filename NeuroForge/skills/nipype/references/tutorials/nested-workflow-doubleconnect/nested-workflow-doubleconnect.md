# How To: Nested Workflow Doubleconnect

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test nested workflow doubleconnect

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
assert 'Some connections were not found' in str(excinfo.value)
```

### Step 2: Assign b = pe.Node(...)

```python
b = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='b')
```

### Step 3: Assign c = pe.Node(...)

```python
c = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='c')
```

### Step 4: Assign flow1 = pe.Workflow(...)

```python
flow1 = pe.Workflow(name='test1')
```

### Step 5: Assign flow2 = pe.Workflow(...)

```python
flow2 = pe.Workflow(name='test2')
```

### Step 6: Assign flow3 = pe.Workflow(...)

```python
flow3 = pe.Workflow(name='test3')
```

### Step 7: Call flow1.add_nodes()

```python
flow1.add_nodes([b])
```

### Step 8: Call flow2.connect()

```python
flow2.connect(a, 'a', flow1, 'b.a')
```

**Verification:**
```python
assert 'Some connections were not found' in str(excinfo.value)
```

### Step 9: Call flow3.connect()

```python
flow3.connect(c, 'b', flow2, 'test1.b.b')
```

### Step 10: Call flow3.connect()

```python
flow3.connect(c, 'a', flow2, 'test1.b.a')
```


## Complete Example

```python
# Workflow
a = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='a')
b = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='b')
c = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='c')
flow1 = pe.Workflow(name='test1')
flow2 = pe.Workflow(name='test2')
flow3 = pe.Workflow(name='test3')
flow1.add_nodes([b])
flow2.connect(a, 'a', flow1, 'b.a')
with pytest.raises(Exception) as excinfo:
    flow3.connect(c, 'a', flow2, 'test1.b.a')
assert 'Some connections were not found' in str(excinfo.value)
flow3.connect(c, 'b', flow2, 'test1.b.b')
```

## Next Steps


---

*Source: test_workflows.py:85 | Complexity: Advanced | Last updated: 2026-05-18*