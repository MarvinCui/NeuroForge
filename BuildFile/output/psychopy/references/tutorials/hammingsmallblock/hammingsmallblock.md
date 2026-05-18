# How To: Hammingsmallblock

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: test HammingSmallBlock

## Prerequisites

**Required Modules:**
- `psychopy.sound._base`
- `psychopy.constants`
- `psychopy.exceptions`
- `numpy`
- `pytest`
- `psychopy.sound`
- `matplotlib.pyplot`


## Step-by-Step Guide

### Step 1: Assign blockSize = 64

```python
blockSize = 64
```

### Step 2: Assign snd1 = apodize(...)

```python
snd1 = apodize(sndArray, sampleRate)
```

### Step 3: Assign sndDev = psychopy.sound.Sound(...)

```python
sndDev = psychopy.sound.Sound(thisFreq, sampleRate=sampleRate, secs=secs, hamming=True, blockSize=blockSize)
```

### Step 4: Assign snd2 = value

```python
snd2 = []
```

### Step 5: Assign snd2 = np.array(...)

```python
snd2 = np.array(snd2)
```

### Step 6: Assign block = sndDev._nextBlock(...)

```python
block = sndDev._nextBlock()
```

### Step 7: Call snd2.extend()

```python
snd2.extend(block)
```

### Step 8: Call plt.subplot()

```python
plt.subplot(2, 1, 1)
```

### Step 9: Call plt.plot()

```python
plt.plot(snd1, 'b-')
```

### Step 10: Call plt.plot()

```python
plt.plot(snd2, 'r--')
```

### Step 11: Call plt.subplot()

```python
plt.subplot(2, 1, 2)
```

### Step 12: Call plt.plot()

```python
plt.plot(t, snd2[0:sampleRate * secs] - snd1)
```

### Step 13: Call plt.show()

```python
plt.show()
```


## Complete Example

```python
# Workflow
blockSize = 64
snd1 = apodize(sndArray, sampleRate)
sndDev = psychopy.sound.Sound(thisFreq, sampleRate=sampleRate, secs=secs, hamming=True, blockSize=blockSize)
snd2 = []
while sndDev.status != FINISHED:
    block = sndDev._nextBlock()
    snd2.extend(block)
snd2 = np.array(snd2)
if plotting:
    plt.subplot(2, 1, 1)
    plt.plot(snd1, 'b-')
    plt.plot(snd2, 'r--')
    plt.subplot(2, 1, 2)
    plt.plot(t, snd2[0:sampleRate * secs] - snd1)
    plt.show()
```

## Next Steps


---

*Source: test_hamming.py:28 | Complexity: Advanced | Last updated: 2026-05-18*