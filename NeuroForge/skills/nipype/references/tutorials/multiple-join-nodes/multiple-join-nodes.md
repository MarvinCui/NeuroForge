# How To: Multiple Join Nodes

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test two join nodes, one downstream of the other.

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

### Step 1: 'Test two join nodes, one downstream of the other.'

```python
'Test two join nodes, one downstream of the other.'
```

**Verification:**
```python
assert len(result.nodes()) == 8, 'The number of expanded nodes is incorrect.'
```

### Step 2: Assign _products = value

```python
_products = []
```

**Verification:**
```python
assert _products == [81], 'The post-join product is incorrect'
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
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
```

### Step 6: Assign inputspec.iterables = value

```python
inputspec.iterables = [('n', [1, 2, 3])]
```

### Step 7: Assign pre_join1 = pe.Node(...)

```python
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
```

### Step 8: Call wf.connect()

```python
wf.connect(inputspec, 'n', pre_join1, 'input1')
```

### Step 9: Assign join1 = pe.JoinNode(...)

```python
join1 = pe.JoinNode(IdentityInterface(fields=['vector']), joinsource='inputspec', joinfield='vector', name='join1')
```

### Step 10: Call wf.connect()

```python
wf.connect(pre_join1, 'output1', join1, 'vector')
```

### Step 11: Assign post_join1 = pe.Node(...)

```python
post_join1 = pe.Node(SumInterface(), name='post_join1')
```

### Step 12: Call wf.connect()

```python
wf.connect(join1, 'vector', post_join1, 'input1')
```

### Step 13: Assign join2 = pe.JoinNode(...)

```python
join2 = pe.JoinNode(IdentityInterface(fields=['vector', 'scalar']), joinsource='inputspec', joinfield='vector', name='join2')
```

### Step 14: Call wf.connect()

```python
wf.connect(pre_join1, 'output1', join2, 'vector')
```

### Step 15: Call wf.connect()

```python
wf.connect(post_join1, 'output1', join2, 'scalar')
```

### Step 16: Assign post_join2 = pe.Node(...)

```python
post_join2 = pe.Node(SumInterface(), name='post_join2')
```

### Step 17: Call wf.connect()

```python
wf.connect(join2, 'vector', post_join2, 'input1')
```

### Step 18: Assign post_join3 = pe.Node(...)

```python
post_join3 = pe.Node(ProductInterface(), name='post_join3')
```

### Step 19: Call wf.connect()

```python
wf.connect(post_join2, 'output1', post_join3, 'input1')
```

### Step 20: Call wf.connect()

```python
wf.connect(join2, 'scalar', post_join3, 'input2')
```

### Step 21: Assign result = wf.run(...)

```python
result = wf.run()
```

**Verification:**
```python
assert len(result.nodes()) == 8, 'The number of expanded nodes is incorrect.'
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test two join nodes, one downstream of the other.'
global _products
_products = []
tmpdir.chdir()
wf = pe.Workflow(name='test')
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
inputspec.iterables = [('n', [1, 2, 3])]
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
wf.connect(inputspec, 'n', pre_join1, 'input1')
join1 = pe.JoinNode(IdentityInterface(fields=['vector']), joinsource='inputspec', joinfield='vector', name='join1')
wf.connect(pre_join1, 'output1', join1, 'vector')
post_join1 = pe.Node(SumInterface(), name='post_join1')
wf.connect(join1, 'vector', post_join1, 'input1')
join2 = pe.JoinNode(IdentityInterface(fields=['vector', 'scalar']), joinsource='inputspec', joinfield='vector', name='join2')
wf.connect(pre_join1, 'output1', join2, 'vector')
wf.connect(post_join1, 'output1', join2, 'scalar')
post_join2 = pe.Node(SumInterface(), name='post_join2')
wf.connect(join2, 'vector', post_join2, 'input1')
post_join3 = pe.Node(ProductInterface(), name='post_join3')
wf.connect(post_join2, 'output1', post_join3, 'input1')
wf.connect(join2, 'scalar', post_join3, 'input2')
result = wf.run()
assert len(result.nodes()) == 8, 'The number of expanded nodes is incorrect.'
assert _products == [81], 'The post-join product is incorrect'
```

## Next Steps


---

*Source: test_join.py:277 | Complexity: Advanced | Last updated: 2026-05-18*