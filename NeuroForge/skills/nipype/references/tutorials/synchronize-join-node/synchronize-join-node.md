# How To: Synchronize Join Node

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test join on an input node which has the ``synchronize`` flag set to True.

## Prerequisites

- [ ] Setup code must be executed first

**Required Modules:**
- `pytest`
- `interfaces`
- `interfaces.utility`
- `interfaces.base`

**Setup Required:**
```python
# Fixtures: tmpdir
```

## Step-by-Step Guide

### Step 1: 'Test join on an input node which has the ``synchronize`` flag set to True.'

```python
'Test join on an input node which has the ``synchronize`` flag set to True.'
```

**Verification:**
```python
assert len(result.nodes()) == 6, 'The number of expanded nodes is incorrect.'
```

### Step 2: Assign _products = value

```python
_products = []
```

**Verification:**
```python
assert _products == [8, 15], 'The post-join products is incorrect: %s.' % _products
```

### Step 3: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 4: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='test')
```

### Step 5: Assign inputspec = pe.Node(...)

```python
inputspec = pe.Node(IdentityInterface(fields=['m', 'n']), name='inputspec')
```

### Step 6: Assign inputspec.iterables = value

```python
inputspec.iterables = [('m', [1, 2]), ('n', [3, 4])]
```

### Step 7: Assign inputspec.synchronize = True

```python
inputspec.synchronize = True
```

### Step 8: Assign inc1 = pe.Node(...)

```python
inc1 = pe.Node(IncrementInterface(), name='inc1')
```

### Step 9: Call wf.connect()

```python
wf.connect(inputspec, 'm', inc1, 'input1')
```

### Step 10: Assign inc2 = pe.Node(...)

```python
inc2 = pe.Node(IncrementInterface(), name='inc2')
```

### Step 11: Call wf.connect()

```python
wf.connect(inputspec, 'n', inc2, 'input1')
```

### Step 12: Assign join = pe.JoinNode(...)

```python
join = pe.JoinNode(IdentityInterface(fields=['vector1', 'vector2']), joinsource='inputspec', name='join')
```

### Step 13: Call wf.connect()

```python
wf.connect(inc1, 'output1', join, 'vector1')
```

### Step 14: Call wf.connect()

```python
wf.connect(inc2, 'output1', join, 'vector2')
```

### Step 15: Assign prod = pe.MapNode(...)

```python
prod = pe.MapNode(ProductInterface(), name='prod', iterfield=['input1', 'input2'])
```

### Step 16: Call wf.connect()

```python
wf.connect(join, 'vector1', prod, 'input1')
```

### Step 17: Call wf.connect()

```python
wf.connect(join, 'vector2', prod, 'input2')
```

### Step 18: Assign result = wf.run(...)

```python
result = wf.run()
```

**Verification:**
```python
assert len(result.nodes()) == 6, 'The number of expanded nodes is incorrect.'
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test join on an input node which has the ``synchronize`` flag set to True.'
global _products
_products = []
tmpdir.chdir()
wf = pe.Workflow(name='test')
inputspec = pe.Node(IdentityInterface(fields=['m', 'n']), name='inputspec')
inputspec.iterables = [('m', [1, 2]), ('n', [3, 4])]
inputspec.synchronize = True
inc1 = pe.Node(IncrementInterface(), name='inc1')
wf.connect(inputspec, 'm', inc1, 'input1')
inc2 = pe.Node(IncrementInterface(), name='inc2')
wf.connect(inputspec, 'n', inc2, 'input1')
join = pe.JoinNode(IdentityInterface(fields=['vector1', 'vector2']), joinsource='inputspec', name='join')
wf.connect(inc1, 'output1', join, 'vector1')
wf.connect(inc2, 'output1', join, 'vector2')
prod = pe.MapNode(ProductInterface(), name='prod', iterfield=['input1', 'input2'])
wf.connect(join, 'vector1', prod, 'input1')
wf.connect(join, 'vector2', prod, 'input2')
result = wf.run()
assert len(result.nodes()) == 6, 'The number of expanded nodes is incorrect.'
assert _products == [8, 15], 'The post-join products is incorrect: %s.' % _products
```

## Next Steps


---

*Source: test_join.py:413 | Complexity: Advanced | Last updated: 2026-05-18*