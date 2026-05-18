# How To: Audioclip Attrib

**Difficulty**: Advanced
**Estimated Time**: 20 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test `AudioClip` attribute setters and getters. Tests attributes
`samples`, `sampleRateHz`, `duration`, and `gain()`.

## Prerequisites

**Required Modules:**
- `os`
- `tempfile`
- `pytest`
- `numpy`
- `psychopy`
- `psychopy.sound`


## Step-by-Step Guide

### Step 1: 'Test `AudioClip` attribute setters and getters. Tests attributes\n    `samples`, `sampleRateHz`, `duration`, and `gain()`.\n    '

```python
'Test `AudioClip` attribute setters and getters. Tests attributes\n    `samples`, `sampleRateHz`, `duration`, and `gain()`.\n    '
```

**Verification:**
```python
assert audioClip.duration > originalDuration
```

### Step 2: Assign originalDuration = 1.0

```python
originalDuration = 1.0
```

**Verification:**
```python
assert np.isclose(audioClip.duration, SAMPLE_RATE_48kHz / SAMPLE_RATE_16kHz)
```

### Step 3: Assign originalSampleRateHz = SAMPLE_RATE_48kHz

```python
originalSampleRateHz = SAMPLE_RATE_48kHz
```

**Verification:**
```python
assert np.isclose(originalDuration / 2.0, audioClip.duration)
```

### Step 4: Assign audioClip = AudioClip.sine(...)

```python
audioClip = AudioClip.sine(duration=originalDuration, sampleRateHz=originalSampleRateHz, gain=0.8)
```

**Verification:**
```python
assert np.max(audioClip.samples) <= 0.81 and np.min(audioClip.samples) >= -0.81
```

### Step 5: Assign audioClip.sampleRateHz = SAMPLE_RATE_16kHz

```python
audioClip.sampleRateHz = SAMPLE_RATE_16kHz
```

**Verification:**
```python
assert np.max(audioClip.samples) <= 1.0 and np.min(audioClip.samples) >= -1.0
```

### Step 6: Assign audioClip.sampleRateHz = SAMPLE_RATE_48kHz

```python
audioClip.sampleRateHz = SAMPLE_RATE_48kHz
```

**Verification:**
```python
assert caughtChannelValueError, 'Failed to catch error be specifying wrong number to `channel` param in `.gain()`.'
```

### Step 7: Assign trimAt = int(...)

```python
trimAt = int(audioClip.samples.shape[0] / 2.0)
```

### Step 8: Assign audioClip.samples = value

```python
audioClip.samples = audioClip.samples[:trimAt, :]
```

**Verification:**
```python
assert np.isclose(originalDuration / 2.0, audioClip.duration)
```

### Step 9: Call audioClip.gain()

```python
audioClip.gain(0.2)
```

**Verification:**
```python
assert np.max(audioClip.samples) <= 1.0 and np.min(audioClip.samples) >= -1.0
```

### Step 10: Assign caughtChannelValueError = False

```python
caughtChannelValueError = False
```

**Verification:**
```python
assert caughtChannelValueError, 'Failed to catch error be specifying wrong number to `channel` param in `.gain()`.'
```

### Step 11: Call audioClip.gain()

```python
audioClip.gain(1.0, channel=2)
```

### Step 12: Assign caughtChannelValueError = True

```python
caughtChannelValueError = True
```


## Complete Example

```python
# Workflow
'Test `AudioClip` attribute setters and getters. Tests attributes\n    `samples`, `sampleRateHz`, `duration`, and `gain()`.\n    '
originalDuration = 1.0
originalSampleRateHz = SAMPLE_RATE_48kHz
audioClip = AudioClip.sine(duration=originalDuration, sampleRateHz=originalSampleRateHz, gain=0.8)
audioClip.sampleRateHz = SAMPLE_RATE_16kHz
assert audioClip.duration > originalDuration
assert np.isclose(audioClip.duration, SAMPLE_RATE_48kHz / SAMPLE_RATE_16kHz)
audioClip.sampleRateHz = SAMPLE_RATE_48kHz
trimAt = int(audioClip.samples.shape[0] / 2.0)
audioClip.samples = audioClip.samples[:trimAt, :]
assert np.isclose(originalDuration / 2.0, audioClip.duration)
assert np.max(audioClip.samples) <= 0.81 and np.min(audioClip.samples) >= -0.81
audioClip.gain(0.2)
assert np.max(audioClip.samples) <= 1.0 and np.min(audioClip.samples) >= -1.0
caughtChannelValueError = False
try:
    audioClip.gain(1.0, channel=2)
except ValueError:
    caughtChannelValueError = True
assert caughtChannelValueError, 'Failed to catch error be specifying wrong number to `channel` param in `.gain()`.'
```

## Next Steps


---

*Source: test_audioclip.py:126 | Complexity: Advanced | Last updated: 2026-05-18*