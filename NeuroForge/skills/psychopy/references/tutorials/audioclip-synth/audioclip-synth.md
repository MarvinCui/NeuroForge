# How To: Audioclip Synth

**Difficulty**: Advanced
**Estimated Time**: 15 minutes
**Tags**: pytest, workflow, integration

## Overview

Workflow: Test `AudioClip` static methods for sound generation. Just check if the
sounds created give back data structured as expected. Not testing if the
contents are correctly generated (yet).

## Prerequisites

**Required Modules:**
- `os`
- `tempfile`
- `pytest`
- `numpy`
- `psychopy`
- `psychopy.sound`


## Step-by-Step Guide

### Step 1: 'Test `AudioClip` static methods for sound generation. Just check if the\n    sounds created give back data structured as expected. Not testing if the\n    contents are correctly generated (yet).\n    '

```python
'Test `AudioClip` static methods for sound generation. Just check if the\n    sounds created give back data structured as expected. Not testing if the\n    contents are correctly generated (yet).\n    '
```

**Verification:**
```python
assert whiteNoise.channels == nChannels
```

### Step 2: Assign duration = 0.25

```python
duration = 0.25
```

**Verification:**
```python
assert np.isclose(whiteNoise.duration, duration)
```

### Step 3: Assign rates = value

```python
rates = (SAMPLE_RATE_16kHz, SAMPLE_RATE_48kHz, SAMPLE_RATE_96kHz)
```

**Verification:**
```python
assert silence.channels == nChannels
```

### Step 4: Assign whiteNoise = AudioClip.whiteNoise(...)

```python
whiteNoise = AudioClip.whiteNoise(duration=duration, sampleRateHz=sampleRateHz, channels=nChannels)
```

**Verification:**
```python
assert np.isclose(silence.duration, duration)
```

### Step 5: Assign silence = AudioClip.silence(...)

```python
silence = AudioClip.silence(duration=duration, sampleRateHz=sampleRateHz, channels=nChannels)
```

**Verification:**
```python
assert sineWave.channels == nChannels
```

### Step 6: Assign sineWave = AudioClip.sine(...)

```python
sineWave = AudioClip.sine(duration=duration, freqHz=440, gain=1.0, sampleRateHz=sampleRateHz, channels=nChannels)
```

**Verification:**
```python
assert np.isclose(sineWave.duration, duration)
```

### Step 7: Assign squareWave = AudioClip.square(...)

```python
squareWave = AudioClip.square(duration=duration, freqHz=440, dutyCycle=0.5, gain=1.0, sampleRateHz=sampleRateHz, channels=nChannels)
```

**Verification:**
```python
assert squareWave.channels == nChannels
```

### Step 8: Assign sawtoothWave = AudioClip.sawtooth(...)

```python
sawtoothWave = AudioClip.sawtooth(duration=duration, freqHz=440, peak=1.0, gain=1.0, sampleRateHz=sampleRateHz, channels=nChannels)
```

**Verification:**
```python
assert np.isclose(squareWave.duration, duration)
```


## Complete Example

```python
# Workflow
'Test `AudioClip` static methods for sound generation. Just check if the\n    sounds created give back data structured as expected. Not testing if the\n    contents are correctly generated (yet).\n    '
duration = 0.25
rates = (SAMPLE_RATE_16kHz, SAMPLE_RATE_48kHz, SAMPLE_RATE_96kHz)
for sampleRateHz in rates:
    for nChannels in (AUDIO_CHANNELS_MONO, AUDIO_CHANNELS_STEREO):
        whiteNoise = AudioClip.whiteNoise(duration=duration, sampleRateHz=sampleRateHz, channels=nChannels)
        assert whiteNoise.channels == nChannels
        assert np.isclose(whiteNoise.duration, duration)
        silence = AudioClip.silence(duration=duration, sampleRateHz=sampleRateHz, channels=nChannels)
        assert silence.channels == nChannels
        assert np.isclose(silence.duration, duration)
        sineWave = AudioClip.sine(duration=duration, freqHz=440, gain=1.0, sampleRateHz=sampleRateHz, channels=nChannels)
        assert sineWave.channels == nChannels
        assert np.isclose(sineWave.duration, duration)
        squareWave = AudioClip.square(duration=duration, freqHz=440, dutyCycle=0.5, gain=1.0, sampleRateHz=sampleRateHz, channels=nChannels)
        assert squareWave.channels == nChannels
        assert np.isclose(squareWave.duration, duration)
        sawtoothWave = AudioClip.sawtooth(duration=duration, freqHz=440, peak=1.0, gain=1.0, sampleRateHz=sampleRateHz, channels=nChannels)
        assert sawtoothWave.channels == nChannels
        assert np.isclose(sawtoothWave.duration, duration)
```

## Next Steps


---

*Source: test_audioclip.py:55 | Complexity: Advanced | Last updated: 2026-05-18*