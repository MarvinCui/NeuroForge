# How To: Node Save

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test Node save

## Prerequisites

**Required Modules:**
- `__future__`
- `tempfile`
- `cPickle`
- `mdp`
- `_tools`
- `py.test`


## Step-by-Step Guide

### Step 1: Assign test_list = value

```python
test_list = [1, 2, 3]
```

**Verification:**
```python
assert generic_node.dummy_attr == copy_node.dummy_attr, 'Node save (string) method did not work'
```

### Step 2: Assign generic_node = mdp.Node(...)

```python
generic_node = mdp.Node()
```

**Verification:**
```python
assert generic_node.dummy_attr != copy_node.dummy_attr, 'Node save (string) method did not work'
```

### Step 3: Assign generic_node.dummy_attr = test_list

```python
generic_node.dummy_attr = test_list
```

**Verification:**
```python
assert generic_node.dummy_attr == copy_node.dummy_attr, 'Node save (file) method did not work'
```

### Step 4: Assign copy_node_pic = generic_node.save(...)

```python
copy_node_pic = generic_node.save(None)
```

**Verification:**
```python
assert generic_node.dummy_attr != copy_node.dummy_attr, 'Node save (file) method did not work'
```

### Step 5: Assign copy_node = cPickle.loads(...)

```python
copy_node = cPickle.loads(copy_node_pic)
```

**Verification:**
```python
assert generic_node.dummy_attr == copy_node.dummy_attr, 'Node save (string) method did not work'
```

### Step 6: Assign unknown = 10

```python
copy_node.dummy_attr[0] = 10
```

**Verification:**
```python
assert generic_node.dummy_attr != copy_node.dummy_attr, 'Node save (string) method did not work'
```

### Step 7: Assign dummy_file = tempfile.mktemp(...)

```python
dummy_file = tempfile.mktemp(prefix='MDP_', suffix='.pic', dir=py.test.mdp_tempdirname)
```

### Step 8: Call generic_node.save()

```python
generic_node.save(dummy_file, protocol=1)
```

### Step 9: Assign dummy_file = open(...)

```python
dummy_file = open(dummy_file, 'rb')
```

### Step 10: Assign copy_node = cPickle.load(...)

```python
copy_node = cPickle.load(dummy_file)
```

**Verification:**
```python
assert generic_node.dummy_attr == copy_node.dummy_attr, 'Node save (file) method did not work'
```

### Step 11: Assign unknown = 10

```python
copy_node.dummy_attr[0] = 10
```

**Verification:**
```python
assert generic_node.dummy_attr != copy_node.dummy_attr, 'Node save (file) method did not work'
```


## Complete Example

```python
# Workflow
test_list = [1, 2, 3]
generic_node = mdp.Node()
generic_node.dummy_attr = test_list
copy_node_pic = generic_node.save(None)
copy_node = cPickle.loads(copy_node_pic)
assert generic_node.dummy_attr == copy_node.dummy_attr, 'Node save (string) method did not work'
copy_node.dummy_attr[0] = 10
assert generic_node.dummy_attr != copy_node.dummy_attr, 'Node save (string) method did not work'
dummy_file = tempfile.mktemp(prefix='MDP_', suffix='.pic', dir=py.test.mdp_tempdirname)
generic_node.save(dummy_file, protocol=1)
dummy_file = open(dummy_file, 'rb')
copy_node = cPickle.load(dummy_file)
assert generic_node.dummy_attr == copy_node.dummy_attr, 'Node save (file) method did not work'
copy_node.dummy_attr[0] = 10
assert generic_node.dummy_attr != copy_node.dummy_attr, 'Node save (file) method did not work'
```

## Next Steps


---

*Source: test_node_operations.py:36 | Complexity: Advanced | Last updated: 2026-05-18*