# How To: Audioclip Create

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Create an audio clip object and see if the properties are correct. Basic
stress test to check if we get the value we expect.

## Prerequisites

**Required Modules:**
- `os`
- `tempfile`
- `pytest`
- `numpy`
- `psychopy`
- `psychopy.sound`


## Step-by-Step Guide

### Step 1: 'Create an audio clip object and see if the properties are correct. Basic\n    stress test to check if we get the value we expect.\n    '

```python
'Create an audio clip object and see if the properties are correct. Basic\n    stress test to check if we get the value we expect.\n    '
```

**Verification:**
```python
assert audioClip.channels == nChannels
```

### Step 2: Assign nSamples = 1024

```python
nSamples = 1024
```

**Verification:**
```python
assert np.isclose(audioClip.duration, duration)
```

### Step 3: Assign rates = value

```python
rates = (SAMPLE_RATE_16kHz, SAMPLE_RATE_48kHz, SAMPLE_RATE_96kHz)
```

**Verification:**
```python
assert audioClip.isMono
```

### Step 4: Assign duration = value

```python
duration = nSamples / float(samplesRateHz)
```

**Verification:**
```python
assert np.allclose(monoClip.samples, audioClip.samples)
```

### Step 5: Assign audioClip = AudioClip(...)

```python
audioClip = AudioClip(samples=np.zeros((nSamples, nChannels)), sampleRateHz=samplesRateHz)
```

**Verification:**
```python
assert audioClip.isStereo
```

### Step 6: Assign monoClip = audioClip.asMono(...)

```python
monoClip = audioClip.asMono()
```

**Verification:**
```python
assert np.allclose(monoClip.samples, audioClip.samples)
```

### Step 7: Assign monoClip = audioClip.asMono(...)

```python
monoClip = audioClip.asMono()
```

### Step 8: Assign audioClip = audioClip.asMono(...)

```python
audioClip = audioClip.asMono(copy=False)
```

**Verification:**
```python
assert np.allclose(monoClip.samples, audioClip.samples)
```


## Complete Example

```python
# Workflow
'Create an audio clip object and see if the properties are correct. Basic\n    stress test to check if we get the value we expect.\n    '
nSamples = 1024
rates = (SAMPLE_RATE_16kHz, SAMPLE_RATE_48kHz, SAMPLE_RATE_96kHz)
for samplesRateHz in rates:
    duration = nSamples / float(samplesRateHz)
    for nChannels in (AUDIO_CHANNELS_MONO, AUDIO_CHANNELS_STEREO):
        audioClip = AudioClip(samples=np.zeros((nSamples, nChannels)), sampleRateHz=samplesRateHz)
        assert audioClip.channels == nChannels
        assert np.isclose(audioClip.duration, duration)
        if audioClip.channels == AUDIO_CHANNELS_MONO:
            assert audioClip.isMono
            monoClip = audioClip.asMono()
            assert np.allclose(monoClip.samples, audioClip.samples)
        elif audioClip.channels == AUDIO_CHANNELS_STEREO:
            assert audioClip.isStereo
            monoClip = audioClip.asMono()
            audioClip = audioClip.asMono(copy=False)
            assert np.allclose(monoClip.samples, audioClip.samples)
```

## Next Steps


---

*Source: test_audioclip.py:18 | Complexity: Advanced | Last updated: 2026-05-18*