# How To: Set Join Node

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: workflow, integration

## Overview

Workflow: Test collecting join inputs to a set.

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

### Step 1: 'Test collecting join inputs to a set.'

```python
'Test collecting join inputs to a set.'
```

**Verification:**
```python
assert _set_len == 3, 'The join Set output value is incorrect: %s.' % _set_len
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
inputspec.iterables = [('n', [1, 2, 1, 3, 2])]
```

### Step 6: Assign pre_join1 = pe.Node(...)

```python
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
```

### Step 7: Call wf.connect()

```python
wf.connect(inputspec, 'n', pre_join1, 'input1')
```

### Step 8: Assign join = pe.JoinNode(...)

```python
join = pe.JoinNode(SetInterface(), joinsource='inputspec', joinfield='input1', name='join')
```

### Step 9: Call wf.connect()

```python
wf.connect(pre_join1, 'output1', join, 'input1')
```

### Step 10: Call wf.run()

```python
wf.run()
```

**Verification:**
```python
assert _set_len == 3, 'The join Set output value is incorrect: %s.' % _set_len
```


## Complete Example

```python
# Setup
# Fixtures: tmpdir

# Workflow
'Test collecting join inputs to a set.'
tmpdir.chdir()
wf = pe.Workflow(name='test')
inputspec = pe.Node(IdentityInterface(fields=['n']), name='inputspec')
inputspec.iterables = [('n', [1, 2, 1, 3, 2])]
pre_join1 = pe.Node(IncrementInterface(), name='pre_join1')
wf.connect(inputspec, 'n', pre_join1, 'input1')
join = pe.JoinNode(SetInterface(), joinsource='inputspec', joinfield='input1', name='join')
wf.connect(pre_join1, 'output1', join, 'input1')
wf.run()
assert _set_len == 3, 'The join Set output value is incorrect: %s.' % _set_len
```

## Next Steps


---

*Source: test_join.py:222 | Complexity: Advanced | Last updated: 2026-05-18*