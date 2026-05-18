# How To: Multifield Join Node

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test join on several fields.

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

### Step 1: 'Test join on several fields.'

```python
'Test join on several fields.'
```

**Verification:**
```python
assert len(result.nodes()) == 10, 'The number of expanded nodes is incorrect.'
```

### Step 2: Assign _products = value

```python
_products = []
```

**Verification:**
```python
assert set(_products) == {8, 10, 12, 15}, 'The post-join products is incorrect: %s.' % _products
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

### Step 7: Assign inc1 = pe.Node(...)

```python
inc1 = pe.Node(IncrementInterface(), name='inc1')
```

### Step 8: Call wf.connect()

```python
wf.connect(inputspec, 'm', inc1, 'input1')
```

### Step 9: Assign inc2 = pe.Node(...)

```python
inc2 = pe.Node(IncrementInterface(), name='inc2')
```

### Step 10: Call wf.connect()

```python
wf.connect(inputspec, 'n', inc2, 'input1')
```

### Step 11: Assign join = pe.JoinNode(...)

```python
join = pe.JoinNode(IdentityInterface(fields=['vector1', 'vector2']), joinsource='inputspec', name='join')
```

### Step 12: Call wf.connect()

```python
wf.connect(inc1, 'output1', join, 'vector1')
```

### Step 13: Call wf.connect()

```python
wf.connect(inc2, 'output1', join, 'vector2')
```

### Step 14: Assign prod = pe.MapNode(...)

```python
prod = pe.MapNode(ProductInterface(), name='prod', iterfield=['input1', 'input2'])
```

### Step 15: Call wf.connect()

```python
wf.connect(join, 'vector1', prod, 'input1')
```

### Step 16: Call wf.connect()

```python
wf.connect(join, 'vector2', prod, 'input2')
```

### Step 17: Assign result = wf.run(...)

```python
result = wf.run()
```

**Verification:**
```python
assert len(result.nodes()) == 10, 'The number of expanded nodes is incorrect.'
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test join on several fields.'
global _products
_products = []
tmpdir.chdir()
wf = pe.Workflow(name='test')
inputspec = pe.Node(IdentityInterface(fields=['m', 'n']), name='inputspec')
inputspec.iterables = [('m', [1, 2]), ('n', [3, 4])]
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
assert len(result.nodes()) == 10, 'The number of expanded nodes is incorrect.'
assert set(_products) == {8, 10, 12, 15}, 'The post-join products is incorrect: %s.' % _products
```

## Next Steps


---

*Source: test_join.py:372 | Complexity: Advanced | Last updated: 2026-05-18*