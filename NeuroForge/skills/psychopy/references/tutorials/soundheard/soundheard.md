# How To: Soundheard

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: workflow, integration

## Overview

Workflow: Check that the sound sensor validator detects a sound played from an audible speaker.

## Prerequisites

**Required Modules:**
- `pytest`
- `psychopy`
- `psychopy.hardware`


## Step-by-Step Guide

### Step 1: '\n        Check that the sound sensor validator detects a sound played from an audible speaker.\n        '

```python
'\n        Check that the sound sensor validator detects a sound played from an audible speaker.\n        '
```

**Verification:**
```python
assert self.validator.valid
```

### Step 2: Assign clock = core.Clock(...)

```python
clock = core.Clock()
```

**Verification:**
```python
assert self.validator.valid
```

### Step 3: Call self.validator.resetTimer()

```python
self.validator.resetTimer(clock)
```

**Verification:**
```python
assert self.validator.tStart is not None
```

### Step 4: Assign t = 0

```python
t = 0
```

**Verification:**
```python
assert self.validator.tStop is not None
```

### Step 5: Assign snd = sound.Sound(...)

```python
snd = sound.Sound('A', speaker=self.speaker)
```

### Step 6: Assign snd.tStart, snd.tStop = None

```python
snd.tStart = snd.tStop = None
```

### Step 7: Assign snd.status, self.validator.status = value

```python
snd.status = self.validator.status = constants.NOT_STARTED
```

**Verification:**
```python
assert self.validator.tStart is not None
```

### Step 8: Assign t = clock.getTime(...)

```python
t = clock.getTime()
```

### Step 9: Assign unknown = self.validator.validate(...)

```python
self.validator.tStart, self.validator.valid = self.validator.validate(state=True, t=snd.tStart, adjustment=0.12)
```

### Step 10: Assign unknown = self.validator.validate(...)

```python
self.validator.tStop, self.validator.valid = self.validator.validate(state=False, t=snd.tStop, adjustment=0)
```

### Step 11: Call snd.play()

```python
snd.play()
```

### Step 12: Assign snd.tStart = t

```python
snd.tStart = t
```

### Step 13: Assign snd.status = value

```python
snd.status = constants.STARTED
```

### Step 14: Assign self.validator.status = value

```python
self.validator.status = constants.STARTED
```

### Step 15: Call snd.stop()

```python
snd.stop()
```

### Step 16: Assign snd.tStop = t

```python
snd.tStop = t
```

### Step 17: Assign snd.status = value

```python
snd.status = constants.FINISHED
```

### Step 18: Assign self.validator.status = value

```python
self.validator.status = constants.STARTED
```

### Step 19: Assign self.validator.status = value

```python
self.validator.status = constants.FINISHED
```

**Verification:**
```python
assert self.validator.valid
```

### Step 20: Assign self.validator.status = value

```python
self.validator.status = constants.FINISHED
```

**Verification:**
```python
assert self.validator.valid
```


## Complete Example

```python
# Workflow
'\n        Check that the sound sensor validator detects a sound played from an audible speaker.\n        '
clock = core.Clock()
self.validator.resetTimer(clock)
t = 0
snd = sound.Sound('A', speaker=self.speaker)
snd.tStart = snd.tStop = None
snd.status = self.validator.status = constants.NOT_STARTED
while t < 3:
    t = clock.getTime()
    if self.validator.status == constants.STARTED and snd.status == constants.STARTED:
        self.validator.tStart, self.validator.valid = self.validator.validate(state=True, t=snd.tStart, adjustment=0.12)
        if self.validator.tStart:
            self.validator.status = constants.FINISHED
            assert self.validator.valid
    if self.validator.status == constants.STARTED and snd.status == constants.FINISHED:
        self.validator.tStop, self.validator.valid = self.validator.validate(state=False, t=snd.tStop, adjustment=0)
        if self.validator.tStop:
            self.validator.status = constants.FINISHED
            assert self.validator.valid
    if snd.status == constants.NOT_STARTED and t > 1:
        snd.play()
        snd.tStart = t
        snd.status = constants.STARTED
        self.validator.status = constants.STARTED
    if snd.status == constants.STARTED and t > 2:
        snd.stop()
        snd.tStop = t
        snd.status = constants.FINISHED
        self.validator.status = constants.STARTED
assert self.validator.tStart is not None
assert self.validator.tStop is not None
```

## Next Steps


---

*Source: test_voicekeyValidator.py:45 | Complexity: Advanced | Last updated: 2026-05-18*