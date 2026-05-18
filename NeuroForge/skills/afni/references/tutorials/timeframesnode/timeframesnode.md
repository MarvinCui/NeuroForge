# How To: Timeframesnode

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: test TimeFramesNode

## Prerequisites

**Required Modules:**
- `mdp`
- `_tools`


## Step-by-Step Guide

### Step 1: Assign length = 14

```python
length = 14
```

**Verification:**
```python
assert_equal(out[-1, -1], -length + 1)
```

### Step 2: Assign gap = 6

```python
gap = 6
```

**Verification:**
```python
assert_array_equal(out[:, 2 * i], out[:, 0] + i * gap)
```

### Step 3: Assign time_frames = 3

```python
time_frames = 3
```

**Verification:**
```python
assert_array_equal(out[:, 2 * i + 1], out[:, 1] - i * gap)
```

### Step 4: Assign inp = value

```python
inp = numx.array([numx.arange(length), -numx.arange(length)]).T
```

**Verification:**
```python
assert_equal(rec.shape[1], inp.shape[1])
```

### Step 5: Assign tf = mdp.nodes.TimeFramesNode(...)

```python
tf = mdp.nodes.TimeFramesNode(time_frames, gap)
```

**Verification:**
```python
assert_array_equal(rec[i:i + block_size], inp[i:i + block_size])
```

### Step 6: Assign out = tf.execute(...)

```python
out = tf.execute(inp)
```

### Step 7: Call assert_equal()

```python
assert_equal(out[-1, -1], -length + 1)
```

### Step 8: Assign rec = tf.pseudo_inverse(...)

```python
rec = tf.pseudo_inverse(out)
```

### Step 9: Call assert_equal()

```python
assert_equal(rec.shape[1], inp.shape[1])
```

### Step 10: Assign block_size = min(...)

```python
block_size = min(out.shape[0], gap)
```

### Step 11: Call assert_array_equal()

```python
assert_array_equal(out[:, 2 * i], out[:, 0] + i * gap)
```

### Step 12: Call assert_array_equal()

```python
assert_array_equal(out[:, 2 * i + 1], out[:, 1] - i * gap)
```

### Step 13: Call assert_array_equal()

```python
assert_array_equal(rec[i:i + block_size], inp[i:i + block_size])
```


## Complete Example

```python
# Workflow
length = 14
gap = 6
time_frames = 3
inp = numx.array([numx.arange(length), -numx.arange(length)]).T
tf = mdp.nodes.TimeFramesNode(time_frames, gap)
out = tf.execute(inp)
assert_equal(out[-1, -1], -length + 1)
for i in xrange(1, time_frames):
    assert_array_equal(out[:, 2 * i], out[:, 0] + i * gap)
    assert_array_equal(out[:, 2 * i + 1], out[:, 1] - i * gap)
rec = tf.pseudo_inverse(out)
assert_equal(rec.shape[1], inp.shape[1])
block_size = min(out.shape[0], gap)
for i in xrange(0, length, gap):
    assert_array_equal(rec[i:i + block_size], inp[i:i + block_size])
```

## Next Steps


---

*Source: test_TimeFrameNode.py:4 | Complexity: Advanced | Last updated: 2026-05-18*