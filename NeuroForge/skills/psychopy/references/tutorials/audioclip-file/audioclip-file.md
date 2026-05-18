# How To: Audioclip File

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test saving and loading audio samples from files. Checks the integrity
of loaded data to ensure things are similar to the original.

## Prerequisites

**Required Modules:**
- `os`
- `tempfile`
- `pytest`
- `numpy`
- `psychopy`
- `psychopy.sound`


## Step-by-Step Guide

### Step 1: 'Test saving and loading audio samples from files. Checks the integrity\n    of loaded data to ensure things are similar to the original.\n    '

```python
'Test saving and loading audio samples from files. Checks the integrity\n    of loaded data to ensure things are similar to the original.\n    '
```

**Verification:**
```python
assert np.allclose(loadedAudioClip.samples, audioClip.samples, atol=0.0001)
```

### Step 2: Call np.random.seed()

```python
np.random.seed(123456)
```

**Verification:**
```python
assert loadedAudioClip.channels == nChannels
```

### Step 3: Assign rates = value

```python
rates = (SAMPLE_RATE_16kHz, SAMPLE_RATE_48kHz, SAMPLE_RATE_96kHz)
```

**Verification:**
```python
assert np.allclose(loadedAudioClip.samples, loadedAudioClip2.samples)
```

### Step 4: Assign audioClip = AudioClip.whiteNoise(...)

```python
audioClip = AudioClip.whiteNoise(duration=1.0, sampleRateHz=sampleRateHz, channels=nChannels)
```

**Verification:**
```python
assert loadedAudioClip2.channels == nChannels
```

### Step 5: Assign testDir = mkdtemp(...)

```python
testDir = mkdtemp(prefix='psychopy-tests-test_audioclip')
```

### Step 6: Assign fname = os.path.join(...)

```python
fname = os.path.join(testDir, 'test_audioclip_file.wav')
```

### Step 7: Call audioClip.save()

```python
audioClip.save(fname)
```

### Step 8: Assign loadedAudioClip = AudioClip.load(...)

```python
loadedAudioClip = AudioClip.load(fname)
```

**Verification:**
```python
assert np.allclose(loadedAudioClip.samples, audioClip.samples, atol=0.0001)
```

### Step 9: Call loadedAudioClip.save()

```python
loadedAudioClip.save(fname)
```

### Step 10: Assign loadedAudioClip2 = AudioClip.load(...)

```python
loadedAudioClip2 = AudioClip.load(fname)
```

**Verification:**
```python
assert np.allclose(loadedAudioClip.samples, loadedAudioClip2.samples)
```


## Complete Example

```python
# Workflow
'Test saving and loading audio samples from files. Checks the integrity\n    of loaded data to ensure things are similar to the original.\n    '
np.random.seed(123456)
rates = (SAMPLE_RATE_16kHz, SAMPLE_RATE_48kHz, SAMPLE_RATE_96kHz)
for sampleRateHz in rates:
    for nChannels in (AUDIO_CHANNELS_MONO, AUDIO_CHANNELS_STEREO):
        audioClip = AudioClip.whiteNoise(duration=1.0, sampleRateHz=sampleRateHz, channels=nChannels)
        testDir = mkdtemp(prefix='psychopy-tests-test_audioclip')
        fname = os.path.join(testDir, 'test_audioclip_file.wav')
        audioClip.save(fname)
        loadedAudioClip = AudioClip.load(fname)
        assert np.allclose(loadedAudioClip.samples, audioClip.samples, atol=0.0001)
        assert loadedAudioClip.channels == nChannels
        loadedAudioClip.save(fname)
        loadedAudioClip2 = AudioClip.load(fname)
        assert np.allclose(loadedAudioClip.samples, loadedAudioClip2.samples)
        assert loadedAudioClip2.channels == nChannels
```

## Next Steps


---

*Source: test_audioclip.py:250 | Complexity: Advanced | Last updated: 2026-05-18*