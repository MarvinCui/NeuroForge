# How To: Workflow Add

**Difficulty**: Intermediate
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: test workflow add

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

### Step 1: Assign n1 = pe.Node(...)

```python
n1 = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='n1')
```

### Step 2: Assign n2 = pe.Node(...)

```python
n2 = pe.Node(niu.IdentityInterface(fields=['c', 'd']), name='n2')
```

### Step 3: Assign n3 = pe.Node(...)

```python
n3 = pe.Node(niu.IdentityInterface(fields=['c', 'd']), name='n1')
```

### Step 4: Assign w1 = pe.Workflow(...)

```python
w1 = pe.Workflow(name='test')
```

### Step 5: Call w1.connect()

```python
w1.connect(n1, 'a', n2, 'c')
```

### Step 6: Call w1.connect()

```python
w1.connect([(w1, n2, [('n1.a', 'd')])])
```

### Step 7: Call w1.add_nodes()

```python
w1.add_nodes([node])
```


## Complete Example

```python
# Workflow
n1 = pe.Node(niu.IdentityInterface(fields=['a', 'b']), name='n1')
n2 = pe.Node(niu.IdentityInterface(fields=['c', 'd']), name='n2')
n3 = pe.Node(niu.IdentityInterface(fields=['c', 'd']), name='n1')
w1 = pe.Workflow(name='test')
w1.connect(n1, 'a', n2, 'c')
for node in [n1, n2, n3]:
    with pytest.raises(IOError):
        w1.add_nodes([node])
with pytest.raises(IOError):
    w1.connect([(w1, n2, [('n1.a', 'd')])])
```

## Next Steps


---

*Source: test_workflows.py:56 | Complexity: Intermediate | Last updated: 2026-05-18*