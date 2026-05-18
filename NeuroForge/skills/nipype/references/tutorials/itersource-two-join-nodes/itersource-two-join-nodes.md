# How To: Itersource Two Join Nodes

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test join with a midstream ``itersource`` and an upstream
iterable.

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

### Step 1: 'Test join with a midstream ``itersource`` and an upstream\n    iterable.'

```python
'Test join with a midstream ``itersource`` and an upstream\n    iterable.'
```

**Verification:**
```python
assert len(result.nodes()) == 15, 'The number of expanded nodes is incorrect.'
```

### Step 2: Call tmpdir.chdir()

```python
tmpdir.chdir()
```

### Step 3: Assign wf = pe.Workflow(...)

```python
wf = pe.Workflow(name='test')
```

### Step 4: Assign inputspec = pe.Node(...)

```python
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
```

### Step 5: Assign inputspec.iterables = value

```python
inputspec.iterables = [('n', [1, 2])]
```

### Step 6: Assign pre_join1 = pe.Node(...)

```python
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
```

### Step 7: Call wf.connect()

```python
wf.connect(inputspec, 'n', pre_join1, 'input1')
```

### Step 8: Assign pre_join2 = pe.Node(...)

```python
pre_join2 = pe.Node(ProductInterface(), name='pre_join2')
```

### Step 9: Assign pre_join2.itersource = value

```python
pre_join2.itersource = ('inputspec', 'n')
```

### Step 10: Assign pre_join2.iterables = value

```python
pre_join2.iterables = ('input1', {1: [3, 4], 2: [5, 6]})
```

### Step 11: Call wf.connect()

```python
wf.connect(pre_join1, 'output1', pre_join2, 'input2')
```

### Step 12: Assign pre_join3 = pe.Node(...)

```python
pre_join3 = pe.Node(IncrementInterface(), name='pre_join3')
```

### Step 13: Call wf.connect()

```python
wf.connect(pre_join2, 'output1', pre_join3, 'input1')
```

### Step 14: Assign join1 = pe.JoinNode(...)

```python
join1 = pe.JoinNode(IdentityInterface(fields=['vector']), joinsource='pre_join2', joinfield='vector', name='join1')
```

### Step 15: Call wf.connect()

```python
wf.connect(pre_join3, 'output1', join1, 'vector')
```

### Step 16: Assign post_join1 = pe.Node(...)

```python
post_join1 = pe.Node(SumInterface(), name='post_join1')
```

### Step 17: Call wf.connect()

```python
wf.connect(join1, 'vector', post_join1, 'input1')
```

### Step 18: Assign join2 = pe.JoinNode(...)

```python
join2 = pe.JoinNode(IdentityInterface(fields=['vector']), joinsource='inputspec', joinfield='vector', name='join2')
```

### Step 19: Call wf.connect()

```python
wf.connect(post_join1, 'output1', join2, 'vector')
```

### Step 20: Assign result = wf.run(...)

```python
result = wf.run()
```

**Verification:**
```python
assert len(result.nodes()) == 15, 'The number of expanded nodes is incorrect.'
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test join with a midstream ``itersource`` and an upstream\n    iterable.'
tmpdir.chdir()
wf = pe.Workflow(name='test')
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
inputspec.iterables = [('n', [1, 2])]
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
wf.connect(inputspec, 'n', pre_join1, 'input1')
pre_join2 = pe.Node(ProductInterface(), name='pre_join2')
pre_join2.itersource = ('inputspec', 'n')
pre_join2.iterables = ('input1', {1: [3, 4], 2: [5, 6]})
wf.connect(pre_join1, 'output1', pre_join2, 'input2')
pre_join3 = pe.Node(IncrementInterface(), name='pre_join3')
wf.connect(pre_join2, 'output1', pre_join3, 'input1')
join1 = pe.JoinNode(IdentityInterface(fields=['vector']), joinsource='pre_join2', joinfield='vector', name='join1')
wf.connect(pre_join3, 'output1', join1, 'vector')
post_join1 = pe.Node(SumInterface(), name='post_join1')
wf.connect(join1, 'vector', post_join1, 'input1')
join2 = pe.JoinNode(IdentityInterface(fields=['vector']), joinsource='inputspec', joinfield='vector', name='join2')
wf.connect(post_join1, 'output1', join2, 'vector')
result = wf.run()
assert len(result.nodes()) == 15, 'The number of expanded nodes is incorrect.'
```

## Next Steps


---

*Source: test_join.py:511 | Complexity: Advanced | Last updated: 2026-05-18*