# How To: Simple Extension

**Difficulty**: Intermediate
**Estimated Time**: 10 minutes
**Tags**: workflow, integration

## Overview

Workflow: test simple extension

## Prerequisites

**Required Modules:**
- `__future__`
- `mdp`
- `inspect`
- `py.test`


## Step-by-Step Guide

### Step 1: Assign node = mdp.nodes.IdentityNode(...)

```python
node = mdp.nodes.IdentityNode()
```

**Verification:**
```python
assert mdp.numx.all(node.execute(X) == X)
```

### Step 2: Assign node = Dummy(...)

```python
node = Dummy()
```

**Verification:**
```python
assert not hasattr(node, 'foo')
```

### Step 3: Assign extension_name = '__test'

```python
extension_name = '__test'
```

**Verification:**
```python
assert mdp.numx.all(node.execute(X) == X)
```

### Step 4: Assign self.foo = 42

```python
self.foo = 42
```

**Verification:**
```python
assert hasattr(node, 'foo')
```


## Complete Example

```python
# Workflow
class TestExtensionNode(mdp.ExtensionNode, mdp.nodes.IdentityNode):
    extension_name = '__test'

    def execute(self, x):
        self.foo = 42
        return self._non_extension_execute(x)

class Dummy(mdp.nodes.IdentityNode):

    def _execute(self, x):
        return 42
node = mdp.nodes.IdentityNode()
assert mdp.numx.all(node.execute(X) == X)
assert not hasattr(node, 'foo')
with mdp.extension('__test'):
    assert mdp.numx.all(node.execute(X) == X)
    assert hasattr(node, 'foo')
node = Dummy()
assert not hasattr(node, 'foo')
assert node.execute(X) == 42
with mdp.extension('__test'):
    assert node.execute(X) == 42
    assert hasattr(node, 'foo')
```

## Next Steps


---

*Source: test_metaclass_and_extensions.py:72 | Complexity: Intermediate | Last updated: 2026-05-18*